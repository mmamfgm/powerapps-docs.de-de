---
title: Color-Enumeration und ColorFade-, ColorValue- und RGBA-Funktionen | Microsoft-Dokumentation
description: Referenzinformationen für die Color-Enumeration und ColorFade-, ColorValue- und RGBA-Funktionen in PowerApps, einschließlich Syntax und Beispiele
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 06/04/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 4af851160ea8a2add22add9f79dcc181a734e715
ms.sourcegitcommit: 7c1e70e94d75140955518349e6f9130ce3fd094e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/29/2019
ms.locfileid: "71994855"
ms.PowerAppsDecimalTransform: true
---
# <a name="color-enumeration-and-colorfade-colorvalue-and-rgba-functions-in-powerapps"></a>Color-Enumeration und ColorFade-, ColorValue- und RGBA-Funktionen in PowerApps

Verwenden Sie integrierte Farbwerte, definieren Sie benutzerdefinierte Farben, und verwenden Sie den Alphakanal.

## <a name="description"></a>Beschreibung

Mithilfe der **farbenumeration** können Sie problemlos auf die Farben zugreifen, die von HTML-Cascading Stylesheets (CSS) definiert werden. **Color. Red** gibt z. b. rein rot zurück. Eine Liste dieser Farben finden Sie am Ende dieses Themas.

Die **ColorValue** -Funktion gibt eine Farbe zurück, die auf einer Farb Zeichenfolge in einem CSS basiert. Die Zeichenfolge kann beliebige dieser Formulare annehmen:

- **CSS-Farbname:** **"roxybrown"** und **"OliveDrab"** sind Beispiele. Diese Namen enthalten keine Leerzeichen. Die Liste der unterstützten Farben wird weiter unten in diesem Thema angezeigt.
- **6-stelliger** Hexadezimalwert: Beispiel: **"#ffd700"** ist identisch mit **"Gold"** . Die Zeichenfolge hat das Format "#*RRGGBB*", wobei *RR* der rote Teil in zwei hexadezimal Ziffern ist, *GG* das grüne und *BB* der blaue Wert ist.
- **8-stelliger** Hexadezimalwert: Beispiel: **"#ff7f5080"** ist identisch mit **"Coral"** mit einem Alphakanal von 50%. Die Zeichenfolge hat das Format "#*RRGGBBAA*", wobei *RR*, *GG*und *BB* mit der 6-stelligen Form identisch sind. Der Alphakanal wird durch *AA*: **00** dargestellt, der vollständig transparent ist, und **FF** stellt vollständig nicht transparent dar.

Die **RGBA** -Funktion gibt eine Farbe zurück, die auf roten, grünen und blauen Komponenten basiert. Die-Funktion enthält auch einen Alphakanal zum Mischen von Farben von Steuerelementen, die vor einander angeordnet sind. Ein Alphakanal variiert von 0 (null) oder 0% (vollständig transparent und unsichtbar) bis 1 oder 100% (der vollständig deckend ist und alle Ebenen hinter einem Steuerelement vollständig blockiert).

Die **ColorFade**-Funktion gibt eine hellere bzw. dunklere Version einer Farbe zurück. Der Wert für das Ausblenden variiert von-1 (wodurch eine Farbe vollständig in schwarz dunkel ist) auf 0 (was sich nicht auf die Farbe auswirkt) auf 1 (wodurch eine Farbe vollständig in weiß dargestellt wird).

## <a name="alpha-channel"></a>Alpha Kanal

In einer Canvas-App können Sie Steuerelemente vor einem anderen Ebenen und die Transparenz eines Steuer Elements für alle dahinter liegenden Steuerelemente festlegen. Folglich werden Farben durch die Ebenen Blend. Dieses Diagramm zeigt z. b., wie die drei primären Farben mit einer Alpha-Einstellung von 50% gemischt werden:

> [!div class="mx-imgBorder"]
> ![drei Primärfarben mit einer Alpha Einstellung von 50%](media/function-colors/alpha-primary.png)

Sie können Bilder auch in Dateiformaten mischen, die Alphakanäle unterstützen. Beispielsweise können Sie keine JPEG-Dateien mischen, aber Sie können auch. png-Dateien mischen. Die nächste Grafik zeigt die gleichen roten, grünen und blauen Farben aus dem vorherigen Beispiel, aber die rote Farbe wird als Wellenlinie (anstelle eines Kreises) in einer PNG-Datei mit einem 50% Alpha-Kanal angezeigt:

> [!div class="mx-imgBorder"]
> ![rote Wellenlinie mit einer Alpha-Einstellung von 50% vor blauen und grünen Kreisen](media/function-colors/alpha-image.png)

Wenn Sie einen farbenumerationswert angeben oder eine **ColorValue** -Formel mit einem Farbnamen oder einem 6-stelligen Hexadezimalwert erstellen, ist die Alpha Einstellung 100%, was vollständig deckend ist.

## <a name="syntax"></a>Syntax

**Color**.*ColorName*

- *ColorName*: Erforderlich.  Name einer Cascading Stylesheet-Farbe (CSS). Die Liste möglicher Enumerationswerte wird am Ende dieses Themas angezeigt.

**ColorValue**( *CSSColor* )

- *CSSColor*: Erforderlich.  Name einer Cascading Stylesheet-Definition (CSS). Sie können einen Namen (z. b. **OliveDrab**) oder einen Hexadezimalwert angeben, z. b. **#6b8e23** oder **#7fffd420**. Hexadezimale Werte können entweder die Form "#*RRGGBB* " oder "#*RRGGBBAA*" haben.

**RGBA**( *Red*; *Green*; *Blue*; *Alpha* )

- *Red*, *Green*, *Blue*: Erforderlich.  Farbkomponenten Werte, die zwischen 0 (keine Sättigung) und 255 (vollständige Sättigung) liegen.
- *Alpha*: Erforderlich.  Alpha Komponente, die zwischen 0 (vollständig transparent) und 1 (vollständig nicht transparent) liegt. Sie können auch einen Prozentsatz, 0 % bis 100 %, verwenden.

**ColorFade**( *Color*; *FadeAmount* )

- *Color*: Erforderlich.  Ein Farbwert wie z.B. **Color.Red** oder die Ausgabe von **ColorValue** oder **RGBA**.
- *FadeAmount*: Erforderlich.  Eine Zahl zwischen -1 und 1. -1 markiert eine Farbe vollständig in schwarz, 0 wirkt sich nicht auf die Farbe aus, und 1 lässt eine Farbe vollständig in weiß aus. Sie können auch einen Prozentsatz zwischen-100% und 100% verwenden.

## <a name="built-in-colors"></a>Integrierte Farben

| Farbenumeration | ColorValue | RGBA | Farbmuster |
| --- | --- | --- | --- |
| **Color.AliceBlue** |**ColorValue ("#F0F8FF" &nbsp;)**<br>**ColorValue ("AliceBlue"-&nbsp;)** |**RGBA (&nbsp;240, &nbsp;248, &nbsp;255, &nbsp;1 &nbsp;)** |![aliceblue](./media/function-colors/color-aliceblue.png) |
| **Color.AntiqueWhite** |**ColorValue ("#faebd7" &nbsp;)**<br>**ColorValue ("AntiqueWhite"-&nbsp;)** |**RGBA (&nbsp;250, &nbsp;235, &nbsp;215, &nbsp;1 &nbsp;)** |![antiquewhite](./media/function-colors/color-antiquewhite.png) |
| **Color.Aqua** |**ColorValue ("#00ffff" &nbsp;)**<br>**ColorValue ("Aqua"-&nbsp;)** |**RGBA (&nbsp;0, &nbsp;255, &nbsp;255, &nbsp;1 &nbsp;)** |![aqua](./media/function-colors/color-aqua.png) |
| **Color.Aquamarine** |**ColorValue ("#7fffd4" &nbsp;)**<br>**ColorValue ("Aquamarine"-&nbsp;)** |**RGBA (&nbsp;127, &nbsp;255, &nbsp;212, &nbsp;1 &nbsp;)** |![aquamarine](./media/function-colors/color-aquamarine.png) |
| **Color.Azure** |**ColorValue ("#f0ffff" &nbsp;)**<br>**ColorValue ("Azure"-&nbsp;)** |**RGBA (&nbsp;240, &nbsp;255, &nbsp;255, &nbsp;1 &nbsp;)** |![azure](./media/function-colors/color-azure.png) |
| **Color.Beige** |**ColorValue ("#f5f5dc" &nbsp;)**<br>**ColorValue ("Beige"-&nbsp;)** |**RGBA (&nbsp;245, &nbsp;245, &nbsp;220, &nbsp;1 &nbsp;)** |![beige](./media/function-colors/color-beige.png) |
| **Color.Bisque** |**ColorValue ("#ffe4c4" &nbsp;)**<br>**ColorValue ("Bisque" &nbsp;)** |**RGBA (&nbsp;255, &nbsp;228, &nbsp;196, &nbsp;1 &nbsp;)** |![bisque](./media/function-colors/color-bisque.png) |
| **Color.Black** |**ColorValue ("#000000" &nbsp;)**<br>**ColorValue ("Black"-&nbsp;)** |**RGBA (&nbsp;0, &nbsp;0, &nbsp;0, &nbsp;1 &nbsp;)** |![black](./media/function-colors/color-black.png) |
| **Color.BlanchedAlmond** |**ColorValue ("#ffebcd" &nbsp;)**<br>**ColorValue ("BlanchedAlmond"-&nbsp;)** |**RGBA (&nbsp;255, &nbsp;235, &nbsp;205, &nbsp;1 &nbsp;)** |![blanchedalmond](./media/function-colors/color-blanchedalmond.png) |
| **Color.Blue** |**ColorValue ("#0000FF" &nbsp;)**<br>**ColorValue ("Blue" &nbsp;)** |**RGBA (&nbsp;0, &nbsp;0, &nbsp;255, &nbsp;1 &nbsp;)** |![blue](./media/function-colors/color-blue.png) |
| **Color.BlueViolet** |**ColorValue ("#8a2be2" &nbsp;)**<br>**ColorValue ("blueviolett"-&nbsp;)** |**RGBA (&nbsp;138, &nbsp;43, &nbsp;226, &nbsp;1 &nbsp;)** |![blueviolet](./media/function-colors/color-blueviolet.png) |
| **Color.Brown** |**ColorValue ("#a52a2a" &nbsp;)**<br>**ColorValue ("Brown" &nbsp;)** |**RGBA (&nbsp;165, &nbsp;42, &nbsp;42, &nbsp;1 &nbsp;)** |![brown](./media/function-colors/color-brown.png) |
| **Color.Burlywood** |**ColorValue ("#deb887" &nbsp;)**<br>**ColorValue ("BurlyWood"-&nbsp;)** |**RGBA (&nbsp;222, &nbsp;184, &nbsp;135, &nbsp;1 &nbsp;)** |![burlywood](./media/function-colors/color-burlywood.png) |
| **Color.CadetBlue** |**ColorValue ("#5f9ea0" &nbsp;)**<br>**ColorValue ("CadetBlue" &nbsp;)** |**RGBA (&nbsp;95, &nbsp;158, &nbsp;160, &nbsp;1 &nbsp;)** |![cadetblue](./media/function-colors/color-cadetblue.png) |
| **Color.Chartreuse** |**ColorValue ("#7fff00" &nbsp;)**<br>**ColorValue ("Chartreuse" &nbsp;)** |**RGBA (&nbsp;127, &nbsp;255, &nbsp;0, &nbsp;1 &nbsp;)** |![chartreuse](./media/function-colors/color-chartreuse.png) |
| **Color.Chocolate** |**ColorValue ("#d2691e" &nbsp;)**<br>**ColorValue ("Chocolate" &nbsp;)** |**RGBA (&nbsp;210, &nbsp;105, &nbsp;30, &nbsp;1 &nbsp;)** |![chocolate](./media/function-colors/color-chocolate.png) |
| **Color.Coral** |**ColorValue ("#ff7f50" &nbsp;)**<br>**ColorValue ("Coral" &nbsp;)** |**RGBA (&nbsp;255, &nbsp;127, &nbsp;80, &nbsp;1 &nbsp;)** |![coral](./media/function-colors/color-coral.png) |
| **Color.CornflowerBlue** |**ColorValue ("#6495ed" &nbsp;)**<br>**ColorValue ("Kornblumenblau" &nbsp;)** |**RGBA (&nbsp;100, &nbsp;149, &nbsp;237, &nbsp;1 &nbsp;)** |![cornflowerblue](./media/function-colors/color-cornflowerblue.png) |
| **Color.Cornsilk** |**ColorValue ("#fff8dc" &nbsp;)**<br>**ColorValue ("Cornsilk"-&nbsp;)** |**RGBA (&nbsp;255, &nbsp;248, &nbsp;220, &nbsp;1 &nbsp;)** |![cornsilk](./media/function-colors/color-cornsilk.png) |
| **Color.Crimson** |**ColorValue ("#dc143c" &nbsp;)**<br>**ColorValue ("Crimson"-&nbsp;)** |**RGBA (&nbsp;220, &nbsp;20, &nbsp;60, &nbsp;1 &nbsp;)** |![crimson](./media/function-colors/color-crimson.png) |
| **Color.Cyan** |**ColorValue ("#00ffff" &nbsp;)**<br>**ColorValue ("Cyan"-&nbsp;)** |**RGBA (&nbsp;0, &nbsp;255, &nbsp;255, &nbsp;1 &nbsp;)** |![cyan](./media/function-colors/color-cyan.png) |
| **Color.DarkBlue** |**ColorValue ("#00008b" &nbsp;)**<br>**ColorValue ("DarkBlue"-&nbsp;)** |**RGBA (&nbsp;0, &nbsp;0, &nbsp;139, &nbsp;1 &nbsp;)** |![darkblue](./media/function-colors/color-darkblue.png) |
| **Color.DarkCyan** |**ColorValue ("#008b8b" &nbsp;)**<br>**ColorValue ("DarkCyan"-&nbsp;)** |**RGBA (&nbsp;0, &nbsp;139, &nbsp;139, &nbsp;1 &nbsp;)** |![darkcyan](./media/function-colors/color-darkcyan.png) |
| **Color.DarkGoldenRod** |**ColorValue ("#b8860b" &nbsp;)**<br>**ColorValue ("darkgoldenrod" &nbsp;)** |**RGBA (&nbsp;184, &nbsp;134, &nbsp;11, &nbsp;1 &nbsp;)** |![darkgoldenrod](./media/function-colors/color-darkgoldenrod.png) |
| **Color.DarkGray** |**ColorValue ("#A9A9A9" &nbsp;)**<br>**ColorValue ("DarkGray" &nbsp;)** |**RGBA (&nbsp;169, &nbsp;169, &nbsp;169, &nbsp;1 &nbsp;)** |![darkgray](./media/function-colors/color-darkgray.png) |
| **Color.DarkGreen** |**ColorValue ("#006400" &nbsp;)**<br>**ColorValue ("darkgreen"-&nbsp;)** |**RGBA (&nbsp;0, &nbsp;100, &nbsp;0, &nbsp;1 &nbsp;)** |![darkgreen](./media/function-colors/color-darkgreen.png) |
| **Color.DarkGrey** |**ColorValue ("#A9A9A9" &nbsp;)**<br>**ColorValue ("Darkgrey" &nbsp;)** |**RGBA (&nbsp;169, &nbsp;169, &nbsp;169, &nbsp;1 &nbsp;)** |![darkgrey](./media/function-colors/color-darkgrey.png) |
| **Color.DarkKhaki** |**ColorValue ("#bdb76b" &nbsp;)**<br>**ColorValue ("DarkKhaki"-&nbsp;)** |**RGBA (&nbsp;189, &nbsp;183, &nbsp;107, &nbsp;1 &nbsp;)** |![darkkhaki](./media/function-colors/color-darkkhaki.png) |
| **Color.DarkMagenta** |**ColorValue ("#8b008b" &nbsp;)**<br>**ColorValue ("darkmagenta" &nbsp;)** |**RGBA (&nbsp;139, &nbsp;0, &nbsp;139, &nbsp;1 &nbsp;)** |![darkmagenta](./media/function-colors/color-darkmagenta.png) |
| **Color.DarkOliveGreen** |**ColorValue ("#556b2f" &nbsp;)**<br>**ColorValue ("darkolivegreen" &nbsp;)** |**RGBA (&nbsp;85, &nbsp;107, &nbsp;47, &nbsp;1 &nbsp;)** |![darkolivegreen](./media/function-colors/color-darkolivegreen.png) |
| **Color.DarkOrange** |**ColorValue ("#FF8C00" &nbsp;)**<br>**ColorValue ("DarkOrange" &nbsp;)** |**RGBA (&nbsp;255, &nbsp;140, &nbsp;0, &nbsp;1 &nbsp;)** |![darkorange](./media/function-colors/color-darkorange.png) |
| **Color.DarkOrchid** |**ColorValue ("#9932cc" &nbsp;)**<br>**ColorValue ("DarkOrchid" &nbsp;)** |**RGBA (&nbsp;153, &nbsp;50, &nbsp;204, &nbsp;1 &nbsp;)** |![darkorchid](./media/function-colors/color-darkorchid.png) |
| **Color.DarkRed** |**ColorValue ("#8b0000" &nbsp;)**<br>**ColorValue ("DarkRed" &nbsp;)** |**RGBA (&nbsp;139, &nbsp;0, &nbsp;0, &nbsp;1 &nbsp;)** |![darkred](./media/function-colors/color-darkred.png) |
| **Color.DarkSalmon** |**ColorValue ("#e9967a" &nbsp;)**<br>**ColorValue ("darklachs"-&nbsp;)** |**RGBA (&nbsp;233, &nbsp;150, &nbsp;122, &nbsp;1 &nbsp;)** |![darksalmon](./media/function-colors/color-darksalmon.png) |
| **Color.DarkSeaGreen** |**ColorValue ("#8fbc8f" &nbsp;)**<br>**ColorValue ("darksagreen" &nbsp;)** |**RGBA (&nbsp;143, &nbsp;188, &nbsp;143, &nbsp;1 &nbsp;)** |![darkseagreen](./media/function-colors/color-darkseagreen.png) |
| **Color.DarkSlateBlue** |**ColorValue ("#483d8b" &nbsp;)**<br>**ColorValue ("DarkSlateBlue" &nbsp;)** |**RGBA (&nbsp;72, &nbsp;61, &nbsp;139, &nbsp;1 &nbsp;)** |![darkslateblue](./media/function-colors/color-darkslateblue.png) |
| **Color.DarkSlateGray** |**ColorValue ("#2f4f4f" &nbsp;)**<br>**ColorValue ("DarkSlateGray" &nbsp;)** |**RGBA (&nbsp;47, &nbsp;79, &nbsp;79, &nbsp;1 &nbsp;)** |![darkslategray](./media/function-colors/color-darkslategray.png) |
| **Color.DarkSlateGrey** |**ColorValue ("#2f4f4f" &nbsp;)**<br>**ColorValue ("darkslategrey" &nbsp;)** |**RGBA (&nbsp;47, &nbsp;79, &nbsp;79, &nbsp;1 &nbsp;)** |![darkslategrey](./media/function-colors/color-darkslategrey.png) |
| **Color.DarkTurquoise** |**ColorValue ("#00ced1" &nbsp;)**<br>**ColorValue ("darktürkis"-&nbsp;)** |**RGBA (&nbsp;0, &nbsp;206, &nbsp;209, &nbsp;1 &nbsp;)** |![darkturquoise](./media/function-colors/color-darkturquoise.png) |
| **Color.DarkViolet** |**ColorValue ("#9400d3" &nbsp;)**<br>**ColorValue ("darkviol"-&nbsp;)** |**RGBA (&nbsp;148, &nbsp;0, &nbsp;211, &nbsp;1 &nbsp;)** |![darkviolet](./media/function-colors/color-darkviolet.png) |
| **Color.DeepPink** |**ColorValue ("#ff1493" &nbsp;)**<br>**ColorValue ("deeppink"-&nbsp;)** |**RGBA (&nbsp;255, &nbsp;20, &nbsp;147, &nbsp;1 &nbsp;)** |![deeppink](./media/function-colors/color-deeppink.png) |
| **Color.DeepSkyBlue** |**ColorValue ("#00bfff" &nbsp;)**<br>**ColorValue ("deepskyblue" &nbsp;)** |**RGBA (&nbsp;0, &nbsp;191, &nbsp;255, &nbsp;1 &nbsp;)** |![deepskyblue](./media/function-colors/color-deepskyblue.png) |
| **Color.DimGray** |**ColorValue ("#696969" &nbsp;)**<br>**ColorValue ("DimGray"-&nbsp;)** |**RGBA (&nbsp;105, &nbsp;105, &nbsp;105, &nbsp;1 &nbsp;)** |![dimgray](./media/function-colors/color-dimgray.png) |
| **Color.DimGrey** |**ColorValue ("#696969" &nbsp;)**<br>**ColorValue ("dimgrey" &nbsp;)** |**RGBA (&nbsp;105, &nbsp;105, &nbsp;105, &nbsp;1 &nbsp;)** |![dimgrey](./media/function-colors/color-dimgrey.png) |
| **Color.DodgerBlue** |**ColorValue ("#1e90ff" &nbsp;)**<br>**ColorValue ("DodgerBlue" &nbsp;)** |**RGBA (&nbsp;30, &nbsp;144, &nbsp;255, &nbsp;1 &nbsp;)** |![dodgerblue](./media/function-colors/color-dodgerblue.png) |
| **Color.FireBrick** |**ColorValue ("#B22222" &nbsp;)**<br>**ColorValue ("Firebrick"-&nbsp;)** |**RGBA (&nbsp;178, &nbsp;34, &nbsp;34, &nbsp;1 &nbsp;)** |![firebrick](./media/function-colors/color-firebrick.png) |
| **Color.FloralWhite** |**ColorValue ("#fffaf0" &nbsp;)**<br>**ColorValue ("FloralWhite" &nbsp;)** |**RGBA (&nbsp;255, &nbsp;250, &nbsp;240, &nbsp;1 &nbsp;)** |![floralwhite](./media/function-colors/color-floralwhite.png) |
| **Color.ForestGreen** |**ColorValue ("#228b22" &nbsp;)**<br>**ColorValue ("ForestGreen"-&nbsp;)** |**RGBA (&nbsp;34, &nbsp;139, &nbsp;34, &nbsp;1 &nbsp;)** |![forestgreen](./media/function-colors/color-forestgreen.png) |
| **Color.Fuchsia** |**ColorValue ("#FF00FF" &nbsp;)**<br>**ColorValue ("Fuchsia" &nbsp;)** |**RGBA (&nbsp;255, &nbsp;0, &nbsp;255, &nbsp;1 &nbsp;)** |![fuchsia](./media/function-colors/color-fuchsia.png) |
| **Color.Gainsboro** |**ColorValue ("#dcdcdc" &nbsp;)**<br>**ColorValue ("Gainsboro"-&nbsp;)** |**RGBA (&nbsp;220, &nbsp;220, &nbsp;220, &nbsp;1 &nbsp;)** |![gainsboro](./media/function-colors/color-gainsboro.png) |
| **Color.GhostWhite** |**ColorValue ("#f8f8ff" &nbsp;)**<br>**ColorValue ("GhostWhite"-&nbsp;)** |**RGBA (&nbsp;248, &nbsp;248, &nbsp;255, &nbsp;1 &nbsp;)** |![ghostwhite](./media/function-colors/color-ghostwhite.png) |
| **Color.Gold** |**ColorValue ("#ffd700" &nbsp;)**<br>**ColorValue ("Gold"-&nbsp;)** |**RGBA (&nbsp;255, &nbsp;215, &nbsp;0, &nbsp;1 &nbsp;)** |![gold](./media/function-colors/color-gold.png) |
| **Color.GoldenRod** |**ColorValue ("#DAA520" &nbsp;)**<br>**ColorValue ("Goldenrod"-&nbsp;)** |**RGBA (&nbsp;218, &nbsp;165, &nbsp;32, &nbsp;1 &nbsp;)** |![goldenrod](./media/function-colors/color-goldenrod.png) |
| **Color.Gray** |**ColorValue ("#808080" &nbsp;)**<br>**ColorValue ("graue" &nbsp;)** |**RGBA (&nbsp;128, &nbsp;128, &nbsp;128, &nbsp;1 &nbsp;)** |![gray](./media/function-colors/color-gray.png) |
| **Color.Green** |**ColorValue ("#008000" &nbsp;)**<br>**ColorValue ("grünes" &nbsp;)** |**RGBA (&nbsp;0, &nbsp;128, &nbsp;0, &nbsp;1 &nbsp;)** |![green](./media/function-colors/color-green.png) |
| **Color.GreenYellow** |**ColorValue ("#adff2f" &nbsp;)**<br>**ColorValue ("greenyellow" &nbsp;)** |**RGBA (&nbsp;173, &nbsp;255, &nbsp;47, &nbsp;1 &nbsp;)** |![greenyellow](./media/function-colors/color-greenyellow.png) |
| **Color.Grey** |**ColorValue ("#808080" &nbsp;)**<br>**ColorValue ("Grauer" &nbsp;)** |**RGBA (&nbsp;128, &nbsp;128, &nbsp;128, &nbsp;1 &nbsp;)** |![grey](./media/function-colors/color-grey.png) |
| **Color.Honeydew** |**ColorValue ("#f0fff0" &nbsp;)**<br>**ColorValue ("honeydew"-&nbsp;)** |**RGBA (&nbsp;240, &nbsp;255, &nbsp;240, &nbsp;1 &nbsp;)** |![honeydew](./media/function-colors/color-honeydew.png) |
| **Color.HotPink** |**ColorValue ("#ff69b4" &nbsp;)**<br>**ColorValue ("hotrosa"-&nbsp;)** |**RGBA (&nbsp;255, &nbsp;105, &nbsp;180, &nbsp;1 &nbsp;)** |![hotpink](./media/function-colors/color-hotpink.png) |
| **Color.IndianRed** |**ColorValue ("#cd5c5c" &nbsp;)**<br>**ColorValue ("IndianRed" &nbsp;)** |**RGBA (&nbsp;205, &nbsp;92, &nbsp;92, &nbsp;1 &nbsp;)** |![indianred](./media/function-colors/color-indianred.png) |
| **Color.Indigo** |**ColorValue ("#4b0082" &nbsp;)**<br>**ColorValue ("Indigo" &nbsp;)** |**RGBA (&nbsp;75, &nbsp;0, &nbsp;130, &nbsp;1 &nbsp;)** |![indigo](./media/function-colors/color-indigo.png) |
| **Color.Ivory** |**ColorValue ("#fffff0" &nbsp;)**<br>**ColorValue ("Elfenbein"-&nbsp;)** |**RGBA (&nbsp;255, &nbsp;255, &nbsp;240, &nbsp;1 &nbsp;)** |![ivory](./media/function-colors/color-ivory.png) |
| **Color.Khaki** |**ColorValue ("#f0e68c" &nbsp;)**<br>**ColorValue ("Khaki" &nbsp;)** |**RGBA (&nbsp;240, &nbsp;230, &nbsp;140, &nbsp;1 &nbsp;)** |![khaki](./media/function-colors/color-khaki.png) |
| **Color.Lavender** |**ColorValue ("#e6e6fa" &nbsp;)**<br>**ColorValue ("Lavendel"-&nbsp;)** |**RGBA (&nbsp;230, &nbsp;230, &nbsp;250, &nbsp;1 &nbsp;)** |![lavender](./media/function-colors/color-lavender.png) |
| **Color.LavenderBlush** |**ColorValue ("#fff0f5" &nbsp;)**<br>**ColorValue ("lavenderblush" &nbsp;)** |**RGBA (&nbsp;255, &nbsp;240, &nbsp;245, &nbsp;1 &nbsp;)** |![lavenderblush](./media/function-colors/color-lavenderblush.png) |
| **Color.LawnGreen** |**ColorValue ("#7cfc00" &nbsp;)**<br>**ColorValue ("lawngreen"-&nbsp;)** |**RGBA (&nbsp;124, &nbsp;252, &nbsp;0, &nbsp;1 &nbsp;)** |![lawngreen](./media/function-colors/color-lawngreen.png) |
| **Color.LemonChiffon** |**ColorValue ("#fffacd" &nbsp;)**<br>**ColorValue ("limonchiffon" &nbsp;)** |**RGBA (&nbsp;255, &nbsp;250, &nbsp;205, &nbsp;1 &nbsp;)** |![lemonchiffon](./media/function-colors/color-lemonchiffon.png) |
| **Color.LightBlue** |**ColorValue ("#add8e6" &nbsp;)**<br>**ColorValue ("LightBlue"-&nbsp;)** |**RGBA (&nbsp;173, &nbsp;216, &nbsp;230, &nbsp;1 &nbsp;)** |![lightblue](./media/function-colors/color-lightblue.png) |
| **Color.LightCoral** |**ColorValue ("#f08080" &nbsp;)**<br>**ColorValue ("LightCoral"-&nbsp;)** |**RGBA (&nbsp;240, &nbsp;128, &nbsp;128, &nbsp;1 &nbsp;)** |![lightcoral](./media/function-colors/color-lightcoral.png) |
| **Color.LightCyan** |**ColorValue ("#e0ffff" &nbsp;)**<br>**ColorValue ("LightCyan"-&nbsp;)** |**RGBA (&nbsp;224, &nbsp;255, &nbsp;255, &nbsp;1 &nbsp;)** |![lightcyan](./media/function-colors/color-lightcyan.png) |
| **Color.LightGoldenRodYellow** |**ColorValue ("#fafad2" &nbsp;)**<br>**ColorValue ("LightGoldenrodYellow" &nbsp;)** |**RGBA (&nbsp;250, &nbsp;250, &nbsp;210, &nbsp;1 &nbsp;)** |![lightgoldenrodyellow](./media/function-colors/color-lightgoldenrodyellow.png) |
| **Color.LightGray** |**ColorValue ("#d3d3d3" &nbsp;)**<br>**ColorValue ("LightGray" &nbsp;)** |**RGBA (&nbsp;211, &nbsp;211, &nbsp;211, &nbsp;1 &nbsp;)** |![lightgray](./media/function-colors/color-lightgray.png) |
| **Color.LightGreen** |**ColorValue ("#90ee90" &nbsp;)**<br>**ColorValue ("LightGreen"-&nbsp;)** |**RGBA (&nbsp;144, &nbsp;238, &nbsp;144, &nbsp;1 &nbsp;)** |![lightgreen](./media/function-colors/color-lightgreen.png) |
| **Color.LightGrey** |**ColorValue ("#d3d3d3" &nbsp;)**<br>**ColorValue ("lightgrey" &nbsp;)** |**RGBA (&nbsp;211, &nbsp;211, &nbsp;211, &nbsp;1 &nbsp;)** |![lightgrey](./media/function-colors/color-lightgrey.png) |
| **Color.LightPink** |**ColorValue ("#ffb6c1" &nbsp;)**<br>**ColorValue ("LightPink" &nbsp;)** |**RGBA (&nbsp;255, &nbsp;182, &nbsp;193, &nbsp;1 &nbsp;)** |![lightpink](./media/function-colors/color-lightpink.png) |
| **Color.LightSalmon** |**ColorValue ("#FFA07A" &nbsp;)**<br>**ColorValue ("LightSalmon"-&nbsp;)** |**RGBA (&nbsp;255, &nbsp;160, &nbsp;122, &nbsp;1 &nbsp;)** |![lightsalmon](./media/function-colors/color-lightsalmon.png) |
| **Color.LightSeaGreen** |**ColorValue ("#20b2aa" &nbsp;)**<br>**ColorValue ("lightsagreen" &nbsp;)** |**RGBA (&nbsp;32, &nbsp;178, &nbsp;170, &nbsp;1 &nbsp;)** |![lightseagreen](./media/function-colors/color-lightseagreen.png) |
| **Color.LightSkyBlue** |**ColorValue ("#87cefa" &nbsp;)**<br>**ColorValue ("LightSkyBlue" &nbsp;)** |**RGBA (&nbsp;135, &nbsp;206, &nbsp;250, &nbsp;1 &nbsp;)** |![lightskyblue](./media/function-colors/color-lightskyblue.png) |
| **Color.LightSlateGray** |**ColorValue ("#778899" &nbsp;)**<br>**ColorValue ("lightürlategray" &nbsp;)** |**RGBA (&nbsp;119, &nbsp;136, &nbsp;153, &nbsp;1 &nbsp;)** |![lightslategray](./media/function-colors/color-lightslategray.png) |
| **Color.LightSlateGrey** |**ColorValue ("#778899" &nbsp;)**<br>**ColorValue ("lightürlategrey" &nbsp;)** |**RGBA (&nbsp;119, &nbsp;136, &nbsp;153, &nbsp;1 &nbsp;)** |![lightslategrey](./media/function-colors/color-lightslategrey.png) |
| **Color.LightSteelBlue** |**ColorValue ("#b0c4de" &nbsp;)**<br>**ColorValue ("LightSteelBlue" &nbsp;)** |**RGBA (&nbsp;176, &nbsp;196, &nbsp;222, &nbsp;1 &nbsp;)** |![lightsteelblue](./media/function-colors/color-lightsteelblue.png) |
| **Color.LightYellow** |**ColorValue ("#FFFFE0" &nbsp;)**<br>**ColorValue ("LightYellow" &nbsp;)** |**RGBA (&nbsp;255, &nbsp;255, &nbsp;224, &nbsp;1 &nbsp;)** |![lightyellow](./media/function-colors/color-lightyellow.png) |
| **Color.Lime** |**ColorValue ("#00FF00" &nbsp;)**<br>**ColorValue ("Kalk" &nbsp;)** |**RGBA (&nbsp;0, &nbsp;255, &nbsp;0, &nbsp;1 &nbsp;)** |![lime](./media/function-colors/color-lime.png) |
| **Color.LimeGreen** |**ColorValue ("#32cd32" &nbsp;)**<br>**ColorValue ("LimeGreen"-&nbsp;)** |**RGBA (&nbsp;50, &nbsp;205, &nbsp;50, &nbsp;1 &nbsp;)** |![limegreen](./media/function-colors/color-limegreen.png) |
| **Color.Linen** |**ColorValue ("#faf0e6" &nbsp;)**<br>**ColorValue ("Leinen" &nbsp;)** |**RGBA (&nbsp;250, &nbsp;240, &nbsp;230, &nbsp;1 &nbsp;)** |![linen](./media/function-colors/color-linen.png) |
| **Color.Magenta** |**ColorValue ("#FF00FF" &nbsp;)**<br>**ColorValue ("Magenta" &nbsp;)** |**RGBA (&nbsp;255, &nbsp;0, &nbsp;255, &nbsp;1 &nbsp;)** |![magenta](./media/function-colors/color-magenta.png) |
| **Color.Maroon** |**ColorValue ("#800000" &nbsp;)**<br>**ColorValue ("Maroon" &nbsp;)** |**RGBA (&nbsp;128, &nbsp;0, &nbsp;0, &nbsp;1 &nbsp;)** |![maroon](./media/function-colors/color-maroon.png) |
| **Color.MediumAquamarine** |**ColorValue ("#66cdaa" &nbsp;)**<br>**ColorValue ("MediumAquamarine" &nbsp;)** |**RGBA (&nbsp;102, &nbsp;205, &nbsp;170, &nbsp;1 &nbsp;)** |![mediumaquamarine](./media/function-colors/color-mediumaquamarine.png) |
| **Color.MediumBlue** |**ColorValue ("#0000CD" &nbsp;)**<br>**ColorValue ("MediumBlue"-&nbsp;)** |**RGBA (&nbsp;0, &nbsp;0, &nbsp;205, &nbsp;1 &nbsp;)** |![mediumblue](./media/function-colors/color-mediumblue.png) |
| **Color.MediumOrchid** |**ColorValue ("#ba55d3" &nbsp;)**<br>**ColorValue ("medienorchid"-&nbsp;)** |**RGBA (&nbsp;186, &nbsp;85, &nbsp;211, &nbsp;1 &nbsp;)** |![mediumorchid](./media/function-colors/color-mediumorchid.png) |
| **Color.MediumPurple** |**ColorValue ("#9370db" &nbsp;)**<br>**ColorValue ("mediumschlag"-&nbsp;)** |**RGBA (&nbsp;147, &nbsp;112, &nbsp;219, &nbsp;1 &nbsp;)** |![mediumpurple](./media/function-colors/color-mediumpurple.png) |
| **Color.MediumSeaGreen** |**ColorValue ("#3cb371" &nbsp;)**<br>**ColorValue ("medienumalagreen" &nbsp;)** |**RGBA (&nbsp;60, &nbsp;179, &nbsp;113, &nbsp;1 &nbsp;)** |![mediumseagreen](./media/function-colors/color-mediumseagreen.png) |
| **Color.MediumSlateBlue** |**ColorValue ("#7b68ee" &nbsp;)**<br>**ColorValue ("MediumSlateBlue" &nbsp;)** |**RGBA (&nbsp;123, &nbsp;104, &nbsp;238, &nbsp;1 &nbsp;)** |![mediumslateblue](./media/function-colors/color-mediumslateblue.png) |
| **Color.MediumSpringGreen** |**ColorValue ("#00fa9a" &nbsp;)**<br>**ColorValue ("mediumspringgreen"-&nbsp;)** |**RGBA (&nbsp;0, &nbsp;250, &nbsp;154, &nbsp;1 &nbsp;)** |![mediumspringgreen](./media/function-colors/color-mediumspringgreen.png) |
| **Color.MediumTurquoise** |**ColorValue ("#48D1CC" &nbsp;)**<br>**ColorValue ("mediumschlag"-&nbsp;)** |**RGBA (&nbsp;72, &nbsp;209, &nbsp;204, &nbsp;1 &nbsp;)** |![mediumturquoise](./media/function-colors/color-mediumturquoise.png) |
| **Color.MediumVioletRed** |**ColorValue ("#c71585" &nbsp;)**<br>**ColorValue ("medienumvioletred" &nbsp;)** |**RGBA (&nbsp;199, &nbsp;21, &nbsp;133, &nbsp;1 &nbsp;)** |![mediumvioletred](./media/function-colors/color-mediumvioletred.png) |
| **Color.MidnightBlue** |**ColorValue ("#191970" &nbsp;)**<br>**ColorValue ("Mittel nachts blau"-&nbsp;)** |**RGBA (&nbsp;25, &nbsp;25, &nbsp;112, &nbsp;1 &nbsp;)** |![midnightblue](./media/function-colors/color-midnightblue.png) |
| **Color.MintCream** |**ColorValue ("#f5fffa" &nbsp;)**<br>**ColorValue ("MintCream"-&nbsp;)** |**RGBA (&nbsp;245, &nbsp;255, &nbsp;250, &nbsp;1 &nbsp;)** |![mintcream](./media/function-colors/color-mintcream.png) |
| **Color.MistyRose** |**ColorValue ("#ffe4e1" &nbsp;)**<br>**ColorValue ("MistyRose"-&nbsp;)** |**RGBA (&nbsp;255, &nbsp;228, &nbsp;225, &nbsp;1 &nbsp;)** |![mistyrose](./media/function-colors/color-mistyrose.png) |
| **Color.Moccasin** |**ColorValue ("#ffe4b5" &nbsp;)**<br>**ColorValue ("Moccasin" &nbsp;)** |**RGBA (&nbsp;255, &nbsp;228, &nbsp;181, &nbsp;1 &nbsp;)** |![moccasin](./media/function-colors/color-moccasin.png) |
| **Color.NavajoWhite** |**ColorValue ("#ffdead" &nbsp;)**<br>**ColorValue ("NavajoWhite" &nbsp;)** |**RGBA (&nbsp;255, &nbsp;222, &nbsp;173, &nbsp;1 &nbsp;)** |![navajowhite](./media/function-colors/color-navajowhite.png) |
| **Color.Navy** |**ColorValue ("#000080" &nbsp;)**<br>**ColorValue ("Navy" &nbsp;)** |**RGBA (&nbsp;0, &nbsp;0, &nbsp;128, &nbsp;1 &nbsp;)** |![navy](./media/function-colors/color-navy.png) |
| **Color.OldLace** |**ColorValue ("#fdf5e6" &nbsp;)**<br>**ColorValue ("OldLace"-&nbsp;)** |**RGBA (&nbsp;253, &nbsp;245, &nbsp;230, &nbsp;1 &nbsp;)** |![oldlace](./media/function-colors/color-oldlace.png) |
| **Color.Olive** |**ColorValue ("#808000" &nbsp;)**<br>**ColorValue ("Olive" &nbsp;)** |**RGBA (&nbsp;128, &nbsp;128, &nbsp;0, &nbsp;1 &nbsp;)** |![olive](./media/function-colors/color-olive.png) |
| **Color.OliveDrab** |**ColorValue ("#6b8e23" &nbsp;)**<br>**ColorValue ("OliveDrab" &nbsp;)** |**RGBA (&nbsp;107, &nbsp;142, &nbsp;35, &nbsp;1 &nbsp;)** |![olivedrab](./media/function-colors/color-olivedrab.png) |
| **Color.Orange** |**ColorValue ("#ffa500" &nbsp;)**<br>**ColorValue ("Orange" &nbsp;)** |**RGBA (&nbsp;255, &nbsp;165, &nbsp;0, &nbsp;1 &nbsp;)** |![orange](./media/function-colors/color-orange.png) |
| **Color.OrangeRed** |**ColorValue ("#ff4500" &nbsp;)**<br>**ColorValue ("Orange"-&nbsp;)** |**RGBA (&nbsp;255, &nbsp;69, &nbsp;0, &nbsp;1 &nbsp;)** |![orangered](./media/function-colors/color-orangered.png) |
| **Color.Orchid** |**ColorValue ("#da70d6" &nbsp;)**<br>**ColorValue ("Orchidee" &nbsp;)** |**RGBA (&nbsp;218, &nbsp;112, &nbsp;214, &nbsp;1 &nbsp;)** |![orchid](./media/function-colors/color-orchid.png) |
| **Color.PaleGoldenRod** |**ColorValue ("#eee8aa" &nbsp;)**<br>**ColorValue ("palegoldenrod" &nbsp;)** |**RGBA (&nbsp;238, &nbsp;232, &nbsp;170, &nbsp;1 &nbsp;)** |![palegoldenrod](./media/function-colors/color-palegoldenrod.png) |
| **Color.PaleGreen** |**ColorValue ("#98fb98" &nbsp;)**<br>**ColorValue ("palettengrün" &nbsp;)** |**RGBA (&nbsp;152, &nbsp;251, &nbsp;152, &nbsp;1 &nbsp;)** |![palegreen](./media/function-colors/color-palegreen.png) |
| **Color.PaleTurquoise** |**ColorValue ("#afeeee" &nbsp;)**<br>**ColorValue ("paletürkis"-&nbsp;)** |**RGBA (&nbsp;175, &nbsp;238, &nbsp;238, &nbsp;1 &nbsp;)** |![paleturquoise](./media/function-colors/color-paleturquoise.png) |
| **Color.PaleVioletRed** |**ColorValue ("#db7093" &nbsp;)**<br>**ColorValue ("PaleVioletRed" &nbsp;)** |**RGBA (&nbsp;219, &nbsp;112, &nbsp;147, &nbsp;1 &nbsp;)** |![palevioletred](./media/function-colors/color-palevioletred.png) |
| **Color.PapayaWhip** |**ColorValue ("#ffefd5" &nbsp;)**<br>**ColorValue ("PapayaWhip" &nbsp;)** |**RGBA (&nbsp;255, &nbsp;239, &nbsp;213, &nbsp;1 &nbsp;)** |![papayawhip](./media/function-colors/color-papayawhip.png) |
| **Color.PeachPuff** |**ColorValue ("#ffdab9" &nbsp;)**<br>**ColorValue ("Peer-Puff"-&nbsp;)** |**RGBA (&nbsp;255, &nbsp;218, &nbsp;185, &nbsp;1 &nbsp;)** |![peachpuff](./media/function-colors/color-peachpuff.png) |
| **Color.Peru** |**ColorValue ("#cd853f" &nbsp;)**<br>**ColorValue ("Peru" &nbsp;)** |**RGBA (&nbsp;205, &nbsp;133, &nbsp;63, &nbsp;1 &nbsp;)** |![peru](./media/function-colors/color-peru.png) |
| **Color.Pink** |**ColorValue ("#ffc0cb" &nbsp;)**<br>**ColorValue ("Rosa" &nbsp;)** |**RGBA (&nbsp;255, &nbsp;192, &nbsp;203, &nbsp;1 &nbsp;)** |![pink](./media/function-colors/color-pink.png) |
| **Color.Plum** |**ColorValue ("#dda0dd" &nbsp;)**<br>**ColorValue ("Plum"-&nbsp;)** |**RGBA (&nbsp;221, &nbsp;160, &nbsp;221, &nbsp;1 &nbsp;)** |![plum](./media/function-colors/color-plum.png) |
| **Color.PowderBlue** |**ColorValue ("#B0E0E6" &nbsp;)**<br>**ColorValue ("Powderblue"-&nbsp;)** |**RGBA (&nbsp;176, &nbsp;224, &nbsp;230, &nbsp;1 &nbsp;)** |![powderblue](./media/function-colors/color-powderblue.png) |
| **Color.Purple** |**ColorValue ("#800080" &nbsp;)**<br>**ColorValue ("Lila" &nbsp;)** |**RGBA (&nbsp;128, &nbsp;0, &nbsp;128, &nbsp;1 &nbsp;)** |![purple](./media/function-colors/color-purple.png) |
| **Color.Red** |**ColorValue ("#FF0000" &nbsp;)**<br>**ColorValue ("Red" &nbsp;)** |**RGBA (&nbsp;255, &nbsp;0, &nbsp;0, &nbsp;1 &nbsp;)** |![red](./media/function-colors/color-red.png) |
| **Color.RosyBrown** |**ColorValue ("#bc8f8f" &nbsp;)**<br>**ColorValue ("RosyBrown" &nbsp;)** |**RGBA (&nbsp;188, &nbsp;143, &nbsp;143, &nbsp;1 &nbsp;)** |![rosybrown](./media/function-colors/color-rosybrown.png) |
| **Color.RoyalBlue** |**ColorValue ("#4169e1" &nbsp;)**<br>**ColorValue ("RoyalBlue" &nbsp;)** |**RGBA (&nbsp;65, &nbsp;105, &nbsp;225, &nbsp;1 &nbsp;)** |![royalblue](./media/function-colors/color-royalblue.png) |
| **Color.SaddleBrown** |**ColorValue ("#8b4513" &nbsp;)**<br>**ColorValue ("SaddleBrown" &nbsp;)** |**RGBA (&nbsp;139, &nbsp;69, &nbsp;19, &nbsp;1 &nbsp;)** |![saddlebrown](./media/function-colors/color-saddlebrown.png) |
| **Color.Salmon** |**ColorValue ("#fa8072" &nbsp;)**<br>**ColorValue ("Lachs"-&nbsp;)** |**RGBA (&nbsp;250, &nbsp;128, &nbsp;114, &nbsp;1 &nbsp;)** |![salmon](./media/function-colors/color-salmon.png) |
| **Color.SandyBrown** |**ColorValue ("#f4a460" &nbsp;)**<br>**ColorValue ("SandyBrown" &nbsp;)** |**RGBA (&nbsp;244, &nbsp;164, &nbsp;96, &nbsp;1 &nbsp;)** |![sandybrown](./media/function-colors/color-sandybrown.png) |
| **Color.SeaGreen** |**ColorValue ("#2e8b57" &nbsp;)**<br>**ColorValue ("&nbsp;")** |**RGBA (&nbsp;46, &nbsp;139, &nbsp;87, &nbsp;1 &nbsp;)** |![seagreen](./media/function-colors/color-seagreen.png) |
| **Color.SeaShell** |**ColorValue ("#fff5ee" &nbsp;)**<br>**ColorValue ("Seashell"-&nbsp;)** |**RGBA (&nbsp;255, &nbsp;245, &nbsp;238, &nbsp;1 &nbsp;)** |![seashell](./media/function-colors/color-seashell.png) |
| **Color.Sienna** |**ColorValue ("#a0522d" &nbsp;)**<br>**ColorValue ("Sienna"-&nbsp;)** |**RGBA (&nbsp;160, &nbsp;82, &nbsp;45, &nbsp;1 &nbsp;)** |![sienna](./media/function-colors/color-sienna.png) |
| **Color.Silver** |**ColorValue ("#C0C0C0" &nbsp;)**<br>**ColorValue ("Silver" &nbsp;)** |**RGBA (&nbsp;192, &nbsp;192, &nbsp;192, &nbsp;1 &nbsp;)** |![silver](./media/function-colors/color-silver.png) |
| **Color.SkyBlue** |**ColorValue ("#87ceeb" &nbsp;)**<br>**ColorValue ("Skyblue"-&nbsp;)** |**RGBA (&nbsp;135, &nbsp;206, &nbsp;235, &nbsp;1 &nbsp;)** |![skyblue](./media/function-colors/color-skyblue.png) |
| **Color.SlateBlue** |**ColorValue ("#6a5acd" &nbsp;)**<br>**ColorValue ("SlateBlue" &nbsp;)** |**RGBA (&nbsp;106, &nbsp;90, &nbsp;205, &nbsp;1 &nbsp;)** |![slateblue](./media/function-colors/color-slateblue.png) |
| **Color.SlateGray** |**ColorValue ("#708090" &nbsp;)**<br>**ColorValue ("SlateGray" &nbsp;)** |**RGBA (&nbsp;112, &nbsp;128, &nbsp;144, &nbsp;1 &nbsp;)** |![slategray](./media/function-colors/color-slategray.png) |
| **Color.SlateGrey** |**ColorValue ("#708090" &nbsp;)**<br>**ColorValue ("slategrey" &nbsp;)** |**RGBA (&nbsp;112, &nbsp;128, &nbsp;144, &nbsp;1 &nbsp;)** |![slategrey](./media/function-colors/color-slategrey.png) |
| **Color.Snow** |**ColorValue ("#fffafa" &nbsp;)**<br>**ColorValue ("Schnee"-&nbsp;)** |**RGBA (&nbsp;255, &nbsp;250, &nbsp;250, &nbsp;1 &nbsp;)** |![snow](./media/function-colors/color-snow.png) |
| **Color.SpringGreen** |**ColorValue ("#00ff7f" &nbsp;)**<br>**ColorValue ("springgreen"-&nbsp;)** |**RGBA (&nbsp;0, &nbsp;255, &nbsp;127, &nbsp;1 &nbsp;)** |![springgreen](./media/function-colors/color-springgreen.png) |
| **Color.SteelBlue** |**ColorValue ("#4682b4" &nbsp;)**<br>**ColorValue ("Stahlblau" &nbsp;)** |**RGBA (&nbsp;70, &nbsp;130, &nbsp;180, &nbsp;1 &nbsp;)** |![steelblue](./media/function-colors/color-steelblue.png) |
| **Color.Tan** |**ColorValue ("#d2b48c" &nbsp;)**<br>**ColorValue ("Tan" &nbsp;)** |**RGBA (&nbsp;210, &nbsp;180, &nbsp;140, &nbsp;1 &nbsp;)** |![tan](./media/function-colors/color-tan.png) |
| **Color.Teal** |**ColorValue ("#008080" &nbsp;)**<br>**ColorValue ("Teal"-&nbsp;)** |**RGBA (&nbsp;0, &nbsp;128, &nbsp;128, &nbsp;1 &nbsp;)** |![teal](./media/function-colors/color-teal.png) |
| **Color.Thistle** |**ColorValue ("#d8bfd8" &nbsp;)**<br>**ColorValue ("Thistle"-&nbsp;)** |**RGBA (&nbsp;216, &nbsp;191, &nbsp;216, &nbsp;1 &nbsp;)** |![thistle](./media/function-colors/color-thistle.png) |
| **Color.Tomato** |**ColorValue ("#ff6347" &nbsp;)**<br>**ColorValue ("Tomaten&nbsp;)** |**RGBA (&nbsp;255, &nbsp;99, &nbsp;71, &nbsp;1 &nbsp;)** |![tomato](./media/function-colors/color-tomato.png) |
| **Color. transparent** |**ColorValue ("#00000000" &nbsp;)**<br>**ColorValue ("transparent" &nbsp;)** |**RGBA (&nbsp;0, &nbsp;0, &nbsp;0, &nbsp;0 &nbsp;)** |![sichtigen](./media/function-colors/color-transparent.png) |
| **Color.Turquoise** |**ColorValue ("#40e0d0" &nbsp;)**<br>**ColorValue ("Türkis"-&nbsp;)** |**RGBA (&nbsp;64, &nbsp;224, &nbsp;208, &nbsp;1 &nbsp;)** |![turquoise](./media/function-colors/color-turquoise.png) |
| **Color.Violet** |**ColorValue ("#ee82ee" &nbsp;)**<br>**ColorValue ("violett" &nbsp;)** |**RGBA (&nbsp;238, &nbsp;130, &nbsp;238, &nbsp;1 &nbsp;)** |![violet](./media/function-colors/color-violet.png) |
| **Color.Wheat** |**ColorValue ("#f5deb3" &nbsp;)**<br>**ColorValue ("Weizen"-&nbsp;)** |**RGBA (&nbsp;245, &nbsp;222, &nbsp;179, &nbsp;1 &nbsp;)** |![wheat](./media/function-colors/color-wheat.png) |
| **Color.White** |**ColorValue ("#FFFFFF" &nbsp;)**<br>**ColorValue ("White" &nbsp;)** |**RGBA (&nbsp;255, &nbsp;255, &nbsp;255, &nbsp;1 &nbsp;)** |![white](./media/function-colors/color-white.png) |
| **Color.WhiteSmoke** |**ColorValue ("#f5f5f5" &nbsp;)**<br>**ColorValue ("whitesmuke"-&nbsp;)** |**RGBA (&nbsp;245, &nbsp;245, &nbsp;245, &nbsp;1 &nbsp;)** |![whitesmoke](./media/function-colors/color-whitesmoke.png) |
| **Color.Yellow** |**ColorValue ("#FFFF00" &nbsp;)**<br>**ColorValue ("gelber" &nbsp;)** |**RGBA (&nbsp;255, &nbsp;255, &nbsp;0, &nbsp;1 &nbsp;)** |![yellow](./media/function-colors/color-yellow.png) |
| **Color.YellowGreen** |**ColorValue ("#9acd32" &nbsp;)**<br>**ColorValue ("Gelbgrün" &nbsp;)** |**RGBA (&nbsp;154, &nbsp;205, &nbsp;50, &nbsp;1 &nbsp;)** |![yellowgreen](./media/function-colors/color-yellowgreen.png) |
