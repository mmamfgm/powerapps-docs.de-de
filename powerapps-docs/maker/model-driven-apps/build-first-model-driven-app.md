---
title: Erstellen Sie Ihre erste modellgesteuerte App komplett neu mit PowerApps | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie eine einfache modellgetriebene App erstellen
documentationcenter: ''
author: Mattp123
manager: kvivek
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: model
ms.date: 02/05/2019
ms.author: matp
search.audienceType:
- maker
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 9c41feb81fbe90c1ca675105fe898b667f61b2b9
ms.sourcegitcommit: d9cecdd5a35279d78aa1b6c9fc642e36a4e4612c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "2752534"
---
# <a name="build-your-first-model-driven-app-from-scratch"></a>Erstellen Sie Ihre erste Modell-angetriebene App neu
Modell-angetriebener App-Entwurf ist eine Komponenten-fokussierte Methode zur App-Entwicklung. In diesem Thema vereinfachen Sie, wie Sie eine modellgesteuerte App erstellen, indem Sie eine der Standardentitäten verwenden, die in Ihrer PowerApps-Umgebung verfügbar ist.

> [!TIP]
> Um alles über das Erstellen von Modell-angetriebene Apps zu erfahren, beginnen Sie hier: [Modell-angetriebene App-Komponenten verstehen](model-driven-app-components.md). 

## <a name="sign-in-to-powerapps"></a>Bei PowerApps anmelden
Melden Sie sich bei [PowerApps](https://make.powerapps.com/) an. Wenn Sie noch kein [!INCLUDE [powerapps](../../includes/powerapps.md)] Konto haben, wählen Sie den Link **Kostenlos beginnen** aus. 

## <a name="create-your-model-driven-app"></a>Erstellen Sie Ihre modellgesteuerte Anwendung

1.  Wählen Sie die gewünschte Umgebung aus oder gehen Sie zu [PowerApps-Administratorcenter](https://admin.powerapps.com/), um eine neue zu erstellen.

  > [!IMPORTANT]
  > "Wenn der **Modell-angetriebe** Entwurfsmodus nicht verfügbar ist, müssen Sie ggf eine [Umgebung erstellen](https://docs.microsoft.com/powerapps/administrator/create-environment).   

2. Wählen Sie auf der **Startseite** die Option **Modellgetriebene App aus dem Leerfeld**.
<!-- ![Start-from-blank_model](media/build-first-model-driven-app/start-from-blank-model-driven.png) -->

3.  Klicken Sie auf der Seite **Eine neue App erstellen "** und geben Sie die folgenden Details ein und wählen dann **Fertig** aus: 
  - **Name**: Geben Sie einen Namen für die App ein, z. B. *Meine erste App*. 
  - **Eindeutiger Name**: Standardmäßig verwendet der eindeutige Name den Namen, den Sie im Feld **Name** ohne Leerzeichen angegeben haben und der durch das Verlagspräfix und einen Unterstrich (_) eingeleitet wird. Zum Beispiel *crecf_Myfirstapp*. Weitere Informationen [Lösungsherausgeberpräfix ändern](../common-data-service/change-solution-publisher-prefix.md)
  - **Beschreibung**: Geben Sie eine kurze Beschreibung ein, um was es bei der App geht, wie *Dies ist meine erste App*.
Informationen zu den zusätzlichen App-Eigenschaften finden Sie unter [Eine App erstellen](create-edit-app.md#create-an-app)

    > [!div class="mx-imgBorder"] 
    > ![](media/create-new-app.png "Create a new app") 


## <a name="add-components-to-your-app"></a>Fügen Sie der App zusätzliche Komponenten hinzu.
Im Anwendungs-Designer fügen Sie Komponenten der App hinzu.
1.  Wählen Sie den Pfeil **Siteübersichts-Designer öffnen**, um den Siteübersichtsdesigner zu öffnen. 

    ![Erstellen von neuen Sitemaps](media/build-first-model-driven-app/new-sitemap.png)

2.  Klicken Sie im Siteübersichtsdesigner im rechten Bereich **Neuer Unterbereich** wählen Sie die **Eigenschaften**, und dann die folgenden Eigenschaften aus.
  - **Typ**. Entität
  - **Entität**: Firma

    ![So fügen Sie Komponenten der Siteübersicht hinzu](media/build-first-model-driven-app/sitemap.png)

3.  Klicken Sie auf **Speichern und schließen**.
4.  Auf dem App-Designer Canvas wählen Sie **Formulare** und anschließend im rechten Bereich **Hauptformulare** und wählen in der Gruppe **Firma**.

    ![Kontohauptformular](media/build-first-model-driven-app/main-form.png)

5.  Auf dem App-Designer-Canvas wählen Sie die Option **Ansichten** und dann **Aktive Firmen**, **Alle Firmen** und **Meine aktiven Firmen** Ansicht aus.

    ![Anzeigen von Konten](media/build-first-model-driven-app/views.png)

6. Auf der App-Designer-Canvas wählen Sie die Option **Diagramme** und wählen dann das Diagramm aus **Firmen nach Branche**.
7. Wählen Sie auf der Symbolleiste des App-Designers **Speichern** aus.

    ![App-Designer Systemleiste speichern](media/build-first-model-driven-app/app-designer-toolbar.png)
 
<!-- ##  Validate your app
This step checks for component dependencies that are required for the app to work, but haven't yet been added to the app. 

1. On the app designer canvas, select the component that indicates a dependency, such as the **Forms** component. Then, on the right-pane select the **Required** tab, expand **Entity Dependencies** and then select all required dependencies. 

    ![Add dependencies](media/build-first-model-driven-app/resolve-dependencies.png)

2. Select **Add Dependencies**.
3. On the app designer toolbar, select **Save**.  -->

## <a name="publish-your-app"></a>Veröffentlichen der App.
Wählen Sie auf der Symbolleiste des App-Designers **Veröffentlichen** aus.

Nachdem die App veröffentlicht wurde, ist Sie bereit, dass Sie sie ausführen oder teilen können.

![Einfache Firmaenentitäts-App](media/build-first-model-driven-app/accounts-quickstart-app.png)

## <a name="next-steps"></a>Nächste Schritte
In diesem Thema werden Modell-angetriebene einfache Apps erstellt. 
- Zur Anzeige der App beim Ausführen, gehen sie zu [Modell-angetriebene App auf einem mobilen Gerät ausführen](../../user/run-app-client-model-driven.md).
- Informationen zum teilen Ihrer App finden Sie unter [Eine Modell-angetriebenen App freigeben](share-model-driven-app.md).
- Um alles über das Erstellen von Modell-angetriebene Apps zu erfahren, beginnen Sie hier: [Modell-angetriebene App-Komponenten verstehen](model-driven-app-components.md).
