---
title: Funktion „GUID“ | Microsoft-Dokumentation
description: Referenzinformationen einschließlich Syntax für die Funktion „GUID“ in PowerApps
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 11/14/2018
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: ea2668ca295d807bbc19f71c9aa9f477c3b96041
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/07/2019
ms.locfileid: "71992688"
ms.PowerAppsDecimalTransform: true
---
# <a name="guid-function-in-powerapps"></a>Funktion „GUID“ in PowerApps
Konvertiert eine GUID-Zeichenfolge ([Globally Unique Identifier](https://en.wikipedia.org/wiki/Universally_unique_identifier), global eindeutiger Bezeichner) in einen GUID-Wert oder erstellt einen neuen GUID-Wert.

## <a name="description"></a>Beschreibung
Verwenden Sie die **GUID**-Funktion, um eine Zeichenfolge, die die hexadezimale Darstellung einer GUID enthält, in einen GUID-Wert zu konvertieren, der an eine Datenbank übergeben werden kann. GUID-Werte werden als Schlüssel von Datenbanksystemen wie Common Data Service und SQL Server verwendet.

Die übergebene Zeichenfolge kann Groß- oder Kleinbuchstaben enthalten, muss aber aus 32 Hexadezimalziffern in einem der folgenden Formate bestehen:

- **"123e4567-e89b-12d3-a456-426655440000"** (Bindestriche an Standardpositionen)
- **"123e4567e89b12d3a456426655440000"** (keine Bindestriche)

Wenn Sie kein Argument angeben, erstellt diese Funktion eine neue GUID.

Um einen GUID-Wert in eine Zeichenfolge zu konvertieren, verwenden Sie ihn einfach in einem Zeichenfolgenkontext. Der GUID-Wert wird in eine hexadezimale Darstellungszeichenfolge mit Bindestrichen und Kleinbuchstaben konvertiert. 

Beim Erstellen einer neuen GUID verwendet diese Funktion Pseudozufallszahlen, um eine Version 4 [IETF RFC 4122](https://www.ietf.org/rfc/rfc4122.txt) -GUID zu erstellen. Wenn eine Zeichenfolge in eine GUID umgerechnet wird, unterstützt diese Funktion jede GUID-Version, indem Sie eine beliebige Zeichenfolge mit hexadezimalen Ziffern von 32 akzeptiert

## <a name="volatile-functions"></a>Veränderliche Funktionen
**GUID** ist eine veränderliche Funktion, wenn sie ohne Argument verwendet wird. Die Funktion gibt bei jeder Auswertung einen anderen Wert zurück.  

Wird eine veränderliche Funktion in einer Datenflussformel verwendet, gibt sie nur dann einen anderen Wert zurück, wenn die Formel, in der sie vorkommt, erneut ausgewertet wird. Wenn nichts in der Formel geändert wird, bleibt der Wert während der Ausführung der App gleich.

Ein Beispiel: Ein Bezeichnungssteuerelement, für das die **Text**-Eigenschaft auf **GUID()** festgelegt ist, ändert sich nicht, solange Ihre App aktiv ist. Nur das Schließen und erneute Öffnen der App führt zu einem anderen Wert.

Die Funktion wird neu ausgewertet, wenn sie Teil einer Formel ist, in der sich etwas anderes geändert hat. Wenn Sie die **Text**-Eigenschaft eines **Label**-Steuerelements auf die folgende Formel festlegen, wird die GUID jedes Mal generiert, wenn ein Benutzer den Wert des **Text input**-Steuerelements ändert:

**TextInput1.Text & " " & GUID()**

Bei der Verwendung in einer [Verhaltensformel](../working-with-formulas-in-depth.md) wird **GUID** immer zusammen mit der Formel ausgewertet. Weitere Informationen finden Sie bei den Beispielen weiter unten in diesem Thema.

## <a name="syntax"></a>Syntax
**GUID**( [ *GUIDString* ] )

* *GUIDString*: Optional.  Eine Textzeichenfolge, die die hexadezimale Darstellung einer GUID enthält. Wenn keine Zeichenfolge bereitgestellt wird, wird eine neue GUID erstellt.

## <a name="examples"></a>Beispiele

#### <a name="basic-usage"></a>Grundlegende Nutzung

So geben Sie einen GUID-Wert basierend auf der hexadezimalen Zeichenfolgendarstellung zurück:

* **GUID( "0f8fad5b-d9cb-469f-a165-70867728950e" )**

Sie können die GUID-Zeichenfolge auch ohne Bindestriche angeben. Diese Formel gibt den gleichen GUID-Wert zurück:

* **GUID( "0f8fad5bd9cb469fa16570867728950e" )**

Um in diesem Kontext das Feld **Status** eines neuen Datenbankdatensatzes auf einen bekannten Wert festzulegen, verwenden Sie Folgendes:

* Patch für **(Produkte; Standard (Produkte); {Status: GUID ("F9168C5E-CEB2-4faa-B6BF-329BF39FA1E4")})**

Sie werden die GUIDs vermutlich für Ihre Benutzer nicht sichtbar machen, aber GUIDs können Ihnen beim Debuggen Ihrer App helfen. Um den Wert des **Status**-Felds in dem Datensatz anzuzeigen, den Sie im vorherigen Beispiel erstellt haben, legen Sie die **Text**-Eigenschaft eines **Label**-Steuerelements auf diese Formel fest:

* **First( Products ).Status**

Das **Label**-Steuerelement zeigt **f9168c5e-ceb2-4faa-b6bf-329bf39fa1e4** an.

#### <a name="create-a-table-of-guids"></a>Erstellen einer Tabelle mit GUIDs

1. Legen Sie die Eigenschaft **[OnSelect](../controls/properties-core.md)** eines **[Button](../controls/control-button.md)** -Steuerelements auf die folgende Formel fest:

    **ClearCollect( NewGUIDs; ForAll( [ 1; 2; 3; 4; 5 ]; GUID() ) )**

    Diese Formel erstellt eine Tabelle mit einer Spalte, die fünfmal durchlaufen wird. Das Ergebnis sind fünf GUIDs.

1. Fügen Sie ein **[Data table](../controls/control-data-table.md)** -Steuerelement hinzu, legen Sie deren **Items**-Eigenschaft auf **NewGUIDs** fest, und zeigen Sie das Feld **Value** an.

1. Klicken oder tippen Sie auf die Schaltfläche, während Sie die ALT-TASTE gedrückt halten.

    Die Datentabelle zeigt eine Liste mit GUIDs:

    ![Bildschirm mit einer Datentabelle mit fünf verschiedenen GUID-Werten](media/function-guid/guid-collection-1.png)

1. Klicken Sie noch einmal auf die Schaltfläche, um eine andere Liste von GUIDs anzuzeigen:

    ![Der gleiche Bildschirm mit einer Datentabelle mit einem neuen Satz aus fünf verschiedenen GUID-Werten](media/function-guid/guid-collection-2.png)

Um eine einzelne GUID anstelle einer Tabelle zu generieren, verwenden Sie diese Formel:

**Set( NewGUID; GUID() )**
