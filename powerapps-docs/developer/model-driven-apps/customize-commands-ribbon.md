---
title: Passen Sie Befehle und Menüband an (modellgesteuerte Apps) | Microsoft Docs
description: Befehle werden in Common Data Service in unterschiedlicher Weise abhängig von der Entität und dem Client angezeigt. An den meisten Stellen in der Webanwendung wird eine Befehlsleiste anstelle eines Menübands angezeigt. Dynamics 365 für Tablets verwendet auch Daten, die als Menübänder definiert sind, um zu steuern, welche Befehle auf einer für Toucheingabe optimierten Befehlsleiste verfügbar sind.
keywords: ''
ms.date: 10/31/2018
ms.service: powerapps
ms.topic: article
ms.assetid: 926364b0-ede6-00e9-39d4-5aae5e00be0b
author: JimDaly
ms.author: jdaly
manager: shilpas
ms.reviewer: ''
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 508ea8788f0fbaf9823721958229c3ed3cd21d55
ms.sourcegitcommit: d9cecdd5a35279d78aa1b6c9fc642e36a4e4612c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "2754583"
---
# <a name="customize-commands-and-the-ribbon"></a>Passen Sie Befehle und das Menüband an

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/customize-dev/customize-commands-ribbon -->

 Befehle werden in Common Data Service in unterschiedlicher Weise abhängig von der Entität und dem Client angezeigt. An den meisten Stellen in der Webanwendung wird eine *Befehlsleiste* anstelle eines Menübands angezeigt. Dynamics 365 for Tablets verwendet auch Daten, die als Menübänder definiert sind, um zu steuern, welche Befehle auf einer für Toucheingabe optimierten Befehlsleiste verfügbar sind.  
  
 Die Befehlsleiste bietet verbesserte Leistung. Das Menüband wird weiterhin in der Webanwendung für bestimmte Entitätsformulare angezeigt und für Listenansichten in Dynamics 365 for Outlook verwendet.  
  
 Sowohl die Befehlsleiste wie auch das Menüband verwenden die gleichen XML-Daten, um zu definieren, welche Befehle angezeigt werden, wann sie aktiviert werden und welche Aktionen dadurch ausgeführt werden.  
  
 Die Themen in diesem Abschnitt bieten Ihnen eine Einführung in die wichtigsten Konzepte, deren Verständnis bei der Anpassung der Befehlsleiste oder des Menübands vorausgesetzt wird, sowie in häufige Aufgaben, die Sie dabei ausführen werden.  
  
> [!NOTE]
>  Da das zugrunde liegende XML-Schema für die Anzeige von Befehlen als Menübänder konzipiert wurde, wird der Begriff *Menüband* weiterhin in der Dokumentation verwendet werden.  
  
 Das SDK beschreibt den Vorgang zum Bearbeiten des Menübands durch direkte Bearbeitung der Datei customization.xml. Einige Benutzer haben Ribbon-Editoren erstellt, die eine Benutzeroberfläche bieten, die das Bearbeiten des Menübands vereinfacht. Gegenwärtig sind die folgenden Projekte u. a auf Codeplex verfügbar:  
  
- [Menüband-Workbench](https://www.develop1.net/public/rwb/ribbonworkbench.aspx)  
  
- [MS CRM 2011: Pragma-Toolkit: Menüband, Siteübersichtseditor](https://pragmatoolkit.codeplex.com/)  
  
- [Visueller Ribbon-Editor für CRM 2011](https://crmvisualribbonedit.codeplex.com/)  
  
  Um Support oder Hilfe für die Verwendung der Software zu erhalten, setzen Sie sich mit dem Programmherausgeber in Verbindung.  
  
  
## <a name="see-also"></a>Siehe auch  

 [Menüband-Core-Schema](ribbon-core-schema.md)  
 [Menübandtypenschema](ribbon-types-schema.md)  
 [Menüband-WSS-Schema](ribbon-wss-schema.md)<br/> 
 [Beispiel: Exportieren von Menübanddefinitionen](sample-export-ribbon-definitions.md)<br/> 
 [Anwenden von Geschäftslogik mit Client-Skripting in modellgesteuerten Apps](client-scripting.md)
