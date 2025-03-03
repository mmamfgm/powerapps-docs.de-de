---
title: Starten eines Flows in einer Canvas-App | Microsoft-Dokumentation
description: Erstellen Sie einen Flow, der mindestens eine Aufgabe ausführt, wenn ein Ereignis in einer Canvas-App auftritt, z.B. wenn ein Benutzer eine Schaltfläche auswählt.
author: stepsic-microsoft-com
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 12/07/2018
ms.author: stepsic
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 636e9f853ada9816e87232348e5ce7ef6df2cedc
ms.sourcegitcommit: 0f0b26122be28d674af0833247b491e9367c4932
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2019
ms.locfileid: "73898325"
---
# <a name="start-a-flow-in-a-canvas-app"></a>Starten eines Flows in einer Canvas-App

Sie können die Energie Automatisierung verwenden, um Logik zu erstellen, die eine oder mehrere Aufgaben ausführt, wenn ein Ereignis in einer Canvas-App auftritt. Sie können zum Beispiel eine Schaltfläche so konfigurieren, dass bei Auswahl durch den Benutzer ein Element in einer SharePoint-Liste erstellt wird, eine E-Mail oder eine Besprechungsanfrage gesendet wird, eine Datei der Cloud hinzugefügt wird oder all dies ausgeführt wird. Sie können jedes Steuerelement in der App für das Starten des Flows konfigurieren, der auch weiterhin ausgeführt wird, wenn Sie PowerApps schließen.

> [!NOTE]
> Wenn ein Benutzer einen Flow aus einer APP heraus ausführt, muss dieser Benutzer über die Berechtigung zum Ausführen der im Flow angegebenen Tasks verfügen. Andernfalls schlägt der Flow fehl.

## <a name="prerequisites"></a>Voraussetzungen

- [Registrieren Sie sich](../signup-for-powerapps.md) bei PowerApps.
- Machen Sie sich damit vertraut, wie Sie [ein Steuerelement konfigurieren](add-configure-controls.md).

## <a name="create-a-flow"></a>Erstellen eines Flows

1. Melden Sie sich bei [PowerApps](https://make.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) an.

1. Wählen Sie in der linken Navigationsleiste **Geschäftslogik**aus, und wählen Sie dann **Flows**aus.

1. Wählen Sie in der linken oberen Ecke der Seite " **meine Flows** " die Option **neu**aus, und wählen Sie dann ohne Vorlage **erstellen aus**.

    ![Option, um einen Flow ohne Vorlage zu erstellen](./media/using-logic-flows/create-from-blank.png)

1. Wählen Sie am unteren Rand der Seite, die angezeigt wird, die Option **Hunderte von Verbindungen und Triggern durchsuchen**aus.

1. Geben Sie im Suchfeld **powerapps**ein, und wählen Sie dann das **powerapps** -Symbol aus.

    ![Erstellen eines powerapps-Auslösers](./media/using-logic-flows/set-trigger.png)
    
1. Wählen Sie auf der nächsten Seite das powerapps-Symbol erneut aus, und wählen Sie dann **neuer Schritt**aus.

1. Geben Sie im Feld mit den **Connectors und Aktionen suchen**eine Aktion für den Flow an, wie in diesem Beispiel:

   1. Geben Sie in das Feld **SharePoint** ein, und wählen Sie dann in der Liste unter **Aktionen**die Option **Element erstellen** aus.

       ![Option zum Erstellen eines SharePoint-Elements](./media/using-logic-flows/create-sharepoint-item.png)

   1. Geben Sie, wenn Sie dazu aufgefordert werden, die Anmeldeinformationen für die Verbindung mit SharePoint an.

   1. Geben oder fügen Sie in das Feld **Websiteadresse** die URL einer SharePoint Online-Website ein, die eine Liste enthält.

       > [!NOTE]
       > Fügen Sie den Namen der Liste nicht an die URL an.

   1. Geben Sie im Feld **Listen Name** die Liste an, die Sie verwenden möchten.
   
       ![Liste angeben](./media/using-logic-flows/list-fields.png)

   1. Wählen Sie das Eingabefeld für ein Feld in der Liste (z. b. **Titel**) aus, wählen Sie im Bereich dynamischer Inhalt die Option **Weitere** anzeigen aus, und wählen Sie dann **in powerapps Fragen**aus. 

       ![Hinzufügen von „In PowerApps fragen“ zum Feld „Titel“](./media/using-logic-flows/ask-in-powerapps.png)

1. optionale Geben Sie einen oder mehrere zusätzliche Schritte an, z. b. das Senden einer Genehmigungs-e-Mail an eine von Ihnen angegebene Adresse oder die Erstellung eines verknüpften Eintrags in einer anderen

1. Geben oder fügen Sie in der Nähe der oberen linken Ecke einen Namen für den Flow ein, und klicken Sie dann in der Nähe der oberen rechten Ecke auf **Speichern** .

## <a name="add-a-flow-to-an-app"></a>Hinzufügen eines Flows zu einer App
1. Klicken Sie in der linken Navigationsleiste auf **Erstellen**.

1. Zeigen Sie auf die **Canvas-APP von einer leeren** Kachel, und wählen Sie dann **diese APP erstellen**aus.

1. Fügen Sie ein **[Texteingabe](controls/control-text-input.md)** -Steuerelement hinzu, und nennen Sie es **RecordTitle**.

1. Fügen Sie ein **[Schaltflächen](controls/control-button.md)** -Steuerelement hinzu, und verschieben Sie es unter **RecordTitle**.

1. Wählen Sie bei ausgewähltem **[Schaltflächen](controls/control-button.md)** -Steuerelement **Flows** auf der Registerkarte **Aktion** aus.

    ![Option „Flows“ auf der Registerkarte „Aktion“](./media/using-logic-flows/action-tab.png)

1. Wählen Sie im Bereich, der angezeigt wird, den Flow aus, den Sie im vorherigen Verfahren erstellt haben.

    > [!NOTE]
   > Wenn der von Ihnen erstellte Flow nicht verfügbar ist, vergewissern Sie sich, dass PowerApps auf die Umgebung festgelegt ist, in der Sie den Flow erstellt haben.

    ![Hinzufügen eines Flows aus dem Bereich „Anpassung“](./media/using-logic-flows/add-flow-from-pane.png)

1. Geben oder fügen Sie in der Bearbeitungsleiste **RecordTitle.Text)** am Ende der Formel ein, die automatisch hinzugefügt wurde.

    ![OnSelect-Eigenschaft, die den Flow enthält](./media/using-logic-flows/onselect-with-flow.png)

## <a name="test-the-flow"></a>Testen des Flows
1. Doppelklicken Sie auf das **Text Eingabe** -Steuerelement, und geben Sie Text ein, oder fügen Sie ihn ein.

1. Wenn Sie die Alt-Taste gedrückt halten, wählen Sie das **[Schalt](controls/control-button.md)** Flächen-Steuerelement.

    Ein SharePoint-Element wird in der Liste erstellt, die Sie mit dem Text angegeben haben, den Sie als Titel angegeben haben. Wenn die Liste bei Ausführung des Flows geöffnet war, müssen Sie ggf. Ihr Browserfenster aktualisieren, um die Änderungen anzuzeigen.
