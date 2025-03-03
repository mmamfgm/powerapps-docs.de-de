---
title: FAQ und Lernprogramm zu Buildtools| Microsoft Docs
description: 'Bei PowerApps build tools handelt es sich um eine Sammlung von PowerApps-spezifischen Azure DevOps-Buildaufgaben, die vermeiden, dass Skripts manuell heruntergeladen werden müssen, um die Entwicklung von PowerApps zu verwalten. In diesem Thema werden das Lernprogramm und die FAQs beschrieben, auf die Sie zugreifen können, um mehr über diese Tools zu erfahren. '
ms.custom: ''
ms.date: 07/21/2019
ms.reviewer: Dean-Haas
ms.service: powerapps
ms.topic: article
author: mikkelsen2000
ms.author: pemikkel
manager: kvivek
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 69736094b6c15d8731ec61f614da3085bed14924
ms.sourcegitcommit: 8185f87dddf05ee256491feab9873e9143535e02
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2019
ms.locfileid: "2748437"
---
# <a name="tutorial-and-faq"></a>Lernprogramm und FAQ


[!INCLUDE [cc-beta-prerelease-disclaimer](../../includes/cc-beta-prerelease-disclaimer.md)]
Verwenden Sie das Lernprogramm und die FAQs, um weitere Informationen zu den PowerApps build tools für Azure DevOps zu erfahren. 

## <a name="hands-on-lab"></a>Praktische Übungseinheit

Die praktische Übungseinheit ist [hier](https://github.com/microsoft/PowerApps-Samples/tree/master/azure/build-tools) verfügbar.

Die praktische Übungseinheit bietet ein Lernprogramm mit schrittweisen Anweisungen zur Erstellung des folgenden Szenarios:

1. Richten Sie Entwicklungs-, Erstellungs- und Produktionsumgebungen ein.
2. Erstellen Sie eine Beispielapp.
3. Exportieren Sie eine Lösung, welche die Beispiel-App aus einer Entwicklungsumgebung enthält.
4. Entpacken Sie die Lösung.
5. Übernehmen Sie die Lösung in die Quelle (Repo).
6. Importieren Sie die nicht verwaltete Lösung in eine Buildumgebung.
7. Erstellen Sie ein Buildartefakt (verwaltete Lösung).
8. Stellen Sie die Lösung in einer Downstreamumgebung bereit.

> [!NOTE]
> Die praktische Übungseinheit bietet praktische Erfahrungen, für die Benutzer, die keine Erfahrung mit Azure DevOps haben und lernen möchten, wie Pipelines in Azure DevOps erstellt werden. Die fertigen Pipelines, die Sie erstellt haben, können auch aus dem Lernprogramm heruntergeladen werden und „wie besehen“ mit wenigen Anpassungen an Umgebungsvariablen, Quell-/Zielordnern und Repositorys verwendet werden.  

## <a name="frequently-asked-question-faq"></a>Häufig gestellte Fragen (FAQ)

**Funktionieren PowerApps build tools nur für PowerApps?**  

*Die PowerApps build tools funktionieren für PowerApps und modellgesteuerte Apps in Dynamics 365 wie z. B. Dynamics 365 Sales und Dynamics 365 Customer Service. Separate Buildaufgaben sind für Microsoft Dynamics for Finance and Operations verfügbar.*

**Kann ich Flow- und Canvas-Apps einbeziehen?**

*Ja, Flow- und Canvas-Apps sind für die Lösung aktiviert. Wenn diese Ihrer Lösung hinzugefügt werden, können sie am Lebenszyklus der App teilnehmen. Allerdings erfordern einige Schritte noch manuelle Konfigurationen. Dies wird im Laufe des Jahrs behoben, wenn wir Umgebungsvariablen und Konnektoren einführen.*

**Wie viel kosten die PowerApps build tools?**

*Die PowerApps build tools sind kostenlos erhältlich. Es ist jedoch ein gültiges Azure DevOps-Abonnement erforderlich, um die  build tools zu nutzen. Weitere Informationen sind [hier](https://azure.microsoft.com/pricing/details/devops/azure-devops-services/) verfügbar.*

**Ich kann die Erweiterung anzeigen, aber warum ist keine Option verfügbar, um sie zu installieren?**

*Wenn die Option zur **Installation** (siehe Screenshot unten) nicht angezeigt wird, haben Sie wahrscheinlich nicht die erforderlichen Rechte in Ihrer Azure DevOps-Organisation. Weitere Informationen finden Sie [hier](https://docs.microsoft.com/azure/devops/marketplace/how-to/grant-permissions?view=azure-devops).*

![Buildaufgabenbildschirm](media/build-tasks.png)