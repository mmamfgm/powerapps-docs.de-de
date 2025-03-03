---
title: Arbeiten mit Metadaten mithilfe von Code (Common Data Service) | Microsoft-Dokumentation
description: Sowohl die [Web-API](org-service/overview.md) als auch der [Organisationsservice](webapi/overview.md) enthalten Funktionen für CRUD-Vorgänge auf dem Entitätsschema.
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: kvivek
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
ms.openlocfilehash: 853fc53221f82a25aeab271c5fca53b19d17eabe
ms.sourcegitcommit: 8185f87dddf05ee256491feab9873e9143535e02
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2019
ms.locfileid: "2748559"
---
# <a name="work-with-metadata-using-code"></a>Verwenden von Metadaten mit Code

Sowohl die [Web-API](org-service/overview.md) als auch der [Organisationsservice](webapi/overview.md) enthalten Funktionen für CRUD-Vorgänge auf dem Entitätsschema. Sie können diese Vorgänge mithilfe von Code ausführen. Im Allgemeinen verwenden Sie Designer, um benutzerdefinierte Schemaelemente hinzuzufügen, zu aktualisieren oder zu löschen. Benutzer müssen Administratorberechtigungen haben, um Schemaänderungen anzuwenden, aber alle Benutzer können Metadaten lesen.

## <a name="why-work-with-metadata"></a>Warum mit Metadaten arbeiten?

Ein allgemeinerer Einsatz für Metadatendienste ist das Abrufen von Metadaten zur Umgebung, in der die Erweiterung ausgeführt wird. Da jede Umgebung anders sein kann und Schemametadaten viele Informationen darüber enthalten, wie die Umgebung konfiguriert ist, müssen Sie diese Informationen abrufen, um zu ermöglichen, dass Ihre Erweiterungen sich an andere Anpassungen anpassen, die in dieser Umgebung wirksam sind.

Einige Beispiele:
- Die Gesamtanzahl der verfügbaren Optionen in einem Optionssatz kann sich ändern. Anstelle die Wert in einer Umgebung fest zu kodieren, sollten Sie beachten, ob verschiedene Optionen vorhanden sind. Sie können das System abfragen, um zu ermitteln, ob in der Umgebung verschiedene Optionen sind.
- Der Anzeigename einer Entität kann geändert werden. Der Standardanzeigename für die Firmenentität ist *Firma*. Dies könnte zu *Unternehmen* geändert werden. Wenn Sie einem Benutzer eine Nachricht anzeigen und auf den Namen der Entität verweisen möchten, sollten Sie nicht fest kodieren, sondern den Wert nutzen, der mit dem übereinstimmt, was der Benutzer gewohnt ist zu sehen und den Anzeigenamen verwenden, der von den Entitätsmetadaten abgerufen wurde.

## <a name="browse-the-metadata-for-your-organization"></a>Durchsuchen der Metadaten für die Organisation

Ein gutes Verständnis der Metadaten im System hilft dabei zu verstehen, wie die Common Data Service-Plattform funktioniert. Die Designer, die zum Bearbeiten der Metadaten verfügbar sind, können nicht alle Details anzeigen, die in den Metadaten gefunden werden. Sie können eine modellgesteuerte App mit dem Namen *Browser für Metadaten* installieren, die es Ihnen ermöglicht, alle ausgeblendeten Entitäten- und Metadateneigenschaften anzuzeigen, die im System vorhanden sind. Weitere Informationen zu *Browser für Metadaten*: [Durchsuchen der Metadaten für Ihre Organisation](browse-your-metadata.md)

## <a name="programmatically-work-with-metadata"></a>Programmtechnisch mit Metadaten arbeiten

Weitere Informationen zum programmgesteuerten Arbeiten mit Metadaten mittels:
- **Web-API**: [Verwenden der Web-API mit Common Data Service-Metadaten](webapi/use-web-api-metadata.md)
- **Organisationsservice**: [Verwenden des Organisationsservice mit Common Data Service-Metadaten](org-service/work-with-metadata.md)