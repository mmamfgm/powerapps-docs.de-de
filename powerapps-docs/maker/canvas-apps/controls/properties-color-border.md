---
title: Farb- und Rahmeneigenschaften | Microsoft-Dokumentation
description: Enthält Referenzinformationen zu Eigenschaften wie „BorderColor“, „HoverBorderColor“ und „PressedBorderColor“.
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 10/25/2016
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 528dc54fe18971ff8971b4d0d7e87c3bf3c5367a
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/07/2019
ms.locfileid: "71986021"
---
# <a name="color-and-border-properties-in-powerapps"></a>Farb- und Rahmeneigenschaften in PowerApps

## <a name="overview"></a>Übersicht

Konfigurieren Sie den Stil eines Steuerelements in Abhängigkeit davon, wie der Benutzer damit interagiert.

Sie können Farben in vielerlei Hinsicht angeben:

- [**Farbenumeration**](../functions/function-colors.md) : Geben Sie die Farbnamen aus Cascading Stylesheets an, wie in den folgenden Beispielen:

  - **Color.Red**
  - **Color.Indigo**

- [**ColorValue**](../functions/function-colors.md) -Funktion: Geben Sie Text Zeichenfolgen wie z. b. Farbnamen aus Cascading Stylesheets und Hex-Code Notation ( **#** ) an, wie in den folgenden Beispielen:

  - **ColorValue ("AliceBlue")**
  - **ColorValue( "#ff00ff" )**

- [**Colorfade**](../functions/function-colors.md) -Funktion: Geben Sie an, wie eine Farbe ausgeblendet ist, von vollständig schwarz (-100%). vollständig weiß (100%), wie in diesem Beispiel:

  - **Colorfade (Color. Red, 50%)**

- [**RGBA**](../functions/function-colors.md) -Funktion: Geben Sie die roten, grünen und blauen Komponenten einer Farbe zwischen 0 und 255 an, und geben Sie einen Alphakanal zwischen 0% (vollständig transparent) und 100% (vollständig deckend) an, wie in diesem Beispiel:

  - **RGBA (255, 0, 255, 25%)**

Farbeigenschaften können auch auf andere Farbeigenschaften verweisen. Beispielsweise kann **Label. pressedcolor** auf die Formel **Label1. Color**festgelegt werden, wobei eine Änderung von einer Eigenschaft in eine andere automatisch kaskadiert wird.

## <a name="normal"></a>Normal

Diese Eigenschaften gelten normalerweise, wenn der Benutzer nicht mit dem Steuerelement interagiert.

**BorderColor**: Die Farbe des Rahmens eines Steuerelements.

- Gilt für Steuerelemente des folgenden Typs: **[Bild hinzufügen](control-add-picture.md)** , **[Audio](control-audio-video.md)** , **[Schaltfläche](control-button.md)** , **[Kamera](control-camera.md)** , **[Karte](control-card.md)** , **[Kontrollkästchen](control-check-box.md)** , **[Säulendiagramm](control-column-line-chart.md)** , **[Datumsauswahl](control-date-picker.md)** , **[Anzeigeformular](control-form-detail.md)** , **[Dropdown](control-drop-down.md)** , **[Bearbeitungsformular](control-form-detail.md)** , **[Export](control-export-import.md)** , **[Katalog](control-gallery.md)** , **[HTML-Text](control-html-text.md)** , **[Bild](control-image.md)** , **[Import](control-export-import.md)** , **[Bezeichnung](control-text-box.md)** , **[Liniendiagramm](control-column-line-chart.md)** , **[Listenfeld](control-list-box.md)** , **[Mikrofon](control-microphone.md)** , **[PDF-Viewer](control-pdf-viewer.md)** , **[Stifteingabe](control-pen-input.md)** , **[Kreisdiagramm](control-pie-chart.md)** , **[Optionsfeld](control-radio.md)** , **[Bewertung](control-rating.md)** , **[Schieberegler](control-slider.md)** , **[Texteingabe](control-text-input.md)** , **[Timer](control-timer.md)** , **[Umschalten](control-toggle.md)** und **[Video](control-audio-video.md)** .

**BorderStyle**: Legt fest, ob der Rahmen eines Steuerelements **Solid** (Durchgehend), **Dashed** (Gestrichelt), **Dotted** (Gepunktet) oder **None** (Keiner) ist.

- Gilt für Steuerelemente des folgenden Typs: **[Bild hinzufügen](control-add-picture.md)** , **[Audio](control-audio-video.md)** , **[Schaltfläche](control-button.md)** , **[Kamera](control-camera.md)** , **[Karte](control-card.md)** , **[Kontrollkästchen](control-check-box.md)** , **[Säulendiagramm](control-column-line-chart.md)** , **[Datumsauswahl](control-date-picker.md)** , **[Anzeigeformular](control-form-detail.md)** , **[Dropdown](control-drop-down.md)** , **[Bearbeitungsformular](control-form-detail.md)** , **[Export](control-export-import.md)** , **[Katalog](control-gallery.md)** , **[HTML-Text](control-html-text.md)** , **[Bild](control-image.md)** , **[Import](control-export-import.md)** , **[Bezeichnung](control-text-box.md)** , **[Liniendiagramm](control-column-line-chart.md)** , **[Listenfeld](control-list-box.md)** , **[Mikrofon](control-microphone.md)** , **[PDF-Viewer](control-pdf-viewer.md)** , **[Stifteingabe](control-pen-input.md)** , **[Kreisdiagramm](control-pie-chart.md)** , **[Optionsfeld](control-radio.md)** , **[Bewertung](control-rating.md)** , **[Schieberegler](control-slider.md)** , **[Texteingabe](control-text-input.md)** , **[Timer](control-timer.md)** , **[Umschalten](control-toggle.md)** und **[Video](control-audio-video.md)** .

**BorderThickness**: Die Linienstärke des Rahmens eines Steuerelements.

- Gilt für Steuerelemente des folgenden Typs: **[Bild hinzufügen](control-add-picture.md)** , **[Audio](control-audio-video.md)** , **[Schaltfläche](control-button.md)** , **[Kamera](control-camera.md)** , **[Karte](control-card.md)** , **[Kontrollkästchen](control-check-box.md)** , **[Säulendiagramm](control-column-line-chart.md)** , **[Datumsauswahl](control-date-picker.md)** , **[Anzeigeformular](control-form-detail.md)** , **[Dropdown](control-drop-down.md)** , **[Bearbeitungsformular](control-form-detail.md)** , **[Export](control-export-import.md)** , **[Katalog](control-gallery.md)** , **[HTML-Text](control-html-text.md)** , **[Bild](control-image.md)** , **[Import](control-export-import.md)** , **[Bezeichnung](control-text-box.md)** , **[Liniendiagramm](control-column-line-chart.md)** , **[Listenfeld](control-list-box.md)** , **[Mikrofon](control-microphone.md)** , **[PDF-Viewer](control-pdf-viewer.md)** , **[Stifteingabe](control-pen-input.md)** , **[Kreisdiagramm](control-pie-chart.md)** , **[Optionsfeld](control-radio.md)** , **[Bewertung](control-rating.md)** , **[Schieberegler](control-slider.md)** , **[Texteingabe](control-text-input.md)** , **[Timer](control-timer.md)** , **[Umschalten](control-toggle.md)** und **[Video](control-audio-video.md)** .

**Color**: Die Farbe des Texts in einem Steuerelement.

- Gilt für Steuerelemente des folgenden Typs: **[Bild hinzufügen](control-add-picture.md)** , **[Schaltfläche](control-button.md)** , **[Kontrollkästchen](control-check-box.md)** , **[Säulendiagramm](control-column-line-chart.md)** , **[Datumsauswahl](control-date-picker.md)** , **[Dropdown](control-drop-down.md)** , **[Export](control-export-import.md)** , **[HTML-Text](control-html-text.md)** , **[Import](control-export-import.md)** , **[Bezeichnung](control-text-box.md)** , **[Liniendiagramm](control-column-line-chart.md)** , **[Listenfeld](control-list-box.md)** , **[Mikrofon](control-microphone.md)** , **[Stifteingabe](control-pen-input.md)** , **[Kreisdiagramm](control-pie-chart.md)** , **[Optionsfeld](control-radio.md)** , **[Texteingabe](control-text-input.md)** und **[Timer](control-timer.md)** .

**Fill**: Die Hintergrundfarbe eines Steuerelements.

- Gilt für Steuerelemente des folgenden Typs: **[Bild hinzufügen](control-add-picture.md)** , **[Audio](control-audio-video.md)** , **[Schaltfläche](control-button.md)** , **[Karte](control-card.md)** , **[Kontrollkästchen](control-check-box.md)** , **[Datumsauswahl](control-date-picker.md)** , **[Anzeigeformular](control-form-detail.md)** , **[Dropdown](control-drop-down.md)** , **[Bearbeitungsformular](control-form-detail.md)** , **[Export](control-export-import.md)** , **[Katalog](control-gallery.md)** , **[HTML-Text](control-html-text.md)** , **[Symbol](control-shapes-icons.md)** , **[Bild](control-image.md)** , **[Import](control-export-import.md)** , **[Bezeichnung](control-text-box.md)** , **[Listenfeld](control-list-box.md)** , **[Mikrofon](control-microphone.md)** , **[PDF-Viewer](control-pdf-viewer.md)** , **[Stifteingabe](control-pen-input.md)** , **[Optionsfeld](control-radio.md)** , **[Bewertung](control-rating.md)** , **[Bildschirm](control-screen.md)** , **[Form](control-shapes-icons.md)** , **[Texteingabe](control-text-input.md)** , **[Timer](control-timer.md)** , **[Umschalten](control-toggle.md)** und **[Video](control-audio-video.md)** .

## <a name="focused"></a>Fokus

Diese Eigenschaften sind wirksam, wenn das Steuerelement der Fokus ist.

**FocusedBorderColor**: die Rahmenfarbe eines Steuerelements, wenn dieses der Fokus ist.

**FocusedBorderThickness**: die Stärke des Rahmen eines Steuerelements, wenn es den Fokus hat.

- Diese Eigenschaften gelten für die Steuerelemente **[Bild hinzufügen](control-add-picture.md)** , **[Anlagen](control-attachments.md)** , **[Audio](control-audio-video.md)** , **[Schaltfläche](control-button.md)** , **[Kamera](control-camera.md)** , **[Kontrollkästchen](control-check-box.md)** , **[Kombinationsfeld](control-combo-box.md)** , **[Datumsauswahl](control-date-picker.md)** , **[Dropdown](control-drop-down.md)** , **[Export](control-export-import.md)** , **[Katalog](control-gallery.md)** , **[Symbol](control-shapes-icons.md)** , **[Bild](control-image.md)** , **[Import](control-export-import.md)** , **[Bezeichnung](control-text-box.md)** , **[Listenfeld](control-list-box.md)** , **[Mikrofon](control-microphone.md)** , **[Radio](control-radio.md)** , **[Bewertung](control-rating.md)** , **[Form](control-shapes-icons.md)** , **[Schieberegler](control-slider.md)** , **[Texteingabe](control-text-input.md)** , **[Timer](control-timer.md)** , **[Schalter](control-toggle.md)** und **[Video](control-audio-video.md)** .

## <a name="disabled"></a>Deaktiviert

Diese Eigenschaften sind wirksam, wenn das Steuerelement deaktiviert ist.  Ein Steuerelement kann deaktiviert werden, indem die **[Disabled](properties-core.md)** -Eigenschaft auf *true* festgelegt wird.

**DisabledBorderColor**: Die Farbe des Steuerelementrahmens, wenn die **[DisplayMode](properties-core.md)** -Eigenschaft des Steuerelements auf **Disabled** (Deaktiviert) festgelegt ist.

- Gilt für Steuerelemente des folgenden Typs: **[Bild hinzufügen](control-add-picture.md)** , **[Schaltfläche](control-button.md)** , **[Kontrollkästchen](control-check-box.md)** , **[Säulendiagramm](control-column-line-chart.md)** , **[Datumsauswahl](control-date-picker.md)** , **[Dropdown](control-drop-down.md)** , **[Export](control-export-import.md)** , **[HTML-Text](control-html-text.md)** , **[Bild](control-image.md)** , **[Import](control-export-import.md)** , **[Bezeichnung](control-text-box.md)** , **[Liniendiagramm](control-column-line-chart.md)** , **[Listenfeld](control-list-box.md)** , **[Mikrofon](control-microphone.md)** , **[PDF-Viewer](control-pdf-viewer.md)** , **[Kreisdiagramm](control-pie-chart.md)** , **[Optionsfeld](control-radio.md)** , **[Schieberegler](control-slider.md)** , **[Texteingabe](control-text-input.md)** , **[Timer](control-timer.md)** und **[Umschalten](control-toggle.md)** .

**DisabledColor**: Die Farbe des Texts in einem Steuerelement, wenn seine **[DisplayMode](properties-core.md)** -Eigenschaft auf **Disabled** (Deaktiviert) festgelegt ist.

- Gilt für Steuerelemente des folgenden Typs: **[Bild hinzufügen](control-add-picture.md)** , **[Schaltfläche](control-button.md)** , **[Kontrollkästchen](control-check-box.md)** , **[Datumsauswahl](control-date-picker.md)** , **[Dropdown](control-drop-down.md)** , **[Export](control-export-import.md)** , **[Import](control-export-import.md)** , **[Bezeichnung](control-text-box.md)** , **[Listenfeld](control-list-box.md)** , **[Mikrofon](control-microphone.md)** , **[Optionsfeld](control-radio.md)** , **[Texteingabe](control-text-input.md)** und **[Timer](control-timer.md)** .

**DisabledFill**: Die Hintergrundfarbe eines Steuerelements, wenn dessen **[DisplayMode](properties-core.md)** -Eigenschaft auf **Disabled** (Deaktiviert) festgelegt ist.

- Gilt für Steuerelemente des folgenden Typs: **[Bild hinzufügen](control-add-picture.md)** , **[Schaltfläche](control-button.md)** , **[Kontrollkästchen](control-check-box.md)** , **[Datumsauswahl](control-date-picker.md)** , **[Dropdown](control-drop-down.md)** , **[Export](control-export-import.md)** , **[HTML-Text](control-html-text.md)** , **[Bild](control-image.md)** , **[Import](control-export-import.md)** , **[Bezeichnung](control-text-box.md)** , **[Listenfeld](control-list-box.md)** , **[Mikrofon](control-microphone.md)** , **[Optionsfeld](control-radio.md)** , **[Texteingabe](control-text-input.md)** und **[Timer](control-timer.md)** .

## <a name="hover"></a>Daraufzeigen

Diese Eigenschaften sind wirksam, wenn der Benutzer mit der Maus auf das Steuerelement zeigt.

**HoverBorderColor**: Die Rahmenfarbe eines Steuerelements, wenn der Benutzer den Mauszeiger auf das Steuerelement bewegt.

- Gilt für Steuerelemente des folgenden Typs: **[Bild hinzufügen](control-add-picture.md)** , **[Schaltfläche](control-button.md)** , **[Kontrollkästchen](control-check-box.md)** , **[Säulendiagramm](control-column-line-chart.md)** , **[Dropdown](control-drop-down.md)** , **[Export](control-export-import.md)** , **[HTML-Text](control-html-text.md)** , **[Bild](control-image.md)** , **[Import](control-export-import.md)** , **[Bezeichnung](control-text-box.md)** , **[Liniendiagramm](control-column-line-chart.md)** , **[Listenfeld](control-list-box.md)** , **[Mikrofon](control-microphone.md)** , **[PDF-Viewer](control-pdf-viewer.md)** , **[Kreisdiagramm](control-pie-chart.md)** , **[Schieberegler](control-slider.md)** , **[Texteingabe](control-text-input.md)** , **[Timer](control-timer.md)** und **[Umschalten](control-toggle.md)** .

**HoverColor**: Die Farbe des Texts in einem Steuerelement, wenn der Benutzer mit der Maus darauf zeigt.

- Gilt für Steuerelemente des folgenden Typs: **[Bild hinzufügen](control-add-picture.md)** , **[Schaltfläche](control-button.md)** , **[Kontrollkästchen](control-check-box.md)** , **[Dropdown](control-drop-down.md)** , **[Export](control-export-import.md)** , **[Import](control-export-import.md)** , **[Bezeichnung](control-text-box.md)** , **[Listenfeld](control-list-box.md)** , **[Mikrofon](control-microphone.md)** , **[Optionsfeld](control-radio.md)** , **[Texteingabe](control-text-input.md)** und **[Timer](control-timer.md)** .

**HoverFill**: Die Hintergrundfarbe eines Steuerelements, wenn der Benutzer mit der Maus darauf zeigt.

- Gilt für Steuerelemente des folgenden Typs: **[Bild hinzufügen](control-add-picture.md)** , **[Schaltfläche](control-button.md)** , **[Kontrollkästchen](control-check-box.md)** , **[Dropdown](control-drop-down.md)** , **[Export](control-export-import.md)** , **[Symbol](control-shapes-icons.md)** , **[Bild](control-image.md)** , **[Import](control-export-import.md)** , **[Bezeichnung](control-text-box.md)** , **[Listenfeld](control-list-box.md)** , **[Mikrofon](control-microphone.md)** , **[Optionsfeld](control-radio.md)** , **[Form](control-shapes-icons.md)** , **[Texteingabe](control-text-input.md)** und **[Timer](control-timer.md)** .

## <a name="pressed"></a>Gedrückt

Diese Eigenschaften sind wirksam, wenn eine Schaltfläche oder ein Bildsteuerelement betätigt wird.

**PressedBorderColor**: Die Rahmenfarbe eines Steuerelements, wenn der Benutzer auf das Steuerelement tippt oder klickt.

- Gilt für Steuerelemente des folgenden Typs: **[Bild hinzufügen](control-add-picture.md)** , **[Schaltfläche](control-button.md)** , **[Kontrollkästchen](control-check-box.md)** , **[Säulendiagramm](control-column-line-chart.md)** , **[Dropdown](control-drop-down.md)** , **[Export](control-export-import.md)** , **[Symbol](control-shapes-icons.md)** , **[Bild](control-image.md)** , **[Import](control-export-import.md)** , **[Bezeichnung](control-text-box.md)** , **[Liniendiagramm](control-column-line-chart.md)** , **[Listenfeld](control-list-box.md)** , **[Mikrofon](control-microphone.md)** , **[PDF-Viewer](control-pdf-viewer.md)** , **[Kreisdiagramm](control-pie-chart.md)** , **[Form](control-shapes-icons.md)** , **[Schieberegler](control-slider.md)** , **[Texteingabe](control-text-input.md)** , **[Timer](control-timer.md)** und **[Umschalten](control-toggle.md)** .

**PressedColor**: Die Farbe des Texts in einem Steuerelement, wenn der Benutzer auf das Steuerelement tippt oder klickt.

- Gilt für Steuerelemente des folgenden Typs: **[Bild hinzufügen](control-add-picture.md)** , **[Schaltfläche](control-button.md)** , **[Kontrollkästchen](control-check-box.md)** , **[Dropdown](control-drop-down.md)** , **[Export](control-export-import.md)** , **[Import](control-export-import.md)** , **[Bezeichnung](control-text-box.md)** , **[Listenfeld](control-list-box.md)** , **[Mikrofon](control-microphone.md)** , **[Optionsfeld](control-radio.md)** , **[Texteingabe](control-text-input.md)** und **[Timer](control-timer.md)** .

**PressedFill**: Die Hintergrundfarbe eines Steuerelements, wenn der Benutzer auf das Steuerelement tippt oder klickt.

- Gilt für Steuerelemente des folgenden Typs: **[Bild hinzufügen](control-add-picture.md)** , **[Schaltfläche](control-button.md)** , **[Kontrollkästchen](control-check-box.md)** , **[Dropdown](control-drop-down.md)** , **[Export](control-export-import.md)** , **[Bild](control-image.md)** , **[Import](control-export-import.md)** , **[Bezeichnung](control-text-box.md)** , **[Listenfeld](control-list-box.md)** , **[Mikrofon](control-microphone.md)** , **[Optionsfeld](control-radio.md)** , **[Texteingabe](control-text-input.md)** und **[Timer](control-timer.md)** .

## <a name="selection"></a>Auswahl

Diese Eigenschaften sind wirksam, wenn der Benutzer ein Element in einem Steuerelement auswählt.

**SelectionColor**: Die Textfarbe des ausgewählten Elements oder der Elemente in einer Liste oder die Farbe des Auswahltools in einem Stift-Steuerelement.

- Gilt für Steuerelemente des folgenden Typs: **[Dropdown](control-drop-down.md)** , **[Listenfeld](control-list-box.md)** und **[Stifteingabe](control-pen-input.md)** .

**SelectionFill**: Die Hintergrundfarbe des ausgewählten Elements oder der Elemente in einer Liste oder eines ausgewählten Bereichs eines Stift-Steuerelements.

- Gilt für Steuerelemente des folgenden Typs: **[Dropdown](control-drop-down.md)** und **[Listenfeld](control-list-box.md)** .