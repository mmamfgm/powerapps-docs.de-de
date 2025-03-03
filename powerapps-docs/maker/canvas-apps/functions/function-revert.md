---
title: Funktion „Revert“ | Microsoft-Dokumentation
description: Referenzinformationen einschließlich Syntax und Beispielen für die Funktion „Revert“ in PowerApps
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 10/21/2015
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: dbf1c623b18bc244e62fd962625f1d7cde35f1e4
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/07/2019
ms.locfileid: "71992455"
ms.PowerAppsDecimalTransform: true
---
# <a name="revert-function-in-powerapps"></a>Funktion „Revert“ in PowerApps
Aktualisiert und behebt Fehler für die [Datensätze](../working-with-tables.md#records) einer [Datenquelle](../working-with-data-sources.md)

## <a name="description"></a>Beschreibung
Die **Revert**-Funktion aktualisiert eine gesamte Datenquelle oder einen einzelnen Datensatz in der Datenquelle. Sie können die Änderungen anzeigen, die andere Benutzer vorgenommen haben.

Bei den wiederhergestellten Datensätzen behebt **Revert** auf alle Fehler der [Tabelle](../working-with-tables.md), die von der **[Errors](function-errors.md)** -Funktion zurückgegeben werden.

Wenn die **[Errors](function-errors.md)** -Funktion einen Konflikt nach einem **[Patch](function-patch.md)** - oder einem anderen Datenvorgang meldet, führen Sie die **Revert**-Funktion auf den Datensatz aus, um mit der in Konflikt stehenden Version zu beginnen und die Änderung erneut vorzunehmen.

**Revert** hat keinen Rückgabewert. Sie können diese Funktion nur in einer [Verhaltensformel](../working-with-formulas-in-depth.md) verwenden.

## <a name="syntax"></a>Syntax
**Revert**( *Datenquelle* [; *Datensatz* ] )

* *Datenquelle*: Erforderlich. Die Datenquelle, die Sie wiederherstellen möchten.
* *Datensatz*: Optional.  Der Datensatz, den Sie wiederherstellen möchten.  Wenn Sie keinen Datensatz angeben, wird die gesamte Datenquelle wiederhergestellt.

## <a name="example"></a>Beispiel
In diesem Beispiel stellen Sie die Datenquelle namens **IceCream** (Eiscreme) wieder her, die mit den Daten in dieser Tabelle beginnt:

![](media/function-revert/icecream.png)

Ein Benutzer auf einem anderen Gerät ändert die **Quantity**-Eigenschaft des Datensatzes **Strawberry** (Erdbeere) auf **400**.  Etwa zur gleichen Zeit ändern Sie die gleiche Eigenschaft des gleichen Datensatzes auf **500**, wobei Sie keine Kenntnis von der anderen Änderung haben.

Sie verwenden die **[Patch](function-patch.md)** -Funktion, um den Datensatz zu aktualisieren:<br>
Patch für **(icecream; First (Filter (icecream; Flavor = "Erdbeer")); {Menge: 500})**

Sie überprüfen die **[Errors](function-errors.md)** -Tabelle und finden einen Fehler:

| Datensatz | [Spalte](../working-with-tables.md#columns) | Nachricht | Fehler |
| --- | --- | --- | --- |
| **{ID: 1;-Konfiguration: "Erdbeer"; Menge: 300}** |*blank* |**"The record you are trying to modify has been modified by another user.  Please revert the record and try again." (Der Datensatz, den Sie versuchen zu ändern, wurde von einem anderen Benutzer geändert. Bitte stellen Sie den Datensatz wieder her, und versuchen Sie es erneut.)** |**ErrorKind.Conflict** |

Basierend auf der Spalte **Error** (Fehler) haben Sie eine Schaltfläche **Reload** (Erneut laden), für die die **[OnSelect](../controls/properties-core.md)** -Eigenschaft auf diese Formel festgelegt wird:<br>
**Revert( IceCream; First( Filter( IceCream; Flavor = "Strawberry" ) ) )**

Nachdem Sie die **Reload**-Schaltfläche ausgewählt haben, ist die **[Errors](function-errors.md)** -Tabelle [leer](function-isblank-isempty.md), und der neue Wert für **Strawberry** wurde geladen:

![](media/function-revert/icecream-after.png)

Sie wenden Ihre Änderung erneut auf die vorherige Änderung an, und Ihre Änderung wird erfolgreich vorgenommen, da der Konflikt gelöst wurde.

![](media/function-revert/icecream-success.png)

