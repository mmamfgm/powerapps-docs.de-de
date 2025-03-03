---
title: Hinzufügen der Team-Entität als Suchoption in Ihrer App | MicrosoftDocs
description: Erfahren Sie mehr über das Hinzufügen der Team-Entität als Suchoption in Ihrer App
ms.custom: ''
ms.date: 07/24/2019
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
- powerapps
author: Mattp123
ms.assetid: ''
caps.latest.revision: 25
ms.author: matp
manager: kvivek
search.audienceType:
- maker
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 3db46288b0f1fc384cae8c683648d1dd0a945d44
ms.sourcegitcommit: 8185f87dddf05ee256491feab9873e9143535e02
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2019
ms.locfileid: "2710857"
---
# <a name="add-the-team-entity-as-a-lookup-option-in-your-app"></a>Hinzufügen der Team-Entität als Suchoption in Ihrer App

Damit die Team-Entität in einer Suche bei Apps der Einheitlichen Oberfläche verfügbar ist, muss sie zur App hinzugefügt werden. Kontaktdatensätze können z. B. einem Benutzer oder einem Team zugewiesen werden.  

> [!div class="mx-imgBorder"] 
> ![](media/entity-lookup-teams.png "Entity lookup with both users and teams available")

Wenn jedoch die Benutzerentität in der App enthalten ist, die Teamentität allerdings nicht, werden nur Benutzerdatensätze in einer Suche angezeigt. 

> [!div class="mx-imgBorder"] 
> ![](media/entity-lookup-user-only.png "Entity lookup with users only")

## <a name="add-the-team-entity-to-an-app"></a>Fügen Sie die Team-Entität einer App hinzu

1. Öffnen Sie die App im App-Designer. 
2. Wählen Sie die Registerkarte **Komponenten** aus, wählen Sie **Entitäten** aus, und wählen Sie dann **Team** aus.    

    > [!div class="mx-imgBorder"] 
    > ![](media/add-team-entity-app.png "Add the team entity to the app")

3. Wählen Sie **Speichern** aus, und wählen Sie **Veröffentlichen** aus, um die Änderungen App-Benutzern bereitzustellen.   

