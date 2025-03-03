---
title: Funktion „Value“ | Microsoft-Dokumentation
description: Referenzinformationen einschließlich Syntax und Beispielen für die Funktion „Value“ in PowerApps
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 11/07/2015
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: de9cf7aa2c01b25f17aa6be7ce1f95871c3ab118
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/07/2019
ms.locfileid: "71983384"
ms.PowerAppsDecimalTransform: true
---
# <a name="value-function-in-powerapps"></a>Funktion „Value“ in PowerApps
Konvertiert eine Textzeichenfolge in eine Zahl

## <a name="description"></a>Beschreibung
Die **Value**-Funktion konvertiert eine Textzeichenfolge, die numerische Zeichen enthält, in einen numerischen Wert. Verwenden Sie diese Funktion, wenn Sie eine Rechnung mit Zahlen durchführen müssen, die von einem Benutzer als Text eingegeben wurden.

Verschiedene Sprachen interpretieren **,** und **.** unterschiedlich.  Standardmäßig wird der Text in der Sprache des aktuellen Benutzers interpretiert.  Sie können die zu verwendende Sprache mit einem Sprachkennzeichen angeben mithilfe der gleichen Sprachkennzeichen, die auch von der **[Language](function-language.md)** -Funktion zurückgegeben werden.

Hinweise zum Format der Zeichenfolge:

* Für die aktuelle Sprache kann der Zeichenfolge das Währungssymbol vorangestellt werden.  Das Währungssymbol wird ignoriert.  Währungssymbole für andere Sprachen werden nicht ignoriert.
* Der Zeichenfolge wird eventuell ein Prozentzeichen ( **%** ) am Ende hinzugefügt, das angibt, dass es sich um einen Prozentsatz handelt.  Die Anzahl wird vor der Rückgabe durch 100 dividiert.  Prozentsätze und Währungssymbolen können nicht kombiniert werden.
* Die Zeichenfolge kann in wissenschaftlicher Schreibweise sein, in der 12 x 10<sup>3</sup> als "12e3" ausgedrückt wird.

Wenn die Anzahl nicht in einem entsprechenden Format ist, gibt **Value** *blank* zurück.

Verwenden Sie zum Konvertieren von Datums-und Uhrzeitwerten die Funktionen [**DateValue**](function-datevalue-timevalue.md), [ **TimeValue**](function-datevalue-timevalue.md) oder [**DateTimeValue**](function-datevalue-timevalue.md).

## <a name="syntax"></a>Syntax
**Value**(*Zeichenfolge* [;*LanguageTag*])

* *Zeichenfolge*: erforderlich. Die Zeichenfolge, die in einen numerischen Wert konvertiert werden soll
* *LanguageTag*: optional.  Das Sprachkennzeichen, in dem die Zeichenfolge analysiert werden soll.  Standardmäßig wird die Sprache des aktuellen Benutzers verwendet, wenn die Sprache nicht angegeben wurde.

## <a name="examples"></a>Beispiele
Der Benutzer, der diese Formeln ausführt, befindet sich in den USA und hat Englisch als seine Sprache ausgewählt.  Die Funktion **Language** gibt „en-US“ zurück.

| Formel | Beschreibung | Ergebnis |
| --- | --- | --- |
| **Value( "123.456" )** |Die Standardsprache "En-US" wird verwendet, in der ein Punkt als Dezimaltrennzeichen verwendet wird. |123.456 |
| **Value( "123.456"; "es-ES" )** |"es-ES" steht für Spanisch (Spanien).  In Spanien ist ein Punkt ein Tausendertrennzeichen. |123456 |
| **Value( "123,456" )** |Die Standardsprache "En-US" wird verwendet, in der ein Komma als Tausendertrennzeichen verwendet wird. |123456 |
| **Value( "123,456"; "es-ES" )** |"es-ES" steht für Spanisch (Spanien).  In Spanien ist das Dezimaltrennzeichen ein Komma. |123.456 |
| **Value( "12.34%" )** |Das Prozentzeichen am Ende der Zeichenfolge gibt an, dass dies ein Prozentsatz ist. |0.1234 |
| **Value( "$ 12.34" )** |Das Währungssymbol der aktuellen Sprache wird ignoriert. |12.34 |
| **Value( "24e3" )** |Wissenschaftliche Schreibweise für 12 x 10<sup>3</sup>. |24000 |

