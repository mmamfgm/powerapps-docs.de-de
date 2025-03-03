---
title: Übergeben von Daten von einer Seite als Parameter an Menüband-Aktionen (modellgestützte Apps) | Microsoft Docs
description: 'In diesem Thema werden die Optionen für die Verwendung des Elements <CrmParameter> zum Abrufen dieser Werte beschrieben. '
ms.custom: ''
ms.date: 02/15/2019
ms.reviewer: kvivek
ms.service: powerapps
ms.topic: article
author: hazhouMSFT
ms.author: hazhou
manager: annbe
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 329e9f1845bfdfc9f2afa87528fbfd10bc4aa886
ms.sourcegitcommit: d9cecdd5a35279d78aa1b6c9fc642e36a4e4612c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "2753602"
---
# <a name="pass-data-from-a-page-as-a-parameter-to-ribbon-actions"></a>Übergeben von Daten von einer Seite als Parameter an Menüband-Aktionen

Wenn Sie eine Aktion in einem Menüband definieren, müssen Sie oft Daten von der Seite entweder an eine JavaScript-Funktion oder eine URL übergeben. In diesem Thema werden die Optionen für die Verwendung des <[\<CrmParameter\>](https://msdn.microsoft.com/library/gg309332.aspx)Elements zum Abrufen dieser Werte beschrieben.

## <a name="form-and-grid-context-in-ribbon-actions"></a>Formular- und Rasterkontext in Menübandaktionen

Um im Ausführungskontext (*Formularkontext* oder *Rasterkontext*) Informationen an die JavaScript-Funktion für Ihre Ribbon-Aktionen zu übergeben, geben Sie **PrimaryControl** für den Formularkontext oder **SelectedControl** für den Gitterkontext als Wert `<CrmParameter>` in Ihrer Ribbondefinition an. **SelectedControl** wird im Grid-Kontext übergeben, sowohl für Teilraster als auch für Homepageraster. Der in **PrimaryControl** übergebene oder der **SelectedControl**-Wert wird als Argument in Ihrer JavaScript-Funktion für den *Formular*- bzw. *Rasterkontext* verwendet. 

Beispielsweise ist hier eine Beispielmenübanddefinition, wo wir den **PrimaryControl:** n Parameter an die JavaScript-Funktion geben:

```xml
<CommandDefinition Id="SampleCommand">
  <EnableRules/>
  <DisplayRules/>
  <Actions>
    <JavaScriptFunction Library="$webresource:new_mySampleScript.js" FunctionName="mySampleFunction">
      <CrmParameter Value="PrimaryControl" />
    </JavaScriptFunction>
  </Actions>
</CommandDefinition>
```

In der**new_mySampleScript.js** Webressourcedatei, die auf das Beispiel oben verweist, definieren Sie die JavaScript-Funktion mit der **primaryControl** Variable als Argument. Dieses Argument liefert den *Formularkontext*, in dem der Ribbon-Befehl ausgeführt wird:

```JavaScript
function mySampleFunction(primaryControl) {
    var formContext = primaryControl;
    // Perform operations using the formContext object
}
```

Sie können auch **CommandProperties** als `<CrmParameter>` Werte in der Menübanddefinition angeben, um Informationen zum Ereignis an das Menübandsteuerelement zu geben. Sie können dies verwenden, um Kontextinformationen an eine JavaScript Funktion zu senden, in der bestimmte Aktionen basierend auf dem Kontext des Ereignisses bestimmt werden können.

> [!NOTE]
> *Formularkontext*und *Rasterkontext* für JavaScript-Funktionen für Menübandaktionen abzurufen, ist jedoch unterschiedlich vom Abrufen dieser Werte in Formularskripts. Informationen über Formularskripts und wie Sie diese Kontexte erhalten, finden Sie unter [Client API Formularkontext](clientapi/clientapi-grid-context.md) und [Client API-Rasterkontext](clientapi/clientapi-form-context.md).

## <a name="form-values"></a>Formularwerte

Mit einem Formularmenüband können Sie die `data.entity`.[Attribut](clientapi/reference/attributes.md)-Sammlung und die `ui`.[Steuerungs](clientapi/reference/controls.md)-Sammlung verwenden, um Werte für bekannte Felder abzurufen. 

Beispielsweise zeigt der folgende Beispielcode an, wie das Firmennamefeld im Firmenformular abgerufen wird und wie Sie einen Wert im websiteurl Feld basierend auf dem Firmennamewert festlegen.

```JavaScript
function mySampleFunction(primaryControl) {
    var formContext = primaryControl;    
    var accountName = formContext.getControl("name").getAttribute().getValue();    

    // Set the WebSiteURL field if account name contains "Contoso"
    if (accountName.toLowerCase().search("contoso") != -1) {
        formContext.getAttribute("websiteurl").setValue("https://www.contoso.com");
    }
    else {
        Xrm.Navigation.openAlertDialog({ text: "Account name does not contain 'Contoso'." });
    }
}
```

  
## <a name="grid-values"></a>Rasterwerte  
 Die meisten der Werte, die für das `<CrmParameter>`-Element verfügbar sind, beziehen sich auf das Arbeiten mit Daten, die in einem Raster oder einem Hierarchiediagramm angezeigt werden. Durch Verwendung der`Value`-Attributaufzählungsoptionen können Sie problemlos Elemente isolieren, indem Sie folgendermaßen vorgehen:  
  
- **Ausgewählte Elemente**  
  
    -   SelectedControlSelectedItemCount  
  
    -   SelectedControlSelectedItemIds  
  
    -   SelectedControlSelectedItemReferences  
  
- **Alle Elemente**  
  
    -   SelectedControlAllItemCount  
  
    -   SelectedControlAllItemIds  
  
    -   SelectedControlAllItemReferences  
  
- **Nicht ausgewählte Elemente**  
  
    -   SelectedControlUnselectedItemCount  
  
    -   SelectedControlUnselectedItemIds  
  
    -   SelectedControlUnselectedItemReferences  
  
  Für jede dieser Gruppierungen können Sie die Anzahl der Elemente und den GUID-Bezeichner sammeln. Wenn Sie die Werte an eine URL übergeben, können Sie auch `EntityReference`-Objekte abrufen, die alle Informationen enthalten, die Sie benötigen, um die Objekte eindeutig zu identifizieren. Diese Parameter treffen zu, wenn die angezeigte Seite das das Hauptraster (`HomepageGrid`) oder ein Unterraster in einem Formular ist. Werden sie zusammen mit dem `SelectedEntityTypeName`-Parameter verwendet, haben Sie alle Informationen, die Sie an eine andere Anwendung übergeben müssen.  
  
 
  
## <a name="other-context-information"></a>Andere Kontextinformationen  
 Zusätzlich zu den Datenwerten können Sie zusätzliche Client-Kontextinformationen abrufen, indem Sie [\<CrmParameter\>](https://msdn.microsoft.com/library/gg309332.aspx) verwenden.  Die folgenden Optionen können als Wert für das `CrmParameter` Element: `OrgName`, `OrgLcid`und `UserLcid` verwendet werden.
 
 Für eine `<Url>`-Aktion können Sie auch das `PassParams`-Attribut verwenden, um kontextbezogenene Informationen zu berücksichtigen.  
  
 Die `Value`-Optionen `PrimaryEntityTypeName` und `FirstPrimaryItemId` stellen Informationen zu einem Entitätsdatensatz zur Verfügung. Sie können `PrimaryItemIds` für ein `HomepageGrid`-Menüband verwenden, um eine Liste aller angezeigten Elemente zu erhalten.
  
### <a name="see-also"></a>Siehe auch  
 [Anpassen des Menübands](customize-commands-ribbon.md)   
 [Parameter mit dem Menüband an eine URL übergeben](pass-parameters-url-by-using-ribbon.md)    
 [Definieren von Menübandaktionen](define-ribbon-actions.md)   
 [Festlegen benutzerdefinierter Aktionen zur Änderung des Menübands](define-custom-actions-modify-ribbon.md)<br>
 [Formularkontext der Client-API](clientapi/clientapi-form-context.md)<br>
 [Rasterkontext der Client-API](clientapi/clientapi-grid-context.md)<br>
 
