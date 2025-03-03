---
title: Öffnen des modellgetriebenen App-Formulareditors unter PowerApps | MicrosoftDocs
ms.custom: ''
ms.date: 06/27/2018
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
- powerapps
author: Mattp123
ms.assetid: 8478a07a-c697-4784-874b-36958eb4f95d
caps.latest.revision: 63
ms.author: matp
manager: kvivek
search.audienceType:
- maker
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: f922908611d56afc99c5ebc844ff75c94d48657c
ms.sourcegitcommit: d9cecdd5a35279d78aa1b6c9fc642e36a4e4612c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "2759510"
---
# <a name="open-the-model-driven-app-form-editor"></a>Öffnen Sie den modellgesteuerten App-Formular-Editor 
Im Formular-Editor können Sie Formulare entwerfen, indem Sie Komponenten wie Abschnitte, Registerkarten, Felder und Steuerelemente auf die Formular-Editor-Canvas ziehen. In diesem Thema erfahren Sie, wie Sie auf verschiedene Arten auf den Formular-Editor zugreifen.
 
Wenn Sie neue Lösungskomponenten bei der Bearbeitung des Formulars erstellen, etwa Webressourcen, verwenden die Namen der Komponenten das Anpassungspräfix des Lösungsherausgebers für die Standardlösung, und diese Komponenten werden nur in der Standardlösung eingeschlossen. Wenn neue Lösungskomponenten in einer bestimmten nicht verwalteten Lösung eingeschlossen werden sollen, sollten Sie den Formulareditor über diese nicht verwaltete Lösung öffnen.  

## <a name="access-the-form-editor-from-the-powerapps-site"></a>Rufen Sie den Formular-Editor von der Seite PowerApps aus auf.

1. Melden Sie sich bei [PowerApps](https://make.powerapps.com/) an. 

2. Wählen Sie **Daten** > **Entitäten** >und wählen Sie dann die gewünschte Entität, z.B. die Firma-Entität. 

3. Wählen Sie die Registerkarte **Formulare** aus und öffnen Sie das gewünschte Formular, z. B. das Hauptformular **Firma**.

## <a name="access-the-form-editor-from-solution-explorer"></a>Greifen Sie vom Lösungs-Explorer auf den Formular-Editor zu.
  
1.  Öffnen Sie den [Lösungs-Explorer](advanced-navigation.md#solution-explorer).
  
2.  Erweitern Sie unter **Komponenten** **Entitätemn**, und dann die gewünschte Entität, und wählen Sie **Formulare** aus.  
  
3.  Klicken Sie in der Liste der Formulare auf das Formular, das Sie bearbeiten wollen.  
  

## <a name="access-the-form-editor-through-the-command-bar-within-a-model-driven-app"></a>Greifen Sie auf den Formular-Editor über die Befehlsleiste innerhalb einer modellgesteuerten Anwendung zu 
  
1.  Öffnen Sie einen Datensatz.  
  
2.  Falls mehrere Hauptformulare für die Entität vorhanden sind, überprüfen Sie, ob das Formular das ist, das Sie bearbeiten möchten. Wenn dies nicht der Fall ist, wählen Sie mit der Formularauswahl das Formular aus, das Sie bearbeiten möchten.  
  
3.  Wählen Sie die Schaltfläche **Weitere Befehle** aus ![„Weitere Befehle“-Schaltflächen in der Termin-Aktivität](media/more-commands.gif "Mehr Befehlsschaltflächen in der Termin-Aktivität").  
  
4.  Wählen Sie den **Formular-Editor** aus.  

## <a name="access-the-form-editor-from-within-app"></a>Zugriff auf den Formular-Editor aus der App heraus
  
 Sie können auf den Fomulareditor über die Befehlsleiste oder das Menüband zugreifen, abhängig von der Entität. Bei beiden Möglichkeiten öffnen Sie das Formular im Kontext der Standardlösung. 

## <a name="access-the-form-editor-for-an-unmanaged-solution"></a>Zugriff auf den Formulareditor für eine nicht verwaltete Lösung  
  
1.  Öffnen Sie die [Lösung](advanced-navigation.md#solutions).  
  
2.  Doppelklicken Sie auf die nicht verwaltete Lösung, die Sie verwenden möchten.  
  
3.  Suchen Sie die Entität mit dem Formular, das Sie bearbeiten möchten. Falls die Entität nicht vorhanden ist, müssen Sie sie hinzufügen möchten. Weitere Informationen: [Hinzufügen einer Entität zu einer nicht verwalteten Lösung](#add-an-entity-to-an-unmanaged-solution) 
  
### <a name="add-an-entity-to-an-unmanaged-solution"></a>Hinzufügen einer Entität zu einer nicht verwalteten Lösung  
  
1.  Wählen Sie den Knoten **Entitäten**, und wählen Sie in der Symbolleiste über der Liste die Option **Vorhandenes Element hinzufügen** aus.  
  
2.  Wählen Sie im Dialogfeld **Lösungskomponenten auswählen**, wenn die Auswahl **Komponententyp** auf **Entität** festgelegt ist, die Entität aus, die Sie hinzufügen möchten, und klicken Sie auf **OK**.  
  
3.  Wenn das Dialogfeld **Fehlende erforderliche Komponenten** angezeigt wird, können Sie auf **Nein, erforderliche Komponenten nicht einschließen** klicken, wenn Sie diese nicht verwaltete Lösung nicht in eine andere Umgebung importieren möchten. Wenn Sie wählen, die fehlenden erforderlichen Komponenten derzeit nicht einzuschließen, können Sie sie später hinzufügen. Sie erhalten erneut eine Benachrichtigung, wenn Sie diese Lösung später exportieren.  
  
5.  Erweitern Sie im Lösungsexplorer die Entität mit dem Formular, das Sie bearbeiten wollen, und wählen Sie **Formulare**.  
  
6.  Doppelklicken Sie in der Liste der Formulare auf das Formular, das Sie bearbeiten wollen.  

## <a name="next-steps"></a>Nächste Schritte

[Formulare erstellen und gestalten](create-design-forms.md)
