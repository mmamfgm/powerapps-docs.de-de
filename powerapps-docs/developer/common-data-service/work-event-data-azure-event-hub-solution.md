---
title: Arbeiten mit Dynamics 365-Ereignisdaten in Ihrer Azure-Ereignishub-Lösung (Common Data Service) | Microsoft Docs
description: In dem Artikel wird die Arbeit mit Ereignisdaten in der Azure-Ereignishublösung beschrieben.
keywords: ''
ms.date: 05/08/2019
ms.service: powerapps
ms.topic: article
ms.assetid: a3732c49-7f47-d87c-5062-585ef28ab511
author: JimDaly
ms.author: jdaly
manager: ryjones
ms.reviewer: pehecke
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: e004b1b5699e0f4fa21241af23eb14987ba781ec
ms.sourcegitcommit: 8185f87dddf05ee256491feab9873e9143535e02
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2019
ms.locfileid: "2748592"
---
# <a name="work-with-common-data-service-event-data-in-your-azure-event-hub-solution"></a>Arbeiten mit Common Data Service-Ereignisdaten in Ihrer Azure-Ereignishub-Lösung

Azure Event Hubs ist ein hoch-skalierbarer öffentlicher Abonnementservice, der Millionen von Ereignissen pro Sekunde übernehmen und in mehrere Anwendungen streamen kann. Die Common Data Service-Azure-Schnittstelle ermöglicht, dass Ihre Ereignisdaten im Azure Service Bus veröffentlicht und den Abonnenten Ihrer Ereignishublösung zur Verfügung gestellt werden. Die folgenden Informationen beschreiben die allgemeinen Aufgaben, die abgeschlossen werden müssen, um Azure-Ereignisdaten an eine Ereignishublösung zu schicken.  
  
> [!NOTE]
> Ein Azure-Abonnement und eine Ereignishublizenz sind für den Zugriff auf Ereignishubs erforderlich.
  
## <a name="1-create-an-event-hub"></a>1. Ereignishub erstellen  
 Sie können einen Ereignishub in Azure entweder durch eine API-Programmierung erstellen oder interaktiv über das [klassische Azure-Portal](https://manage.windowsazure.com). Unabhängig von der Art der Erstellung des Ereignishubs benötigen Sie anschließend eine Kopie der Ereignishub-Verbindungszeichenfolge. Diese Verbindungszeichenfolge müssen Sie bereitstellen, wenn Sie den Azure-Dienstendpunkt registrieren, der im nächsten Abschnitt beschrieben wird.  
  
 Weitere Informationen zum Erstellen von Ereignishubs finden Sie unter [Event Hubs – Dokumentation](https://azure.microsoft.com/documentation/services/event-hubs/).  
  
## <a name="2-register-an-endpoint"></a>2. Endpunkt registrieren  
 Das Registrieren eines Dienstendpunkts ähnelt dem Registrieren für irgendeine andere unterstützte Vertragsart wie Warteschlangen und Themen. Sie benutzen das Plug-In-Registrierungstool, das über den SDK-Download bereitgestellt wird, um den Dienstendpunkt zu registrieren.  Wenn Sie das Anmeldeformular ausfüllen, geben Sie den Vertragstyp **Ereignishub** an. Für das Nachrichtentextformat können Sie **XML** oder **JSON** wählen. Darüber hinaus ist nur die SAS-Autorisierung erlaubt, und Sie müssen die Verbindungszeichenfolge bereitstellen, die Sie beim Erstellen des Ereignishubs erhalten haben. Weitere Informationen: [Lernprogramm: Konfigurieren von Microsoft Azure (SAS) für die Integration mit Common Data Service](walkthrough-configure-azure-sas-integration.md).  
  
## <a name="3-register-code"></a>3. Code registrieren  
 Dynamics 365 muss den genauen Vorgang (Entität/Nachrichtenkombination) kennen, der bei der Verarbeitung dazu führt, dass das Azure-fähige Plug-In ausgeführt wird. Da Sie einen Ereignishub erstellen, würde dieser Vorgang insbesondere mit der Verarbeitung von Azure-Ereignisdaten zusammenhängen. Sie müssen einen Schritt für das Azure-fähige Plug-In in der Azure-Ereignisausführungspipeline registrieren.  Weitere Informationen finden Sie unter [Lernprogramm: Registrieren eines Azure-fähigen Plug-Ins mithilfe des Plug-In-Registrierungstools](walkthrough-register-azure-aware-plug-in-using-plug-in-registration-tool.md).  
  
 Wenn Sie eine Azur-fähige benutzerdefinierte Workflowaktivität anstelle eines Plug-Ins verwenden, würden Sie die Aktivitäts-Assembly über das Plug-In-Registrierungstools registrieren und die Aktivität in den Workflow einschließen. Weitere Informationen finden Sie unter [Beispiel: Azure-fähige benutzerdefinierte Workflowaktivität](/dynamics365/customer-engagement/developer/sample-azure-aware-custom-workflow-activity).
  
## <a name="4-start-listening"></a>4. Listening starten  
 Starten Sie das Überwachen Ihrer Azure-Servicehublösungsanwendung auf dem Dienstendpunkt  
  
## <a name="5-trigger"></a>5. Auslöser  
 Führen Sie einen Vorgang in Azure aus, der dazu führen würde, dass das Plug-In oder der Workflow mit der benutzerdefinierte Workflowaktivität ausgeführt wird. Dieses ist die gleiche Operation (Entität/Nachrichtenkombination), für die Sie den Plug-In-Schritt im vorherigen Abschnitt dieses Themas registriert haben. Sie können den beabsichtigten Vorgang durchführen, indem Sie die Webanwendung nutzen. Sie können auch einen Anwendungscode verwenden, der auf die Azure-Webdienste zugreift.  
  
## <a name="6-verification"></a>6. Überprüfung  
 Sie können den entsprechenden Systemauftrag in der Azure-Webanwendung prüfen und nachsehen, ob der Status **Erfolgreich** ist. Lautet der Status **Fehler**, verwenden Sie die Statusangaben, um die mögliche Ursache des Fehlers zu identifizieren. Sie können dann die Konfigurationen beider Systeme erneut prüfen oder den Anwendungscode debuggen, um das Problem abhängig von der Art des Fehlers zu lokalisieren und zu beheben.  
  
### <a name="see-also"></a>Siehe auch  
 [Azure-Integration in Common Data Service](azure-integration.md)
