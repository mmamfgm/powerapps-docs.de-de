---
title: Integrieren von globaler Unterstützung in Canvas-Apps | Microsoft-Dokumentation
description: Verwenden Sie PowerApps, um Apps zu erstellen, die weltweit verwendet werden.
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 10/25/2016
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 8df786dfea77849f41992c704d69d214df73d13a
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/07/2019
ms.locfileid: "71983255"
ms.PowerAppsDecimalTransform: true
---
# <a name="build-global-support-into-canvas-apps"></a>Integrieren von globaler Unterstützung in Canvas-Apps
PowerApps ist ein globales Produkt. Sie können Canvas-Apps in vielen verschiedenen Sprachen und Regionen erstellen und verwenden.

Sowohl beim Erstellen als auch beim Ausführen von Apps wurde der von PowerApps angezeigte Text in eine Vielzahl von Sprachen übersetzt.  Menüelemente, Dialogfelder, Menübandregisterkarten und anderer Text wird in Ihrer Muttersprache angezeigt.  Die Eingabe und die Datums- und Zahlenanzeige ist ebenfalls an Ihre bestimmte Sprache und Region angepasst.  Beispielsweise wird in einigen Regionen der Welt ein verwendet **.** (Punkt oder Punkt) als Dezimaltrennzeichen, während andere einen **,** (Komma) verwenden.  

Die Apps, die Sie erstellen, können ebenfalls global kompatibel sein.  Verwenden Sie die Funktionen **[Language](functions/function-language.md)** , **[Text](functions/function-text.md)** , **[Value](functions/function-value.md)** , **[DateValue](functions/function-datevalue-timevalue.md)** sowie andere Funktionen, um anzupassen, was als Eingabe in verschiedenen Sprachen angezeigt und verwendet wird.   

## <a name="language-settings"></a>Spracheinstellungen
Wenn Sie ein natives Studio oder einen nativen Spieler verwenden, wird die verwendete Sprache vom Hostbetriebssystem bereitgestellt.  Bei Windows kann dies unter „Alle Einstellungen“ und dann unter den Einstellungen für „Zeit & Sprache“ gesteuert werden.  Windows ermöglicht Ihnen auch, die Zeichen anzugeben, die als Dezimalzeichen verwendet werden sollen, wobei die Spracheinstellungen überschrieben werden.  

Bei Verwendung der Webbenutzeroberfläche wird die verwendete Sprache vom Browser bereitgestellt.  Die meisten Browser übernehmen standardmäßig die Einstellung des Hostbetriebssystems, wobei einige auch die Möglichkeit bieten, die Sprache manuell festzulegen.

## <a name="authoring-environment"></a>Erstellungsumgebung
Die Erstellungsumgebung passt sich an die Spracheinstellung des Autors an.  Die App selbst wird auf eine sprachunabhängige Weise gespeichert, sodass Autoren, die verschiedene Sprachen verwenden, die gleiche App bearbeiten können.

### <a name="names-in-formulas"></a>Namen in Formeln
Die meisten Elemente in einer Formel sind immer auf Englisch:

* Funktionsnamen: **If**, **Navigate**, **Collect**,...
* Eigenschaften Namen für Steuerelemente: **Screen. Fill**, **Button. onselect**, **TextBox. Font**,...
* Enumerationsnamen: **Color. Aqua**, **DataSourceInfo. MaxValue**, **FontWeight. Bold**...
* Signal Datensätze: **Compass. Überschrift**,  **Location. Latitude**, **App.ActiveScreen**, ...
* Veranstalter **Parent**, **in**, **exactin**,...

Da die Erstellungsumgebung lokalisiert wird, werden Steuer- und andere Objektnamen in der Muttersprache des Autors angezeigt.  In Spanisch werden einige der Steuerelementnamen wie folgt angezeigt:

![](media/global-apps/insert-controls-es.png)

Wenn Sie eines dieser Steuerelemente in Ihre App einfügen, wird dessen Name standardmäßig auf Englisch angezeigt.  Dies geschieht aus Gründen der Konsistenz zwischen den Namen der Steuerelementeigenschaften und dem Rest der Formel.  Beispielsweise wird das oben aufgeführte **Casilla** als **Checkbox1** eingefügt.  

Nach dem Einfügen eines Steuerelements können Sie den Namen beliebig ändern.  Solange es ausgewählt ist, zeigt der ganz linke Teil des Menübands „Content“ (Inhalt) den Namen des Steuerelements an.  Wenn Sie diesen Namen auswählen, wird ein Textfeld angezeigt, in dem Sie den Namen bearbeiten können:

![](media/global-apps/control-rename.png)

Wenn Sie möchten, können Sie hier das Steuerelement in **Casilla1** umbenennen.  Die rote Wellenlinie, die in diesem Fall von einem Browser angezeigt wird, ist darauf zurückzuführen, dass es sich bei dem Wort nicht um ein spanisches Wort handelt, und ist nicht zu beachten.

Sie können beliebige Namen für folgende Namen verwenden:

* Steuerelementnamen
* Sammlungsnamen
* Namen von Kontextvariablen

### <a name="formula-separators-and-chaining-operator"></a>Formeltrennzeichen und Verkettungsoperator
Einige [Trennzeichen und Operatoren](functions/operators.md) werden basierend auf dem Dezimaltrennzeichen der Sprache des Autors verschoben:

| Dezimaltrennzeichen der Sprache des Autors | Dezimaltrennzeichen von PowerApps | Listentrennzeichen von PowerApps | Verkettungsoperator von PowerApps |
| --- | --- | --- | --- |
| **.** (Punkt oder Punkt) |**.** (Punkt oder Punkt) |**,** (Komma) |**;** (Semikolon) |
| **,** (Komma) |**,** (Komma) |**;** (Semikolon) |**;;** (doppeltes Semikolon) |

Die Änderung im powerapps-Listen Trennzeichen ist konsistent mit dem Trennzeichen für Excel-Listen Trennzeichen.  Sie wirkt sich auf Folgendes aus:

* Argumente in Funktionsaufrufen
* Felder in einem [Datensatz](working-with-tables.md#elements-of-a-table)
* Datensätze in einer [Tabelle](working-with-tables.md#inline-value-tables).

Sehen Sie sich z. b. die folgende Formel in einer Sprache und einer Region an, die einen Punkt oder einen Punkt als Dezimaltrennzeichen verwendet, z. b. Japan oder das Vereinigte Königreich:

![Powerapps-Formel bei öffnenden Parametern slider1 Punktwert größer als 12 Punkt 59 Komma Benachrichtigen Open-Parser "gültig!" Kommas: Schließen Sie die Semikolon-Navigation mit einem Semikolon, öffnen Sie "nextScreen", "nextScreen", wenn die Meldung "Fehler bei öffnenden öffnenden Parametern schließen"](media/global-apps/operators-dot.png)

Sehen Sie sich nun dieselbe Formel in einer Sprache und Region an, in der ein Komma für das Dezimaltrennzeichen verwendet wird, z. b. Frankreich oder Spanien:

![Powerapps-Formel bei öffnenden Parametern slider1 Punktwert größer als 12 Komma 59 Semikolon Benachrichtigungs öffnende Parser "gültig!" Semikolon Success Close, Double Semikolon Navigate Open Parser "nextScreen" Semikola None close Semikolon notify Open Parser "Invalid, try again" Semikolon Error close Parser close para.](media/global-apps/operators-comma.png)

Die Hervorhebung zeigt die Operatoren, die sich zwischen den beiden Versionen ändern.  Beachten Sie, dass der Eigenschaftenauswahloperator **.** (Punkt oder Punkt) in **Slider1. der Wert** ist immer gleich, unabhängig davon, was das Dezimaltrennzeichen ist.

Intern wird die Formel nicht geändert; es wird nur geändert, wie diese vom Autor angezeigt und bearbeitet wird.  Zwei verschiedene Autoren, die zwei verschiedene Sprachen verwenden, können die gleiche Formel anzeigen und bearbeiten, wobei jedem die für seine Sprache entsprechenden Trennzeichen und Operatoren angezeigt werden.

## <a name="creating-a-global-app"></a>Erstellen einer globalen App
Die App, die Sie erstellen kann an verschiedene Sprachen angepasst werden, wodurch eine hervorragende Benutzerfreundlichkeit für Benutzer auf der ganzen Welt geboten wird.

### <a name="language-function"></a>„Language“-Funktion
Die Funktion **[Language](functions/function-language.md)** gibt das Sprachkennzeichen für den aktuellen Benutzer zurück.  Diese Funktion gibt z.B. **"en-GB"** für Benutzer in Großbritannien und **"de-DE"** für Benutzer in Deutschland zurück.  

Unter anderem können Sie **Language** dazu verwenden, Ihren Benutzern übersetzten Text anzuzeigen.  Ihre App kann eine Tabelle mit übersetzten Werten in Ihre App einschließen:

![](media/global-apps/loc-table.png)

Anschließend kann eine Formel wie die folgende verwendet werden, um übersetzte Zeichenfolgen aus der Tabelle zu ziehen:

**LookUp( Table1; TextID = "Hello" && (LanguageTag = Left( Language(); 2 ) || IsBlank( LanguageTag ))).LocalizedText**  

Bedenken Sie, dass die übersetzten Zeichenfolgen in anderen Sprachen wesentlich länger sein könnten als sie in Ihrer Sprache sind.  In vielen Fällen müssen die Bezeichnungen und anderen Elemente, die die Zeichenfolgen in Ihrer Benutzerschnittstelle anzeigen, breiter sein, um sich dem anzupassen.

Weitere Informationen finden Sie in der Dokumentation zur **[Language](functions/function-language.md)** -Funktion.

### <a name="formatting-numbers-dates-and-times"></a>Formatieren von Zahlen, Datumsangaben und Zeitangaben
Zahlen, Datumsangaben und Zeitangaben werden in verschiedenen Teilen der Welt in verschiedenen Formaten geschrieben.  Die Bedeutung von Kommas, Dezimalstellen und die Reihenfolge von Monat, Datum und Jahr variieren von Ort zu Ort.   

Die **[Text](functions/function-text.md)** -Funktion formatiert Zahlen und Datumsangaben anhand der Spracheinstellung des Benutzers.

**Text** erfordert, dass eine Formatzeichenfolge weiß, wie Sie die Zahl oder die Datumsangabe formatieren möchten.  Diese Zeichenfolge kann eine von zwei Formen annehmen:

* **Eine global kompatible Enumeration**.  Zum Beispiel **Text( Now(); DateTimeFormat.LongDate )** .  Mit dieser Formel wird das aktuelle Datum in einem für die Sprache geeigneten Format formatiert.  Dies stellt die bevorzugte Methode zum Angeben der Formatzeichenfolge dar.
* **Eine benutzerdefinierte Formatzeichenfolge**.  Zum Beispiel zeigt **Text( Now(); "[$-en-US]dddd, mmmm dd, yyyy" )** den gleichen Text wie die Enumeration an, wenn sie in der Sprache „en-US“ verwendet wird.  Der Vorteil der benutzerdefinierten Formatzeichenfolge ist, dass Sie genau angeben können, was Sie möchten.

"[$-en-US]" am Anfang der benutzerdefinierten Formatzeichenfolge gibt **Text** an, in welcher Sprache die benutzerdefinierte Formatzeichenfolge interpretiert werden soll.  Dies wird für Sie eingefügt und übernimmt standardmäßig Ihre Erstellungssprache.  Normalerweise müssen Sie dies nicht ändern.  Es ist hilfreich, wenn Autoren mit verschiedenen Sprachen die gleiche App bearbeiten.

Das dritte Argument für **Text** gibt an, welche Sprache für das Ergebnis der Funktion verwendet werden soll.  Der Standardwert ist die Spracheinstellung des aktuellen Benutzers.

Weitere Informationen finden Sie in der Dokumentation zur **[Text](functions/function-text.md)** -Funktion.      

### <a name="reading-numbers-dates-and-times"></a>Lesen von Zahlen, Datumsangaben und Zeitangaben
Es gibt vier Funktionen zum Lesen von Zahlen, Datumsangaben und Uhrzeiten, die vom Benutzer bereitgestellt werden:

* **[Wert](functions/function-value.md)** : Konvertiert eine Zahl in einer Text Zeichenfolge in einen Zahlenwert.
* **[DateValue](functions/function-datevalue-timevalue.md)** : Konvertiert einen Datumswert in einer Text Zeichenfolge in einen Datums-/Uhrzeitwert.  Jede Zeitangabe in der Textzeichenfolge wird ignoriert.
* **[TimeValue](functions/function-datevalue-timevalue.md)** : Konvertiert einen Zeitwert in einer Text Zeichenfolge in einen Datums-/Uhrzeitwert.  Jede Datumsangabe in der Textzeichenfolge wird ignoriert.
* **[DateTimeValue](functions/function-datevalue-timevalue.md)** : Konvertiert einen Datums-und Uhrzeitwert in einer Text Zeichenfolge in einen Datums-/Uhrzeitwert.  

Wenn Sie Excel verwendet haben, werden alle diese Funktionen in der einzelnen **Value**-Funktion kombiniert.  Sie werden hier besonders ausgewiesen, da PowerApps über getrennte Typen für date/time-Werte und Zahlen verfügt.

Alle diese Funktionen haben die gleichen Argumente:

* *Zeichenfolge, erforderlich*: Eine Zeichenfolge vom Benutzer. Beispielsweise gibt eine Zeichenfolge mit der **Text**-Eigenschaft Text in eine **Texteingabe**-Steuerelement ein und liest aus diesem.
* *Sprache, optional*: Die Sprache, in der die *Zeichenfolge*interpretiert werden soll.  Dabei handelt es sich standardmäßig um die Spracheinstellung des Benutzers.

Beispiel:

* **Value( "12,345.678"; "en-US" )** oder **Value( "12,345.678" )** , wo die Sprache des Benutzers „en-US“ ist, gibt die Zahl **12345,678** zurück, bereit für Berechnungen.
* **DateValue( "1/2/01"; "es-ES" )** oder **DateValue( "1/2/01" )** , wo die Sprache des Benutzers „es-ES“ ist, gibt den date/time-Wert **February 1, 2001 at midnight** (01. Februar 2001, Mitternacht) zurück.
* **TimeValue( "11:43:02"; "fr-FR" )** or **DateValue( "11:43:02" )** , wo die Sprache des Benutzers „fr-FR“ ist, gibt den date/time-Wert **January 1, 1970 at 11:43:02** (01. Januar 1970, 11:43:02) zurück.
* **TimeDateValue( "11:43:02 1/2/01"; "de-DE" )** or **DateValue( "11:43:02" )** , wo die Sprache des Benutzers „de-DE“ ist, gibt den date/time-Wert **February 1, 2001 at 11:43:02** (01. Februar 2001, 11:43:02) zurück.

Weitere Informationen finden Sie in der Dokumentation zu den Funktionen **[Value](functions/function-value.md)** , **[DateValue, TimeValue und DateTimeValue](functions/function-datevalue-timevalue.md)** sowie unter [Show text and format dates and times in PowerApps (Anzeigen von Text und Formatieren von Datums- und Zeitangaben in PowerApps)](show-text-dates-times.md).

### <a name="calendar-and-clock-information"></a>Kalender- und Uhrzeitinformationen
Die Funktionen **[Calendar](functions/function-clock-calendar.md)** und **[Clock](functions/function-clock-calendar.md)** stellen Kalender- und Uhrzeitinformationen für die aktuelle Sprache des Benutzers bereit.  

Verwenden Sie diese Funktionen u.a. zum Bereitstellen eines **Dropdown**-Steuerelements mit einer Liste von Auswahlmöglichkeiten.  

Weitere Informationen finden Sie in der Dokumentation zu den **[Calendar](functions/function-clock-calendar.md)** - und **[Clock](functions/function-clock-calendar.md)** -Funktionen.
