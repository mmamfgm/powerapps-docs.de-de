---
title: Benutzerdefiniertes Azure-fähiges Plug-In (Common Data Service) | Microsoft-Dokumentation
description: Dieses Beispiel-Plugin kann den Pipeline-Ausführungskontext auf den Azure Service Bus posten.
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: JimDaly
ms.author: jdaly
manager: ryjones
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 1148a8e6194a5aa78cda9f01c458c8c817dd261c
ms.sourcegitcommit: 8185f87dddf05ee256491feab9873e9143535e02
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2019
ms.locfileid: "2748528"
---
# <a name="sample-azure-aware-custom-plug-in"></a>Beispiel: Benutzerdefiniertes Azure-fähiges Plug-In

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/sample-azure-aware-custom-plugin -->

Das Plug-In demonstriert, wie der Ausführungskontext und der Nachverfolgungsdienst vom Dienstanbieterparameter der `Execute`-Methode abgerufen werden kann. Das Plug-In veröffentlicht den Kontext dann auf dem Azure Service Bus-Endpunkt und schreibt Informationen in das Ablaufverfolgungsprotokoll, um das Debuggen zu erleichtern. Sie können das Beispiel von [hier](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/Azureplugin) herunterladen.

## <a name="how-to-run-this-sample"></a>Wie man dieses Beispiel ausführt

1. Um eine lokale Kopie zu erhalten, laden Sie den [Beispielbericht](https://github.com/Microsoft/PowerApps-Samples) herunter, oder klonen Sie ihn.
2. Öffnen Sie die Beispiellösung in Visual Studio und signieren Sie die Assembly mit einem Schlüssel.
3. Registrieren Sie das Plugin mit dem **Plug-in-Registrierungstool**.

>[!NOTE]
> Dieses Beispiel erfordert, dass zuerst ein Service-Endpunkt erstellt und seine ID über den unsicheren Konfigurationsparameter an den Plugin-Konstruktor übergeben wird, wenn der Plugin-Schritt registriert wird.


