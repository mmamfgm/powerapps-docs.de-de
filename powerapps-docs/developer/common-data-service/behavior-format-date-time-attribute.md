---
title: Verhalten und Format des Datums- und Uhrzeitattributs (Common Data Service) | Microsoft-Dokumentation
description: Die Klasse "DateTimeAttributeMetadata" wird verwendet, um die Attribute des Typs DateTime im Common Data Service zu definieren und zu verwalten.
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: mayadumesh
ms.author: jdaly
manager: ryjones
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: a2f2fbbf8b541945d665cf9203c9f9112cdea1a4
ms.sourcegitcommit: 8185f87dddf05ee256491feab9873e9143535e02
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2019
ms.locfileid: "2748252"
---
# <a name="behavior-and-format-of-the-date-and-time-attribute"></a>Verhalten und Format des Datums- und Uhrzeitattributs

Wenn Sie Benutzer und Büros auf der ganzen Welt haben, ist es wichtig, Datums- und Uhrzeitwerte in mehreren Zeitzonen ordnungsgemäß darzustellen. Die `DateTimeAttributeMetadata` (<xref href="Microsoft.Dynamics.CRM.DateTimeAttributeMetadata?text=DateTimeAttributeMetadata EntityType" />- oder <xref:Microsoft.Xrm.Sdk.Metadata.DateTimeAttributeMetadata>-Klasse) wird verwendet, um die Attribute des Typs `DateTime` in Common Data Service zu definieren und zu verwalten. Verwenden Sie die `DateTimeBehavior`-Eigenschaft (Information zum Organisationsservice finden Sie unter <xref:Microsoft.Xrm.Sdk.Metadata.DateTimeAttributeMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.DateTimeAttributeMetadata.DateTimeBehavior>), um festzulegen, ob Datums- und Uhrzeitwert mit oder ohne Zeitzoneninformationen gespeichert werden, und verwenden Sie die `DateTimeAttributeMetadata.Format`-Eigenschaft, um das Anzeigeformat dieser Attribute anzugeben.  

  
 Sie können den Anpassungsbereich in Common Data Service auch verwenden, um das Verhalten und das Format der Datums- und Uhrzeitattribute zu definieren. Weitere Informationen: [Verhalten und Format des Datums- und Uhrzeitfelds](/dynamics365/customer-engagement/customize/behavior-format-date-time-field)  
  
> [!NOTE]
>  Alle Daten- und Zeitattribute in Common Data Service unterstützen Werte ab dem 1/1/1753 12:00 Uhr.  
  
<a name="SpecifyBehavior"></a>   

## <a name="specify-the-behavior-of-a-date-and-time-attribute"></a>Angeben des Verhaltens eines Datums- und Uhrzeitattributs

 Sie können die `DateTimeBehavior` (<xref href="Microsoft.Dynamics.CRM.DateTimeBehavior?text=DateTimeBehavior ComplexType" />- oder <xref:Microsoft.Xrm.Sdk.Metadata.DateTimeBehavior>-Klasse) verwenden, um einen Wert für die <xref href="Microsoft.Dynamics.CRM.DateTimeAttributeMetadata?text=DateTimeAttributeMetadata EntityType" />.DateTimeBehavior-Eigenschaft anzugeben. Die `DateTimeBehavior` enthält folgende Mitglieder; jedes Mitglied gibt eine Zeichenfolge mit demselben Wert wie dem Mitgliedsnamen zurück:  
  
|Mitgliedsname und Wert|Beschreibung|  
|---------------------------|-----------------|  
|`UserLocal`|-   Speichert den Datums- und Uhrzeitwert als UTC-Wert im System.<br />-   Der Abrufvorgang gibt den UTC-Wert zurück.<br />-   Der Aktualisierungsvorgang konvertiert den UTC-Wert in den Zeitzonenwert des aktuellen Benutzers und speichert dann den aktualisierten Wert im Istzustand oder als Entsprechung des UTC-Werts. Dies ist von dem Wertetyp abhängig ([DateTimeKind](https://msdn.microsoft.com/library/shx7s921.aspx)), der für den Aktualisierungsvorgang angegeben ist. Wenn der angegebene Wert dem UTC-Typ angehört, wird er im Istzustand gespeichert. Andernfalls wird der entsprechende UTC-Wert gespeichert.<br />-   Durch das Abrufen des formatierten Werts erfolgt eine Konvertierung von UTC in die aktuelle Zeitzone des Benutzers auf Grundlage der Zeitzonen- und Gebietsschemaeinstellung des Benutzers.<br />-   Für die Web-API wird das Attribut als DateTimeOffset verfügbar gemacht.<br />-   Dieses Verhalten wird für Systemattribute wie `CreatedOn` und `ModifiedOn` verwendet und kann nicht geändert werden. Außerdem sollte dieses Verhalten für benutzerdefinierte Attribute verwendet werden, in denen Sie Datums- und Uhrzeitwerte mit den Zeitzoneninformationen speichern.|  
|`DateOnly`|-   Speichert den tatsächlichen Datumswert mit dem Zeitwert als 00:00 Uhr (00:0000) im System.<br />-   Für Abruf- und Aktualisierungsvorgänge wird keine Zeitzonenkonvertierung ausgeführt, und der Zeitwert lautet immer 00:00 Uhr (00:00:00).<br />-   Das Abrufen des formatierten Werts zeigt den Datumswert ohne Zeitzonenkonvertierung an.<br />-   Für die Web-API wird das Attribut als DateTimeOffset verfügbar gemacht.<br />-   Dieses Verhalten sollte für benutzerdefinierte Attribute verwendet werden, die Geburtstage und Jahrestage speichern, bei denen die Zeitinformationen nicht erforderlich sind.|  
|`TimeZoneIndependent`|-   Speichert die tatsächlichen Datums- und Uhrzeitwerte im System unabhängig von der Benutzerzeitzone.<br />-   Für die Abruf- und Aktualisierungsvorgänge wird keine Zeitzonenkonvertierung durchgeführt. Es werden tatsächliche Datums- und Uhrzeitwerte im System zurückgegeben und aktualisiert, unabhängig von der Benutzerzeitzone.<br />-   Beim Abrufen des formatierten Werts wird der Datums- und Uhrzeitwert (ohne Zeitzonenkonvertierung) gemäß dem Format angezeigt, das von der Zeitzonen- und Gebietsschemaeinstellung des aktuellen Benutzers angegeben wird.<br />-   Für die Web-API wird das Attribut als DateTimeOffset verfügbar gemacht.<br />-   Dieses Verhalten sollte für Attribute verwendet werden, die Informationen wie z.B. die Uhrzeiten vom Ein- und Auschecken in Hotels speichern.|  
  
 Der folgende Beispielcode zeigt, wie ein `UserLocal`-Verhalten für ein neues Datums- und Uhrzeitattribut festgelegt wird:  
  
 ```csharp
// Create a date time attribute for the Account entity
// with the UserLocal behavior
dtAttribute = new DateTimeAttributeMetadata
{                             
    SchemaName = "new_SampleDateTimeAttribute",
    DisplayName = new Label("Sample Date Time Attribute", _languageCode),
    RequiredLevel = new AttributeRequiredLevelManagedProperty(AttributeRequiredLevel.None),                
    Description = new Label("Created by SDK Sample", _languageCode),                
    DateTimeBehavior = DateTimeBehavior.UserLocal,
    Format = DateTimeFormat.DateAndTime,
    ImeMode = ImeMode.Disabled
};

CreateAttributeRequest createAttributeRequest = new CreateAttributeRequest
{
    EntityName = Account.EntityLogicalName,
    Attribute = dtAttribute
};
_serviceProxy.Execute(createAttributeRequest);
Console.WriteLine("Created attribute '{0}' with UserLocal behavior\nfor the Account entity.\n", 
                            dtAttribute.SchemaName);
```
  
 Im Beispielcode können Sie den Wert für die Eigenschaft `DateTimeBehavior` festlegen, indem Sie den direkten Zeichenfolgenwert angeben: `DateTimeBehavior = "UserLocal"`  
  
 Wenn Sie beim Erstellen eines Datums- und Zeitattributs kein Verhalten angeben, wird das Attribut standardmäßig mit dem Verhalten `UserLocal` erstellt. Das vollständige Beispielcode finden Sie unter [Beispiel: Konvertieren der Datums- und Zeitwerte](/dynamics365/customer-engagement/developer/org-service/sample-convert-date-time-behavior).  
  
> [!IMPORTANT]
>  -   Sobald Sie ein Datums- und Uhrzeitattribut mit dem festgelegten Verhalten `DateOnly` oder `TimeZoneIndependent` erstellt haben, können Sie das Verhalten des Attributs nicht mehr ändern. Weitere Informationen: [Ändern Sie das Verhalten eines DateTime-Attributs](behavior-format-date-time-attribute.md#ChangeBehavior)  
> -   Die Datums- und Uhrzeitattribute mit dem Verhalten `DateOnly` oder `TimeZoneIndependent` werden behandelt, als ob sie das Verhalten `UserLocal` hätten, wenn sie in einer früheren Version des Dynamics 365 for Outlook-Clients im Offlinemodus bearbeitet werden. Dies liegt daran, dass der Client die neuen Verhalten nicht versteht und sie nicht anders behandelt als `UserLocal`. Beim Upgrade werden keine Datums- und Uhrzeitattribute in die neuen Verhaltensweisen konvertiert. Die empfohlene Vorgehensweise ist, ein Upgrade aller Common Data Service-Clients auf die neueste Version durchzuführen, bevor ein Kunde eine der neuen Verhaltensweisen übernimmt. Im Onlinemodus funktioniert das Bearbeiten von Daten für Felder mit den neuen Verhaltensweisen problemlos.  
  
<a name="SpecifyFormat"></a>   

## <a name="specify-format-of-the-date-and-time-attribute"></a>Angeben des Formats eines Datums- und Uhrzeitattributs  

 Verwenden Sie die `Format`-Eigenschaft, um das Anzeigeformat für Datum und Uhrzeit eines Attributs unabhängig davon anzugeben, wie es im System gespeichert ist. Sie können die Enumeration `DateTimeFormat` (Enumeration <xref href="Microsoft.Dynamics.CRM.DateTimeFormat?text=DateTimeFormat EnumType" /> oder <xref:Microsoft.Xrm.Sdk.Metadata.DateTimeFormat>) verwenden, um das Anzeigeformat anzugeben: `DateAndTime` oder `DateOnly`.  
  
 Wenn die Eigenschaft `DateTimeAttributeMetadata.DateTimeBehavior` auf `DateOnly` gesetzt ist, können Sie den Wert der Eigenschaft `DateTimeAttributeMetadata.Format` nicht auf `DateAndTime` setzten oder ändern.  
  
<a name="UnsupportedQueryOperators"></a>   

## <a name="date-and-time-query-operators-not-supported-for-dateonly-behavior"></a>Datums- und Uhrzeitabfrageoperatoren für DateOnly-Verhalten werden nicht unterstützt  

 Zeitbezogene Abfrageoperatoren werden für das `DateOnly`-Verhalten nicht unterstützt. Im Gegensatz zu den zeitspezifischen Abfrageoperatoren, die hier aufgeführt werden, alle anderen Abfrageoperatoren unterstützt.  
  
-   Älter als X Minuten  
  
-   Älter als X Stunden  
  
-   Letzte X Stunden  
  
-   Nächste X Stunden  
  
 Mehr Informationen: [Datums- und Zeitabfrageoperatoren in FetchXML](/dynamics365/customer-engagement/developer/org-service/fiscal-date-older-datetime-query-operators-fetchxml)  
  
<a name="ChangeBehavior"></a>
   
## <a name="change-the-behavior-of-a-date-and-time-attribute"></a>Ändern des Verhaltens eines Datums- und Uhrzeitattributs  

 Sie können ein Datums- und Uhrzeitattribut aktualisieren, um sein Verhalten zu ändern, wenn Sie in Ihrer Common Data Service-Instanz die Systemanpasser-Rolle haben und die verwaltete Eigenschaft `DateTimeAttributeMetadata.CanChangeDateTimeBehavior` für das Datums- und Uhrzeitattribut auf `True` gesetzt ist.  
  
> [!CAUTION]
>  Bevor Sie das Verhalten eines Datums- und Zeitattribut ändern, sollten Sie alle Abhängigkeiten des Attributs wie Geschäftsregelwn, Wrkflows und berechnete oder Rollupattribute überprüfen, um sicherzustellen, dass als Ergebnis der Änderung des Verhaltens keine Probleme auftreten. Systemanpasser können Änderungen des Verhaltens der vorhandenen Datums- und Uhrzeitattribute mithilfe der verwalteten Eigenschaft `DateTimeAttributeMetadata.CanChangeDateTimeBehavior` einschränken.  
>   
>  Zumindest sollten Sie nach der Änderung des Verhaltens eines Datums- und Uhrzeitattributs alle Datensätze von Geschäftsregeln, Workflows, berechneten Attributen und Rollupattributen öffnen, die von dem geänderten Datums- und Uhrzeitattribut abhängig sind, die Informationen überprüfen und die Datensätze speichern, um sicherzustellen, dass das aktuelle Verhalten und der aktuelle Wert des Attributs verwendet werden.  
>   
>  Nachdem Sie das Datums- und Uhrzeitverhalten eines berechneten oder Rollupattributs geändert haben, öffnen Sie den Editor für die Definition von berechneten oder Rollupfeldern und speichern Sie die Felddefinition, um sicherzustellen, dass das Attribut nach der Verhaltensänderung noch gültig ist. Systemanpasser können den Felddefinitionseditor für berechnete oder Rollupattribute öffnen, indem Sie in Common Data Service neben **Feldtyp** auf **Bearbeiten** klicken. Weitere Informationen: [Definieren von berechneten Feldern](/dynamics365/customer-engagement/customize/define-calculated-fields) und [Definieren der Rollupfelder](/dynamics365/customer-engagement/developer/customize/define-rollup-fields)  
  
-   Das Verhalten der Attribute `CreatedOn` und `ModifiedOn` für die vordefinierten und benutzerdefinierten Entitäten wird standardmäßig auf `UserLocal` gesetzt und die verwaltete Eigenschaft `DateTimeAttributeMetadata.CanChangeDateTimeBehavior` wird auf `False` gesetzt, was impliziert, dass Sie das Verhalten dieser Attribute nicht ändern können. Obwohl Benutzer den Wert der verwalteten Eigenschaft `DateTimeAttributeMetadata.CanChangeDateTimeBehavior` dieser Attribute für benutzerdefinierte Entitäten ändern können, können Sie das Verhalten der Attribute noch nicht ändern.  
  
-   Für neue benutzerdefinierte Datums- und Uhrzeitattribute wird die verwaltete Eigenschaft `DateTimeAttributeMetadata.CanChangeDateTimeBehavior` auf `True` gesetzt. Dies bedeutet, dass Sie das Verhalten eines benutzerdefinierten Datums- und Uhrzeitattribut von `UserLocal` in `DateOnly` oder `TimeZoneIndependent` ändern können. Es sind keine anderen Verhaltensübergänge zulässig.  
  
     Für benutzerdefinierte Datums- und Zeitattribute, die Teil einer Common Data Service-Organisation sind, wird die verwaltete Eigenschaft `DateTimeAttributeMetadata.CanChangeDateTimeBehavior` auf `True` gesetzt, es sei denn, das Attribut oder die übergeordnete Entität ist nicht anpassbar.  
  
    > [!NOTE]
    >  Wenn Sie die Eigenschaft `DateTimeAttributeMetadata.DateTimeBehavior` eines Attributs von `UserLocal` in `DateOnly` ändern, sollten Sie sicherstellen, dass Sie auch die Eigenschaft `DateTimeAttributeMetadata.Format` von `DateAndTime` in `DateOnly` ändern. Andernfalls tritt eine Ausnahme auf.  
  
-   Die folgenden vordefinierten Datums- und Uhrzeitattribute in Common Data Service sind standardmäßig auf `DateOnly` gesetzt und die verwaltete Eigenschaft `DateTimeAttributeMetadata.CanChangeDateTimeBehavior` dieser Attribute wird auf `False` gesetzt. Das bedeutet, dass Sie das Verhalten für diese Attribute nicht ändern können:  
  
    |Datums- und Uhrzeitattribut|Übergeordnete Entität|  
    |-----------------------------|-------------------|  
    |anniversary|Kontakt|  
    |birthdate|Kontakt|  
    |duedate|Rechnung|  
    |estimatedclosedate|Lead|  
    |actualclosedate|Verkaufschance|  
    |estimatedclosedate|Verkaufschance|  
    |finaldecisiondate|Verkaufschance|  
    |validfromdate|Produkt|  
    |validtodate|Produkt|  
    |closedon|Angebot|  
    |expireson|Angebot|  
  
     Das Verhalten dieser Attribute ist auf `UserLocal` und die verwaltete Eigenschaft `DateTimeAttributeMetadata.CanChangeDateTimeBehavior` auf `True` eingestellt, und Sie können das Verhalten dieser Attribute nur auf `DateOnly` ändern. Keine anderen Verhaltensübergänge sind erlaubt.  
  
 Nachdem Sie das Verhalten eines Attributes aktualisiert haben, müssen Sie die Anpassungen veröffentlichen, damit die Änderungen wirksam ist. Durch Aktualisieren des Verhaltens eines Datums- und Uhrzeitattributs wird sichergestellt, dass sämtliche Werte, die eingegeben/aktualisiert wurden, *nachdem* das Attributverhalten geändert wurde, im System gemäß dem neuen Verhalten gespeichert werden. Dies wirkt sich nicht auf die Werte aus, die bereits in der Datenbank gespeichert sind, und sie werden weiterhin als UTC-Werte gespeichert. Falls Sie jedoch die vorhandenen Werte mithilfe des SDK (Software Development Kit) abrufen oder in der Benutzeroberfläche anzeigen, werden die vorhandenen Werte gemäß dem neuen Verhalten des Attributs angezeigt. Beispiel: Wenn Sie das Verhalten eines benutzerdefinierten Attributs für eine Firmenentität von `UserLocal` in `DateOnly` geändert haben und einen vorhandenen Firmendatensatz mithilfe des SDK abrufen, werden Datum und Uhrzeit als \<Datum> gefolgt von der Uhrzeit als 00:00 Uhr (00:00:00) angezeigt. Entsprechend wird bei der Verhaltensänderung von `UserLocal` in `TimeZoneIndependent` der tatsächliche Wert in der Datenbank im Istzustand ohne Zeitzonenkonvertierungen angezeigt.  
  
 Der folgende Beispielcode zeigt, wie ein das Verhalten für ein Datums- und Uhrzeitattribut aktualisiert wird:  
  
```csharp
// Retrieve the attribute to update its behavior and format
RetrieveAttributeRequest attributeRequest = new RetrieveAttributeRequest
{
    EntityLogicalName = Account.EntityLogicalName,
    LogicalName = "new_sampledatetimeattribute",
    RetrieveAsIfPublished = false
};
// Execute the request
RetrieveAttributeResponse attributeResponse =
                (RetrieveAttributeResponse)_serviceProxy.Execute(attributeRequest);

Console.WriteLine("Retrieved the attribute '{0}'.",
                attributeResponse.AttributeMetadata.SchemaName);

// Modify the values of the retrieved attribute
DateTimeAttributeMetadata retrievedAttributeMetadata =
                (DateTimeAttributeMetadata)attributeResponse.AttributeMetadata;
retrievedAttributeMetadata.DateTimeBehavior = DateTimeBehavior.DateOnly;
retrievedAttributeMetadata.Format = DateTimeFormat.DateOnly;

// Update the attribute with the modified value
UpdateAttributeRequest updateRequest = new UpdateAttributeRequest
{
    Attribute = retrievedAttributeMetadata,
    EntityName = Account.EntityLogicalName,
    MergeLabels = false
};
_serviceProxy.Execute(updateRequest);
Console.WriteLine("Updated the behavior and format of '{0}' to DateOnly.",
    retrievedAttributeMetadata.SchemaName);

// Publish customizations to the account entity
PublishXmlRequest pxReq = new PublishXmlRequest
{
    ParameterXml = String.Format("<importexportxml><entities><entity>account</entity></entities></importexportxml>")
};
_serviceProxy.Execute(pxReq);
Console.WriteLine("Published customizations to the Account entity.\n");
 
``` 
  
 Das vollständige Beispielcode finden Sie unter [Beispiel: Konvertieren der Datums- und Zeitwerte](/dynamics365/customer-engagement/developer/org-service/sample-convert-date-time-behavior).  
  
<a name="Convert"></a>   
## <a name="convert-behavior-of-existing-date-and-time-values-in-the-database"></a>Konvertieren des Verhaltens von Datums- und Uhrzeitwerten in der Datenbank 

 Wenn Sie ein Datums- und Uhrzeitattribut so aktualisieren, dass sein Verhalten von `UserLocal` in `DateOnly` oder `TimeZoneIndependent` geändert wird, werden die vorhandenen Attributwerte in der Datenbank nicht automatisch konvertiert. Die Verhaltensänderung beeinflusst lediglich die Werte, die in dem Attribut eingegeben oder aktualisiert wurden, *nachdem* das Verhalten geändert wurde. Die vorhandenen Datums- und Uhrzeitwerte im System liegen weiterhin als UTC vor und werden von Common Data Service gemäß dem neuen Verhalten angezeigt, wenn sie durch das SDK oder in der Benutzeroberfläche abgerufen werden (siehe vorheriger Abschnitt). Für Attribute, dessen Verhalten von `UserLocal` in `DateOnly` geändert wurde, können Sie die vorhandenen UTC-Wert in der Datenbank mithilfe der `ConvertDateAndTimeBehavior`-Nachricht in den entsprechenden `DateOnly`-Wert konvertieren, um Datenanomalien zu vermeiden.  
  
 Die Nachricht ermöglicht Ihnen die Angabe einer Konvertierungsregel (Wenn Sie mit dem Organisationsservice arbeiten, sehen Sie <xref:Microsoft.Xrm.Sdk.Messages.ConvertDateAndTimeBehaviorRequest.ConversionRule>), um die Zeitzone auszuwählen, die für die Konvertierung der Werte aus UTC in DateOnly verwendet wird. Sie können einen der folgenden Konvertierungsregeln angeben:  
  
-   `SpecificTimeZone`: Konvertiert einen UTC-Wert gemäß dem angegebenen Common Data Service-Zeitzonencode in einen DateOnly-Wert. In diesem Fall müssen Sie auch einen Wert für den Parameter <xref:Microsoft.Xrm.Sdk.Messages.ConvertDateAndTimeBehaviorRequest.TimeZoneCode> angeben.  
  
-   `CreatedByTimeZone`: Konvertiert einen UTC-Wert in einen DateOnly-Wert, der dem Benutzer, der den Datensatz erstellt hat, in der Benutzeroberfläche angezeigt wird.  
  
-   `OwnerTimeZone`: Konvertiert einen UTC-Wert in einen DateOnly-Wert, der dem Benutzer, der den Datensatz besitzt, in der Benutzeroberfläche angezeigt wird.  
  
-   `LastUpdatedByTimeZone`: Konvertiert einen UTC-Wert in einen DateOnly-Wert, der dem Benutzer, der den Datensatz zuletzt aktualisiert hat, in der Benutzeroberfläche angezeigt wird.  
  
 Sie können eines der Mitglieder der folgenden vier unterstützten <xref:Microsoft.Xrm.Sdk.DateTimeBehaviorConversionRule>-Klassen verwenden, um einen gültigen Wert für den Parameter <xref:Microsoft.Xrm.Sdk.Messages.ConvertDateAndTimeBehaviorRequest.ConversionRule> anzugeben.  
  
> [!NOTE]
>  Sie müssen in Ihrer Common Data Service-Instanz über die Systemadministratorrolle verfügen, um die <xref:Microsoft.Xrm.Sdk.Messages.ConvertDateAndTimeBehaviorRequest>-Nachricht auszuführen.  
  
 Wenn Sie die `ConvertDateAndTimeBehavior` (Wenn Sie mit dem Organisationsservice arbeiten, lesen Sie <xref:Microsoft.Xrm.Sdk.Messages.ConvertDateAndTimeBehaviorRequest>-Nachricht) Nachricht ausführen, wird ein Systemauftrag (asynchroner Vorgang) erstellt, um die Konvertierugnsanforderung auszuführen. Das `ConvertDateAndTimeBehaviorResponse.JobId`-Attribut in der Nachrichtenantwort zeigt die ID des Systemauftrags an, der infolge der Konvertierugnsanforderung erstellt wird. Nachdem der Systemauftrag abgeschlossen wurde, müssen Sie die Auftragsdetails (`AsyncOperation.Message`) überprüfen, um Konvertierungsdetails oder Fehler anzuzeigen.  
  
> [!NOTE]
>  Es wird empfohlen, dass Sie Konvertierungen von mehreren Attributen in einem einzelnen Konvertierungsauftrag zusammenfassen und jeweils einen einzelnen Konvertierungsauftrag ausführen, um sicherzustellen, dass keine Konflikte beim Konvertieren auftreten, und um eine optimale Systemleistung zu gewährleisten.  
  
 Folgende wichtige Punkte sollten bei der Verwendung der `ConvertDateAndTimeBehavior`-Nachricht berücksichtigt werden:  
  
-   Sie sollten alle großen Änderungen an Lösungen in Common Data Service während der Ausführung der Nachricht, z.B. Importieren oder Löschen einer Lösung oder Löschen eines Attributes oder einer übergeordneten Entität, vermeiden. Derartige Änderungen führen möglicherweise zu unerwartetem Verhalten; Datenverluste treten jedoch nicht auf.  
  
-   Die Updates, die im System als Ergebnis der Ausführung der Nachricht vorgenommen wurden, führen keine Workflows und Plug-Ins aus.  
  
-   Updates, die im System infolge der Nachrichtenausführung vorgenommen wurden, ändern den Wert „Zuletzt geändert am“ des Attributs nicht, werden jedoch überwacht, damit Administratoren den Zeitpunkt der Konvertierung und die ursprünglichen bzw. geänderten Werte für ein Attribut ermitteln können.  
  
 Im folgenden Beispielcode wird gezeigt, wie die Meldung verwendet wird:  
  
```csharp
ConvertDateAndTimeBehaviorRequest request = new ConvertDateAndTimeBehaviorRequest()
{
    Attributes = new EntityAttributeCollection() 
            { 
                new KeyValuePair<string, StringCollection>("account", new StringCollection() 
                { "new_sampledatetimeattribute" }) 
            },
    ConversionRule = DateTimeBehaviorConversionRule.SpecificTimeZone.Value,
    TimeZoneCode = 190, // Time zone code for India Standard Time (IST) in CRM
    AutoConvert = false // Conversion must be done using ConversionRule
};

// Execute the request
ConvertDateAndTimeBehaviorResponse response = (ConvertDateAndTimeBehaviorResponse)_serviceProxy.Execute(request);

```
  
 Das vollständige Beispielcode finden Sie unter [Beispiel: Konvertieren der Datums- und Zeitwerte](/dynamics365/customer-engagement/developer/org-service/sample-convert-date-time-behavior).  
  
### <a name="see-also"></a>Siehe auch  
 [Beispiel: Konvertierung der Datums- und Uhrzeitwerte](/dynamics365/customer-engagement/developer/org-service/sample-convert-date-time-behavior.md)   
 [Verhalten und Format des Datums- und Uhrzeitfelds](/dynamics365/customer-engagement/developer/customize/behavior-format-date-time-field)   
 [Anpassen von Entitätsattributmetadaten](/dynamics365/customer-engagement/developer/customize-entity-attribute-metadata)          
 <xref:Microsoft.Xrm.Sdk.Messages.ConvertDateAndTimeBehaviorRequest>      
 <xref:Microsoft.Xrm.Sdk.Metadata.DateTimeAttributeMetadata> 