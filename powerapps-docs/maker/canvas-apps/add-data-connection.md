---
title: Hinzufügen einer Datenverbindung in einer Canvas-App | Microsoft-Dokumentation
description: Hinzufügen einer Datenverbindung in einer vorhandenen Canvas-App oder in einer leeren App
author: lancedMicrosoft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 04/06/2018
ms.author: lanced
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 420728d60555c3aeaf5fd5e844a900d412b0c3ef
ms.sourcegitcommit: d9cecdd5a35279d78aa1b6c9fc642e36a4e4612c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "73540961"
---
# <a name="add-a-data-connection-to-a-canvas-app-in-powerapps"></a>Hinzufügen einer Datenverbindung in einer Canvas-App in PowerApps

Fügen Sie in PowerApps einer vorhandenen Canvas-App oder einer von Grund auf neu erstellten App eine Datenverbindung hinzu. Ihre APP kann eine Verbindung mit SharePoint, Common Data Service, Salesforce, onedrive oder [vielen anderen Datenquellen](connections-list.md)herstellen.

Ihr [nächster Schritt](#next-steps) nach diesem Artikel besteht darin, Daten aus dieser Datenquelle in der App anzuzeigen und zu verwalten; siehe folgende Beispiele:

* Verbinden mit OneDrive und Verwalten von Daten in einer Excel-Arbeitsmappe in Ihrer App.
* Verbinden mit Twilio und senden einer SMS-Nachricht von Ihrer App.
* Stellen Sie eine Verbindung mit Common Data Service her, und aktualisieren Sie eine Entität von Ihrer APP.
* Herstellen einer Verbindung mit SQL Server und Aktualisieren einer Tabelle aus Ihrer App.

## <a name="prerequisites"></a>Voraussetzungen

[Registrieren Sie sich](../signup-for-powerapps.md) für PowerApps, und [melden Sie sich an](https://make.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc), indem Sie dieselben Anmeldeinformationen bereitstellen, die Sie bei der Registrierung angegeben haben.

## <a name="open-a-blank-app"></a>Öffnen einer leeren App

1. Wählen Sie auf der Registerkarte **Startseite** **Canvas-APP von leer aus**.

1. Geben Sie einen Namen für Ihre APP an, und wählen Sie dann **Erstellen**aus.

1. Falls das Dialogfeld **Willkommen bei PowerApps Studio** angezeigt wird, klicken Sie auf **Überspringen**.

## <a name="add-data-source"></a>Datenquelle hinzufügen

1. Wählen Sie im mittleren Bereich die Option **mit Daten verbinden** aus, um den Bereich **Daten** zu öffnen.

    Wenn dies eine vorhandene App wäre und der Bildschirm bereits ein Steuerelement enthielt, wählen Sie > **Datenquellen** **anzeigen** aus, um denselben Bereich zu öffnen.

1. Wählen Sie **Datenquelle hinzufügen**aus.

1. Wenn die Liste der Verbindungen die gewünschte Verbindung enthält, wählen Sie diese aus, um Sie der APP hinzuzufügen. Andernfalls fahren Sie mit dem nächsten Schritt fort.

    ![Vorhandene Verbindung auswählen](./media/add-data-connection/choose-existing-connection.png)

1. Wählen Sie **neue Verbindung** aus, um eine Liste der Verbindungen anzuzeigen.

    ![Hinzufügen einer Verbindung](./media/add-data-connection/add-connection.png)

1. Geben Sie in der Suchleiste die ersten Buchstaben der gewünschten Verbindung ein, oder fügen Sie Sie ein, und wählen Sie dann die Verbindung aus, wenn Sie angezeigt wird.

    ![Suchen nach einer Verbindung](./media/add-data-connection/search-connections.png)

1. Klicken Sie auf **Erstellen**, um die Verbindung zu erstellen und der App hinzuzufügen.

    Einige Connectors wie **Office 365 Outlook** erfordern keine weiteren Schritte, und Sie können sofort Daten daraus anzeigen. Andere Connectors fordern Sie auf, Anmeldeinformationen bereitzustellen, einen bestimmten Satz von Daten anzugeben oder weitere Schritte durchzuführen. In [SharePoint](connections/connection-sharepoint-online.md) und [SQL Server](connections/connection-azure-sqldatabase.md) sind z.B. zusätzliche Informationen erforderlich, bevor Sie sie verwenden können. Mit [Common Data Service](connections/connection-common-data-service.md)können Sie die Umgebung ändern, bevor Sie eine Entität auswählen.

## <a name="identify-or-change-a-data-source"></a>Identifizieren oder Ändern einer Datenquelle
Wenn Sie eine App aktualisieren, müssen Sie möglicherweise die im Katalog angezeigte Datenquelle, ein Formular oder ein anderes Steuerelement angeben oder ändern. Beispielsweise müssen Sie möglicherweise eine Datenquelle identifizieren, wenn Sie eine APP aktualisieren, die von einem anderen Benutzer erstellt oder vor längerer Zeit erstellt wurde.

1. Wählen Sie das Steuerelement aus, z. b. einen Katalog, für das Sie die Datenquelle identifizieren oder ändern möchten.

    Der Name der Datenquelle wird im rechten Bereich auf der Registerkarte **Eigenschaften** angezeigt.

    ![Identifizieren einer Verbindung](./media/add-data-connection/identify-connection.png)

1. Wenn Sie weitere Informationen zur Datenquelle anzeigen oder ändern möchten, klicken Sie auf den Pfeil nach unten neben dem Namen.

    Weitere Informationen zur aktuellen Datenquelle werden angezeigt, und Sie können eine weitere Quelle auswählen oder erstellen.

    ![Ändern einer Verbindung](./media/add-data-connection/change-connection.png)

## <a name="next-steps"></a>Nächste Schritte

* Um Daten in einer Quelle wie Excel, SharePoint, Common Data Service oder SQL Server anzuzeigen und zu aktualisieren, [fügen Sie einen Katalog hinzu](add-gallery.md), und [fügen Sie ein Formular hinzu](add-form.md).
* Verwenden Sie für die Daten in anderen Quellen Connector-spezifische Funktionen, z.B. für [Office 365 Outlook](connections/connection-office365-outlook.md), [Twitter](connections/connection-twitter.md) und [Microsoft Translator](connections/connection-microsoft-translator.md).
