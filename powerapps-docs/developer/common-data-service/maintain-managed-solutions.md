---
title: Pflegen von verwalteten Lösungen (Common Data Service) | Microsoft-Dokumentation
description: ''
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: shmcarth
ms.author: jdaly
manager: ryjones
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 72d1960bcdab96f1bd2f899bb4573f8f20d0e9a5
ms.sourcegitcommit: 8185f87dddf05ee256491feab9873e9143535e02
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2019
ms.locfileid: "2748272"
---
# <a name="maintain-managed-solutions"></a>Pflegen von verwalteten Lösungen

Bevor Sie die verwaltete Lösung freigeben, sollten Sie überlegen, wie Sie sie pflegen. Die De- und Neuinstallation einer verwalteten Lösung ist praktisch nie eine Option, wenn die Lösung Entitäten oder Attribute enthält. Dies liegt daran, dass Daten verloren gehen, wenn Entitäten gelöscht werden. Glücklicherweise bieten Lösungen eine Möglichkeit, die verwaltete Lösung unter Beibehaltung der Daten zu aktualisieren. Wie Sie Ihre Lösungen aktualisieren, hängt genau von den Eigenschaften der Lösung und den Anforderungen der Änderung ab.  

<a name="BKMK_VersionCompatibilty"></a>   

## <a name="version-compatibility"></a>Versionskompatibilität  
 Aus einer neueren Version von Common Data Service exportierte Lösungen können nicht in ältere Versionen von Dynamics 365 importiert werden. Hierzu zählen Haupt- und Nebenversionen. Lösungen, die aus einer früheren Version von Dynamics 365 exportiert wurden, können in spätere Versionen wie im folgenden Diagramm angezeigt importiert werden.  
  
![Lösungsversions-Kompatibilität](media/crm_v9.0_solution_compatibility_chart.png)
  
 Da zusätzliche Updaterollups oder Serviceupdates für Common Data Service angewendet werden, können Lösungen, die aus Organisationen mit diesen Updates exportiert wurden, nicht in Organisationen importiert werden, die nicht über diese Updates verfügen. Weitere Informationen: [Einführung in Lösungen](introduction-solutions.md).  
  
 Das Stammelement `<ImportExportXml>`- Stammelement verwendet ein `SolutionPackageVersion`-Attribut, um den Wert für die Version festzulegen, mit der die Lösung kompatibel ist. Sie sollten diesen Wert nicht manuell bearbeiten.  
  
<a name="BKMK_CreateManagedSolutionUpdates"></a>   
## <a name="create-managed-solution-updates"></a>Erstellen von Aktualisierungen einer verwalteten Lösung  
 Es gibt zwei grundlegende Ansätze zum Aktualisieren von Lösungen:  
  
-   Veröffentlichen Sie eine neue Version Ihrer verwalteten Lösung  
  
-   Veröffentlichen Sie ein Update für die verwaltete Lösung  
  
<a name="BKMK_ReleaseANewVersion"></a>   
### <a name="release-a-new-version-of-your-managed-solution"></a>Veröffentlichen Sie eine neue Version Ihrer verwalteten Lösung  
 Die bevorzugte Methode ist die Veröffentlichung einer neuen Version Ihrer verwalteten Lösung. Mithilfe der ursprünglichen nicht verwalteten Quelllösung können Sie erforderliche Änderungen vornehmen und die Versionsnummer der Lösung erhöhen, bevor Sie sie als verwaltete Lösung bereitstellen. Wenn die Organisationen, die Ihre Lösung verwenden, die neue Version installieren, werden ihre Funktionen so aktualisiert, dass sie Ihre Änderungen enthalten. Wenn Sie zum Verhalten in einer früheren Version zurückkehren möchten, installieren Sie einfach die Vorgängerversion neu. Dieses überschreibt alle Lösungskomponenten mit den Definitionen der früheren Version, entfernt aber nicht die Lösungskomponenten, die in der neueren Version hinzugefügt werden. Diese neueren Lösungskomponenten bleiben im System, haben aber keine Auswirkung, da die älteren Lösungskomponentendefinitionen sie nicht verwenden.  
  
 Während der Installation einer früheren Version einer Lösung bestätigt Common Data Service, dass die Person, die die Vorgängerversion installiert, fortfahren möchte.  
<a name="BKMK_ReleaseAnUpdate"></a>   
### <a name="release-an-update-for-your-managed-solution"></a>Veröffentlichen Sie ein Update für die verwaltete Lösung  
 Wenn nur eine kleine Teilmenge von Lösungskomponenten dringend eine Änderung erfordert, können Sie ein Update veröffentlichen, um das Problem zu lösen. Um ein Update zu veröffentlichen, erstellen Sie eine neue nicht verwalteten Lösung und fügen Sie jegliche Komponenten von der ursprünglichen nicht verwalteten Quelllösung hinzu, die Sie aktualisieren möchten. Sie müssen die neue nicht verwaltete Lösung demselben Herausgeberdatensatz zuordnen, der für die ursprüngliche Lösung verwendet wurde. Wenn Sie die Änderungen fertiggestellt haben, stellen Sie die neue Lösung als verwaltete Lösung bereit.  
  
 Wenn die in Updatelösung in einer Organisation installiert wird, in der die ursprüngliche Lösung installiert wurde, werden die Änderungen, die in dem Update enthalten sind, auf die Organisation angewendet. Wenn eine Organisation einen „Rollback“ auf die ursprüngliche Version durchführen muss, können sie das Update einfach deinstallieren.  
  
 Alle Anpassungen, die auf die Lösungskomponenten im Update angewendet wurden, werden überschrieben. Wenn Sie das Update deinstallieren, kehren sie wieder zurück.  
  
### <a name="see-also"></a>Siehe auch  
 [Planen einer Lösungsentwicklung](/dynamics365/customer-engagement/developer/plan-solution-development)   
 [App auf AppSource veröffentlichen](publish-app-appsource.md)
