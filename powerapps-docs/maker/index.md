---
title: Übersicht über das Erstellen von Apps | Microsoft-Dokumentation
description: Übersicht über das Erstellen von Apps im Canvas-Modus oder im modellgesteuerten Modus sowie über die Integration von Common Data Service
author: tapanm-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.date: 07/18/2018
ms.author: tapanm
ms.reviewer: ''
ms.openlocfilehash: a0430ab6b3baebf1a4144c52c63526745cd13928
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/07/2019
ms.locfileid: "71987799"
---
# <a name="overview-of-creating-apps-in-powerapps"></a>Übersicht über das Erstellen von Apps in PowerApps

PowerApps ist eine hochproduktive Entwicklungsplattform für Geschäfts-Apps und umfasst vier Hauptkomponenten:

- Bei [Canvas-Apps](canvas-apps/getting-started.md) beginnen Sie mit der Benutzeroberfläche, erstellen eine stark angepasste, leistungsfähige Schnittstelle und verbinden diesen mit Ihrer Auswahl aus 200 Datenquellen. Sie können Canvas-Apps für mobile Anwendungen sowie für Web- und Tabletanwendungen erstellen.
- Bei [modellgesteuerten Apps](model-driven-apps/model-driven-app-overview.md) beginnen Sie mit Ihrem Datenmodell. Die Erstellung beginnt bei der Form Ihrer wichtigsten Geschäftsdaten und -prozesse in Common Data Service. Auf dieser Grundlage werden Formulare, Ansichten und andere Komponenten modelliert. Modellgesteuerte Apps generieren automatisch eine leistungsstarke UI, die geräteübergreifend reagiert.
- In [Portals](portals/overview.md) beginnen Sie mit der Erstellung externer Websites, bei denen sich Benutzer außerhalb Ihrer Organisation mit einer Vielzahl von Identitäten anmelden, Daten in Common Data Service erstellen und anzeigen oder sogar Inhalte anonym durchsuchen können.
- Bei [Common Data Service](common-data-service/data-platform-intro.md) handelt es sich um die in PowerApps enthaltene Datenplattform, die Ihnen das Speichern und Modellieren von Geschäftsdaten ermöglicht. Auf dieser Plattform werden Dynamics 365-Anwendungen erstellt. Wenn Sie ein Kunde von Dynamics sind, befinden Ihre Daten sich bereits in Common Data Service.

Sie können Ihre erste App schnell und einfach erstellen. Es gibt einen 30-tägigen Testplan und einen kostenlosen Communityplan. Finden Sie heraus, welcher Plan am besten zu Ihnen passt, und legen Sie los.

## <a name="canvas-apps"></a>Canvas-Apps

Canvas-Apps bieten Ihnen die Flexibilität, die Benutzeroberfläche und Servicequalität nach Ihren Vorstellungen zu gestalten. Lassen Sie sich bei der Optik und dem Verhalten Ihrer Apps von Ihrer Kreativität und Ihrem Geschäftssinn leiten.

Sie können Ihre App mithilfe der Microsoft-Tools erstellen, in denen sich Ihre Daten befinden, z.B.:

- [Anhand einer SharePoint-Liste](canvas-apps/app-from-sharepoint.md#generate-an-app-from-within-sharepoint-online)
- [Anhand eines Power BI-Dashboards](canvas-apps/embed-powerapps-powerbi.md)

Das Erstellen einer Canvas-App ist einfach. Mit PowerApps können Sie Ihre App auf verschiedene Arten suchen oder erstellen:

- [Anhand von Daten](canvas-apps/app-from-sharepoint.md)
- [Anhand eines Beispiels](canvas-apps/open-and-run-a-sample-app.md)
- [Anhand einer Common Data Service-Quelle](canvas-apps/data-platform-create-app.md)
- [Anhand einer leeren Canvas](canvas-apps/data-platform-create-app-scratch.md)
- [Über AppSource](../user/app-source.md)

## <a name="model-driven-apps"></a>Modellgesteuerte Apps

Wenn Sie eine modellgesteuerte App erstellen, können Sie die gesamte Leistungsfähigkeit von Common Data Service verwenden, um Ihre Formulare, Geschäftsregeln und Prozessabläufe schnell zu konfigurieren. Eine modellgesteuerte App wird über die PowerApps-Website erstellt.

Die ersten Schritte mit modellgesteuerten Apps sind einfach. Sie können mit folgenden Themen beginnen:

- [Erstellen einer App](https://docs.microsoft.com/dynamics365/customer-engagement/customize/create-edit-app)
- [Erstellen und Entwerfen von Formularen](https://docs.microsoft.com/dynamics365/customer-engagement/customize/create-design-forms)
- [Erstellen oder Bearbeiten von Ansichten](https://docs.microsoft.com/dynamics365/customer-engagement/customize/create-edit-views)
- [Erstellen oder Bearbeiten eines Systemdiagramms](https://docs.microsoft.com/dynamics365/customer-engagement/customize/create-edit-system-chart)
- [Erstellen oder Bearbeiten von Dashboards](https://docs.microsoft.com/dynamics365/customer-engagement/customize/create-edit-dashboards)
- [Hinzufügen von Sicherheit](https://docs.microsoft.com/dynamics365/customer-engagement/customize/manage-access-apps-security-roles)
- [Hinzufügen von Geschäftslogik](https://docs.microsoft.com/dynamics365/customer-engagement/customize/guide-staff-through-common-tasks-processes)

## <a name="common-data-service"></a>Common Data Service

Mit Common Data Service können Sie Daten sicher innerhalb von Standardentitäten und benutzerdefinierten Entitäten speichern und verwalten. Sie können nach Bedarf ebenfalls Felder zu diesen Entitäten hinzufügen.

Die ersten Schritte mit Common Data Service sind einfach. Sie können beispielsweise mit folgenden Elementen beginnen:

- [Erstellen einer benutzerdefinierten Entität](common-data-service/data-platform-create-entity.md)
- [Verwalten von Feldern](common-data-service/data-platform-manage-fields.md)
- [Erstellen von benutzerdefinierten Optionen](common-data-service/custom-picklists.md)
- [Create a business rule (Erstellen einer Geschäftsregel)](https://docs.microsoft.com/dynamics365/customer-engagement/customize/create-business-rules-recommendations-apply-logic-form)

## <a name="canvas-and-model-driven-artifacts"></a>Canvas-Apps und modellgesteuerte Artefakte

Während wir die Funktionen von Canvas-Apps und modellgesteuerten Apps zusammenführen, sind diese Artefakte entweder für Canvas-Apps oder modellgesteuerte Apps relevant.

| Artefakt            | App-Typ     |
|---------------------|--------------|
| Entität > Ansichten      | Modellgesteuert |
| Entität > Formulare      | Modellgesteuert |
| Entität > Dashboards | Modellgesteuert |
| Verbindungen         | Zeichenbereich       |
| Gateways            | Zeichenbereich       |
| Benutzerdefinierte Connectors   | Zeichenbereich       |
| Apps > Importieren       | Zeichenbereich       |

Nachdem Sie Ihre App erstellt haben, können Sie diese für Ihre Teammitglieder [freigeben](canvas-apps/share-app.md).
