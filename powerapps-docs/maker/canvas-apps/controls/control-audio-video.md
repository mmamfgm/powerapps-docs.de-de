---
title: 'Audio- und Video-Steuerelemente: Referenz | Microsoft-Dokumentation'
description: Informationen, einschließlich Eigenschaften und Beispiele, über Audio- und Video-Steuerelemente
author: chmoncay
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.date: 10/25/2016
ms.author: chmoncay
ms.reviewer: tapanm
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 3b8c5ea5ee2784bc1ab97d6943045cee8da6a52f
ms.sourcegitcommit: 8e42a5996799d9831f8c5a52b0b051a6088d9ce7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2019
ms.locfileid: "73650790"
---
# <a name="audio-and-video-controls-in-powerapps"></a>Audio- und Video-Steuerelemente in PowerApps
Ein Steuerelement, das eine Audiodatei, eine Videodatei oder Videos auf YouTube abspielt.

## <a name="description"></a>Beschreibung
In einem **Audio**-Steuerelement kann ein Audioclip aus einer Datei, eine Aufzeichnung aus einem **[Mikrofon](control-microphone.md)** -Steuerelement oder die Audiospur aus einer Videodatei abgespielt werden.

Ein **Video**-Steuerelement spielt ein Video aus einer Datei, von YouTube oder Azure Media Services ab.  Auf Wunsch können auch Untertitel angezeigt werden.

## <a name="key-properties"></a>Haupteigenschaften
**Loop** – Gibt an, ob ein Audio- oder Videoclip am Ende der Wiedergabe automatisch neu gestartet wird.

**Media**: Ein Bezeichner für den Clip, der von einem Audio- oder Video-Steuerelement wiedergegeben wird.

**ShowControls**: Gibt beispielsweise an, ob für einen Audio- oder Videoplayer eine Schaltfläche für die Wiedergabe und ein Lautstärkeregler und für ein Stift-Steuerelement Symbole zum Zeichnen oder Löschen angezeigt werden.

## <a name="additional-properties"></a>Zusätzliche Eigenschaften
**[AccessibleLabel](properties-accessibility.md)** : Bezeichnung für Sprachausgaben Sollte dem Titel des Videos oder der Audiodatei entsprechen.

**AutoPause**: Gibt an, ob ein Audio- oder Videoclip automatisch angehalten wird, wenn der Benutzer zu einem anderen Bildschirm navigiert.

**AutoStart**: Gibt an, ob ein Audio- oder Video-Steuerelement automatisch einen Clip wiedergibt, wenn der Benutzer zu dem Bildschirm navigiert, der das Steuerelement enthält.

**[BorderColor](properties-color-border.md)** – Die Farbe des Rahmens eines Steuerelements.

**[BorderStyle](properties-color-border.md)** – Legt fest, ob der Rahmen eines Steuerelements **Solid** (Durchgehend), **Dashed** (Gestrichelt), **Dotted** (Gepunktet) oder **None** (Keiner) ist.

**[BorderThickness](properties-color-border.md)** – Die Stärke des Rahmens eines Steuerelements.

**ClosedCaptionsUrl** – Steuerelement nur für Videos.  URL der Datei mit den Untertiteln für Hörgeschädigte im WebVTT-Format.  Video- und Untertitel-URL müssen HTTPS-URLs sein. Auf dem Server, auf dem die Video- und Untertiteldateien gehostet werden, muss CORS aktiviert sein.

**[DisplayMode](properties-core.md)** : Legt fest, ob das Steuerelement Benutzereingaben zulässt (**Edit**, Bearbeiten), ob nur Daten angezeigt werden (**View**, Anzeigen) oder ob das Steuerelement deaktiviert ist (**Disabled**, Deaktiviert).

**[Fill](properties-color-border.md)** – Die Hintergrundfarbe eines Steuerelements.

**[FocusedBorderColor](properties-color-border.md)** : die Rahmenfarbe eines Steuerelements, wenn das Steuerelement der Fokus ist.

**[FocusedBorderThickness](properties-color-border.md)** : die Rahmendicke eines Steuerelements, wenn das Steuerelement der Fokus ist.

**[Height](properties-size-location.md)** – Die Entfernung zwischen dem oberen und unteren Rand eines Steuerelements.

**[Image](properties-visual.md)** : Der Name des Bilds, das in einem Bild-, Audio- oder Mikrofon-Steuerelement angezeigt wird.

**[ImagePosition](properties-visual.md)** : Die Position (**Fill**, **Fit**, **Stretch**, **Tile** oder **Center**) eines Bilds auf einem Bildschirm oder in einem Steuerelement, wenn die Größe nicht mit der Bildgröße identisch ist.

**OnEnd** – Gibt an, wie eine App reagiert, wenn die Wiedergabe eines Audio- oder Videoclips beendet ist.

**OnPause** – Gibt an, wie eine App reagiert, wenn der Benutzer den Clip anhält, der von einem Audio- oder Video-Steuerelement wiedergegeben wird.

**OnStart**: gibt an, wie die App reagiert, wenn der Benutzer eine Aufzeichnung mit einem Steuerelement-Mikrofon beginnt.

**Paused** – Ist *true*, wenn ein Steuerelement zum Wiedergeben von Medien angehalten wurde, andernfalls *false*.

**[Reset](properties-core.md)** : Gibt an, ob ein Steuerelement auf seinen Standardwert zurückgesetzt wird.

**Start**: Gibt an, ob ein Audio- oder Videoclip wiedergegeben wird.

**StartTime** – Der Zeitpunkt nach dem Start eines Audio- oder Videoclips, zu dem die Wiedergabe des Clips beginnt.

**Time** – Die aktuelle Position eines Mediensteuerelements.

**[TabIndex](properties-accessibility.md)** : Navigationsreihenfolge der Tastatur in Bezug auf andere Steuerelemente.

**[QuickInfo](properties-core.md)** : Erklärender Text, der angezeigt wird, wenn der Benutzer auf ein Steuerelement zeigt.

**[Visible](properties-core.md)** – Legt fest, ob ein Steuerelement angezeigt wird oder ausgeblendet ist.

**[Width](properties-size-location.md)** – Der Abstand zwischen dem linken und rechten Rand eines Steuerelements.

**[X](properties-size-location.md)** – Der Abstand zwischen dem linken Rand eines Steuerelements und dem linken Rand des übergeordneten Containers (bzw. des Bildschirms, wenn kein übergeordneter Container vorhanden ist).

**[Y](properties-size-location.md)** – Der Abstand zwischen dem oberen Rand eines Steuerelements und dem oberen Rand des übergeordneten Containers (bzw. des Bildschirms, wenn kein übergeordneter Container vorhanden ist).

## <a name="related-functions"></a>Verwandte Funktionen
[**First**( *TableName* )](../functions/function-first-last.md)

## <a name="examples"></a>Beispiele
### <a name="play-an-audio-or-video-file"></a>Wiedergeben einer Audio- oder Videodatei
1. Klicken oder tippen Sie im Menü **Datei** auf **Medien**, klicken oder tippen Sie auf **Videos** oder **Audio**, und klicken oder tippen Sie dann auf **Durchsuchen**.
2. Navigieren Sie zu der Datei, die Sie verwenden möchten, klicken oder tippen Sie darauf und dann auf **Öffnen**.
3. Drücken Sie ESC, um zum Standardarbeitsbereich zurückzukehren, fügen Sie ein **Audio**- oder **Video**-Steuerelement hinzu, und legen Sie die **Media**-Eigenschaft auf die hinzugefügte Datei fest.

    Möchten Sie wissen, wie Sie ein [Steuerelement hinzufügen und konfigurieren](../add-configure-controls.md)?
4. Drücken Sie F5, und spielen Sie den Clip durch Klicken oder Tippen auf die Wiedergabeschaltfläche des Steuerelements ab, das Sie hinzugefügt haben.

    > [!TIP]
   > Die Wiedergabeschaltfläche für das **Video**-Steuerelement wird angezeigt, wenn Sie auf das Steuerelement zeigen.
5. Drücken Sie die ESC-TASTE, um zum Standardarbeitsbereich zurückzukehren.

### <a name="play-a-youtube-video"></a>Abspielen eines YouTube-Videos
1. Fügen Sie ein **Video**-Steuerelement hinzu, und legen Sie die **Media**-Eigenschaft auf die URL (in doppelten Anführungszeichen) eines YouTube-Videos fest.
2. Drücken Sie F5, und spielen Sie den Clip durch Klicken oder Tippen auf die Wiedergabeschaltfläche des **Video**-Steuerelements ab.
3. Drücken Sie die ESC-TASTE, um zum Standardarbeitsbereich zurückzukehren.

### <a name="play-a-video-from-azure-media-services"></a>Abspielen eines Videos aus Azure Media Services
1. Nachdem die Videos auf AMS veröffentlicht wurden, kopieren Sie die URL der Manifestdatei. Starten Sie den Streamingendpunkt Ihres Diensts, falls noch nicht geschehen.
1. Fügen Sie ein **Video**-Steuerelement hinzu, und legen Sie die **Media**-Eigenschaft auf die URL (in doppelten Anführungszeichen) eines AMS-Videos fest.
2. Drücken Sie F5, und spielen Sie den Clip durch Klicken oder Tippen auf die Wiedergabeschaltfläche des **Video**-Steuerelements ab.
3. Drücken Sie die ESC-TASTE, um zum Standardarbeitsbereich zurückzukehren.


## <a name="accessibility-guidelines"></a>Richtlinien für Barrierefreiheit
### <a name="audio-and-video-alternatives"></a>Alternativen zu Audio- und Videodateien
* **ShowControls** muss auf TRUE festgelegt sein, sodass Benutzer Multimediadateien in ihrem eigenen Tempo hören oder ansehen können. Damit können Benutzer auch Untertitel und den Vollbildmodus in Videoplayern aktivieren bzw. deaktivieren.
* Untertitel müssen für alle Videos bereitgestellt werden.
  *  Für YouTube-Videos können Sie dazu von YouTube bereitgestellte Tools verwenden.
  *  Für andere Videos können Sie Untertitel im WebVTT Format erstellen und hochladen und **ClosedCaptionsUrl** auf den URL-Speicherort festlegen. Es gibt jedoch einige Einschränkungen. Die Server, die die Videos und Untertitel hosten, müssen CORS-fähig sein und diese über das HTTPS-Protokoll übertragen. Untertitel funktionieren außerdem nicht in Internet Explorer.
* Sie können auch ein Audio- oder Videotranskript mithilfe einer der folgenden Methoden bereitstellen:
  1. Platzieren Sie den Text in einer **[Bezeichnung](control-text-box.md)** , und positionieren Sie ihn neben dem Multimedia-Player. Erstellen Sie optional eine **[Schaltfläche](control-button.md)** , um die Textanzeige umzuschalten.
  2. Platzieren Sie den Text in einem anderen Bildschirm. Erstellen Sie eine **[Schaltfläche](control-button.md)** , die auf diesen Bildschirm weiterleitet, und positionieren Sie die Schaltfläche neben dem Multimedia-Player.
  3. Wenn die Beschreibung kurz ist, kann sie in **[AccessibleLabel](properties-accessibility.md)** eingegeben werden.

### <a name="color-contrast"></a>Farbkontrast
Zwischen den folgenden Eigenschaften muss es einen ausreichenden Farbkontrast geben:
* **[FocusedBorderColor](properties-color-border.md)** und die äußere Farbe
* **[Bild](properties-visual.md)** und dem Multimedia-Player-Steuerelement (falls zutreffend)
* **[Fill](properties-color-border.md)** (Füllfarbe) und dem Multimedia-Player-Steuerelement (falls zutreffend)

Stellen Sie Untertitel und/oder Transkripte bereit, wenn der Videoinhalt Probleme mit dem Farbkontrast aufweist.

### <a name="screen-reader-support"></a>Unterstützung der Sprachausgabe
* **[AccessibleLabel](properties-accessibility.md)** muss vorhanden sein.

### <a name="keyboard-support"></a>Tastaturunterstützung
* **[TabIndex](properties-accessibility.md)** muss gleich 0 (null) oder größer sein, damit Tastaturbenutzer dorthin navigieren können.
* Fokusindikatoren müssen deutlich sichtbar sein. Mithilfe von **[FocusedBorderColor](properties-color-border.md)** und **[FocusedBorderThickness](properties-color-border.md)** können Sie dies archivieren.
* **AutoStart** sollte FALSE sein, da es für Tastaturbenutzer schwierig sein kann, die Wiedergabe schnell zu beenden.
