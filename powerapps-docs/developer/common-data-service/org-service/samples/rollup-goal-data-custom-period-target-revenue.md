---
title: 'Beispiel: Rollup-Zieldaten für eine benutzerdefinierte Periode für den Zielumsatz (Common Data Service) | Microsoft-Dokumentation'
description: Dieses Beispiel zeigt, wie für Zieldaten für eine benutzerdefinierte Periode für den Zielumsatz ein Rollup durchgeführt wird.
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: samples
author: JimDaly
ms.author: jdaly
manager: ryjones
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 90867101361c8f2ca5bf9ed29e8712890ba162c3
ms.sourcegitcommit: 8185f87dddf05ee256491feab9873e9143535e02
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2019
ms.locfileid: "2748717"
---
# <a name="sample-rollup-goal-data-for-a-custom-period-against-the-target-revenue"></a>Beispiel: Rollup-Zieldaten für eine benutzerdefinierte Periode für den Zielumsatz

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/sample-rollup-goal-data-custom-period-target-revenue -->

Dieses Beispiel zeigt, wie für Zieldaten während einer benutzerdefinierten Periode für den Zielumsatz ein Rollup durchgeführt wird. Sie können das Beispiel [hier](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/RollupGoalData) herunterladen.

Dieses Beispiel benötigt weitere drei Benutzer, die nicht in Ihrem System sind. Erstellen Sie die drei erforderliche Benutzer manuell **wie besehen** (siehe unten) in **Office 365**. Ersetzen Sie `yourorg` durch den Namen Ihrer Organisation.

**Vorname**: Nancy<br/>
**Nachname**: Anderson<br/>
**Sicherheitsrolle**: Vertriebsmitarbeiter<br/>
**Benutzername**: nanderson@yourorg.onmicrosoft.com<br/>

**Vorname**: David<br/>
**Nachname**: Bristol<br/>
**Sicherheitsrolle**: Vertriebsmitarbeiter<br/>
**Benutzername**: dbristol@yourorg.onmicrosoft.com<br/>

**Vorname**: Kevin<br/>
**Nachname**: Cook<br/>
**Sicherheitsrolle**: Vertriebsmanager<br/>
**Benutzername**: kcook@yourorg.onmicrosoft.com<br/>

## <a name="how-to-run-this-sample"></a>Wie man dieses Beispiel ausführt

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>Funktionsweise:

Dieses Beispiel zeigt, wie für Zieldaten während einer benutzerdefinierten Periode für den Zielumsatz ein Rollup durchgeführt wird.

## <a name="how-this-sample-works"></a>Wie dieses Beispiel funktioniert

Um das unter [Was macht dieses Beispiel](#what-this-sample-does), beschriebene Szenario zu simulieren, geht das Beispiel wie folgt vor:

### <a name="setup"></a>Einrichten

1. Tests für die Version der Organisation.
2. Ruft den Vertriebsmanager und 2 Vertriebsmitarbeiter ab, die manuell in **Office 365** erstellt werden.
3. Erstellt eine Beispieleinheitengruppe und ruft die Standardeinheits-ID ab. 
4. Erstellt einige Produkte und eine neue Rabattliste.
5. `PriceLevel` erstellt die Preisliste.
6. `ProductPriceLevel` erstellt ein Preislistenelement für das erste Produkt und wendet den Mengenrabatt an.
7. Erstellt einen Account-Datensatz für die potenzielle Kunden-ID der Verkaufschance.
8. Erstellt eine neue Verkaufschance mit dem vom Benutzer angegebenen geschätzten Umsatz.
9. Erstellt einen Produktkatalog und überschreibt den Listenpreis.
10. Erstellt ein neues einzutragendes Verkaufschancenprodukt mit einem manuell angewandten Rabatt.

### <a name="demonstrate"></a>Demonstrieren

1. Erstellt eine Metrik und stellt als Betragsdatentyp `Money` ein.
2. Erstellt Rollupfelder, die auf die Schätzwerte und die tatsächlichen Werte abzielen.
3. `GoalRollupQuery` erstellt die Zielrollup-Abfragen zum Auffinden von Verkaufschancen im Bereich des Vertriebsmitarbeiters. 
4. Erstellt drei Ziele, ein übergeordnetes Ziel und zwei untergeordnete Ziele.
5. `RecalculateRequest` berechnet den Rollup für Ziele. 

### <a name="clean-up"></a>Bereinigung

1. Zeigt eine Option an, um die Beispieldaten zu löschen, die in [Einrichtung](#setup)erstellt wurden.

    Das Löschen ist optional, falls Sie die Entitäten und Daten durchsuchen möchten, die durch das Beispiel erstellt wurden. Sie können die Datensätze manuell löschen, um das gleiche Ergebnis zu erzielen.
