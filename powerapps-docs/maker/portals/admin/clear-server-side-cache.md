---
title: Löschen des serverseitigen Caches für ein Portal | Microsoft-Dokumentation
description: Anleitungen zum Erzwingen, dass das Portal seinen Cache sofort aktualisiert.
author: sbmjais
manager: shujoshi
ms.service: powerapps
ms.topic: conceptual
ms.custom: ''
ms.date: 10/07/2019
ms.author: shjais
ms.reviewer: ''
ms.openlocfilehash: 8351ca8d3befec80a9e97da03ca62980383b01b1
ms.sourcegitcommit: 8185f87dddf05ee256491feab9873e9143535e02
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2019
ms.locfileid: "2709889"
---
# <a name="clear-the-server-side-cache-for-a-portal"></a>Löschen des serverseitigen Caches für ein Portal

Als Portaladministrator können Sie den serverseitigen Cache für das gesamte Portal löschen, damit aktualisierte Daten von Common Data Service direkt im Portal angezeigt werden. Updates von Common Data Service werden dem Portal im asynchronen Modus mitgeteilt, sodass unter Umständen eine Verzögerung zwischen dem Zeitpunkt, an dem Daten in Common Data Service aktualisiert werden, und dem Zeitpunkt, an dem diese Daten im Portal angezeigt werden, auftreten kann. Um diese Verzögerung zu eliminieren, beispielsweise, wenn sie Probleme mit der Portalkonfiguration verursacht, können Sie erzwingen, dass das Portal seinen Cache unmittelbar aktualisiert.

> [!NOTE]
> Das SLA für Cacheaktualisierung (Datenübertragung zwischen Common Data Service und Portal) ist 15 Minuten.

Löschen des serverseitigen Caches

1.  Melden Sie sich beim Portal als Administrator an.

2.  Navigieren Sie wie folgt zur URL: `<portal_path>/_services/about`

3.  Wählen Sie **Cache löschen** aus. 

Der serverseitige Cache wird gelöscht, und Daten werden von Common Data Service neu geladen. Beachten Sie, dass das Löschen des serverseitigen Portalcaches vorübergehend zu einer schlechten Portalleistung führt, wenn die Daten von Common Data Service neu geladen werden.

> [!div class=mx-imgBorder]
> ![Löschen des Portalcaches](../media/clear-portal-cache.png "Löschen des Portalcaches")
