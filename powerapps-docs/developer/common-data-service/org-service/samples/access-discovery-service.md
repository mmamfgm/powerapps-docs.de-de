---
title: 'Beispiel: Arbeiten mit Suchdienst <Topic Title> (Common Data Service) | Microsoft Docs'
description: Dieser Beispielcode zeigt, wie Sie Suchdienste verwenden können.
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
ms.openlocfilehash: 3f707eef358454053436d633c4ad48e30348ea17
ms.sourcegitcommit: 8185f87dddf05ee256491feab9873e9143535e02
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2019
ms.locfileid: "2748390"
---
# <a name="sample-access-the-discovery-service"></a>Beispiel: Zugreifen auf den Suchdienst

Dieser Beispielcode zeigt, wie Sie den Suchdienst mit SDK-Assemblies verwenden können. Sie können das Beispiel [hier](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/DiscoveryService) herunterladen.

## <a name="how-to-run-this-sample"></a>Wie man dieses Beispiel ausführt

Dieses Beispiel öffnet keinen Dialog, um Sie nach Verbindungsinformationen zu fragen.

Wenn Sie `Username`- und `Password`-Werte in den App.config-Verbindungszeichenfolgen festgelegt haben, werden diese verwendet. Andernfalls müssen Sie `username` und `password` Variablen in der `SampleProgram.Main`-Methode festlegen.

## <a name="what-this-sample-does"></a>Funktionsweise:

Dieses Beispiel verwendet die SDK Assembly `DiscoveryServiceProxy`, um den Suchdienst mit den Anmeldeinformationen eines Benutzers abzufragen, um festzustellen, mit welchen Umgebungen er sich verbinden kann.

Wenn eine oder mehrere Umgebungen zurückgegeben werden, fordert das Beispiel den Benutzer auf, eine auszuwählen und verwendet dann ein `WhoAmIRequest`, um das `SystemUser.UserId` für diese Umgebung zurückzugeben.

## <a name="how-this-sample-works"></a>Wie dieses Beispiel funktioniert

Um das unter [Was macht dieses Beispiel](#what-this-sample-does), beschriebene Szenario zu simulieren, geht das Beispiel wie folgt vor:

### <a name="setup"></a>Einrichten

Dieses Beispiel erfordert keine spezielle Konfiguration, außer dass es einen gültigen Benutzernamen und ein gültiges Passwort für die Benutzeranmeldung gibt.

Wenn Sie das regionale Rechenzentrum kennen, in dem sich Ihre Umgebungen befinden, wird das Beispiel schneller laufen, wenn Sie diesen Wert in Zeile 40 der Datei SampleProgram.cs festlegen.

In SampleMethods.cs gibt es eine `DataCenter` Enumeration für jedes der bekannten Rechenzentren. Jedes Enumerationsmitglied ist mit einer `Description`-Notation versehen. Alle diese Mitglieder mit Ausnahme von `Unknown` haben die URL für den regionalen Suchdienst als Beschreibung. 


### <a name="demonstrate"></a>Demonstrieren

1. Unter Verwendung der Benutzer-Anmeldeinformationen und des `dataCenter`-Wertes verwendet das Programm die statische `GetAllOrganizations`-Methode, um alle bekannten Umgebungen für den Benutzer abzurufen.
1. Das `GetAllOrganizations`-Verfahren erkennt, ob der `dataCenter`-Wert auf `DataCenter.Unknown` gesetzt ist. Wenn es auf dieses Element gesetzt ist, wird diese Methode alle anderen Elemente in der `DataCenter`-Enumeration durchlaufen und alle Umgebungen abrufen, die mit der statischen `GetOrganizationsForDataCenter`-Methode gefunden werden.

    Wenn ein bestimmtes Rechenzentrum festgelegt ist, ruft `GetAllOrganizations` einfach `GetOrganizationsForDataCenter` mit diesen Werten an.

1. Die `GetOrganizationsForDataCenter`-Methode extrahiert die Rechenzentrum-Suchdienst-Url aus der Mitglied `Description`-Dekoration und verwendet sie zusammen mit den Benutzer-Anmeldeinformationen, um die `RetrieveOrganizationsRequest`-Suchdienstmeldung auszuführen.

    Ein `System.ServiceModel.Security.SecurityAccessDeniedException` wird erwartet, wenn der Benutzer keine Umgebungen in einem bestimmten Rechenzentrum hat.

1. Wenn Umgebungen nach der `GetAllOrganizations`-Methode zurückgegeben werden, werden sie in der Konsole aufgelistet und Sie werden aufgefordert, eine durch Eingabe einer Zahl auszuwählen. Wenn Ihre Auswahl gültig ist, werden die ausgewählten Umgebungsdaten verwendet, um einen `WhoAmIRequest` auszuführen und den `SystemUser.UserId` für den Benutzer in dieser Umgebung zurückzugeben.

### <a name="clean-up"></a>Bereinigung

Dieses Beispiel erstellt keine Datensätze. Keine Bereinigung erforderlich
