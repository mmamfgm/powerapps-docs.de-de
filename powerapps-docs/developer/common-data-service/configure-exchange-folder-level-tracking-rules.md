---
title: Regeln für die Exchange-Nachverfolgung auf Ordnerebene konfigurieren (Common Data Service) | Microsoft-Dokumentation
description: Erfahren Sie, wie die Regeln für die Exchange-Nachverfolgung auf Ordnerebene zu konfigurieren.
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: mayadumesh
ms.author: jdaly
manager: ryjones
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 09b7d273968f2d37b45ca5210924546a8bee6cd9
ms.sourcegitcommit: 8185f87dddf05ee256491feab9873e9143535e02
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2019
ms.locfileid: "2748574"
---
# <a name="configure-exchange-folder-level-tracking-rules"></a>Konfigurieren der Regeln für die Nachverfolgung auf Ordnerebene

Konfigurieren Sie Regeln für die Nachverfolgung auf Ordnerebene, um einen Microsoft Exchange-Posteingangsorder einem Common Data Service-Datensatz zuzuordnen, damit alle E-Mails im Microsoft Exchange-Ordner automatisch für den zugeordneten Datensatz in Common Data Service nachverfolgt werden. Nachverfolgung von E-Mails auf Ordnerebene funktioniert nur, wenn Folgendes zutrifft:  

- Die Nachverfolgungsfunktion auf Ordnerebene für Ihre Common Data Service-Instanz ist aktiviert. Sie können Nachverfolgung auf Ordnerebene aktivieren, indem Sie den Webclient oder Dynamics 365 for Outlook verwenden. Weitere Informationen: [Nachverfolgung auf Ordnerebene konfigurieren](/dynamics365/customer-engagement/admin/configure-outlook-exchange-folder-level-tracking)  

- Der Ordner, den Sie nachverfolgen, wird unter dem Ordner **Posteingang** in Microsoft Exchange angezeigt. E-Mails in den Ordnern, die nicht unter dem Ordner **Posteingang** sind, werden nicht nachverfolgt.  

<a name="Create"></a>   

## <a name="create-and-manage-folder-level-tracking-rules"></a>Erstellen und Verwalten von Nachverfolgungsregeln auf Ordnerebene 
 
 Verwenden Sie die [MailboxTrackingFolder-Entität](/reference/entities/mailboxtrackingfolder.md), um die Nachverfolgungsregeln auf Ordnerebene programmgesteuert zu konfigurieren und zu verwalten. Um eine Nachverfolgungsregel einzurichten, verwenden Sie die folgenden Attribute.  


|                                   Attribut                                   |                                                                                                                                                                                                                Beschreibung                                                                                                                                                                                                                 |
|-------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  [ExchangeFolderId](/reference/entities/mailboxtrackingfolder.md#BKMK_ExchangeFolderId)  | Geben Sie die Microsoft Exchange-Ordner-ID, die Sie zuordnen möchten. Sie können Exchange Web Services (EWS) verwenden, um die ID eines Ordners unter Ihrem Posteingangsordner abzurufen. Weitere Informationen finden Sie unter [MSDN: How to: Work with folders by using EWS in Exchange](https://msdn.microsoft.com/library/office/dn535504.aspx). Dies ist ein erforderliches Attribut. |
|         [MailboxId](/reference/entities/mailboxtrackingfolder.md#BKMK_MailboxId)         |                                                                                                                                         Geben Sie die Postfach-ID in Common Data Service ein, für die Sie die Regel erstellen möchten. Dies ist ein erforderliches Attribut.                                                                                                                                          |
| [RegardingObjectId](/reference/entities/mailboxtrackingfolder.md#BKMK_RegardingObjectId) |                                                                                                       Legen Sie das entsprechende Objekt in Common Data Service fest, dem der angegebene Microsoft Exchange-Ordner zugeordnet werden soll. Dies ist ein optionales Attribut.                                                                                                       |

 Der folgende Beispielcode zeigt, wie Sie eine Nachverfolgungsregel auf Ordnerebene erstellen können.  

```csharp  
// Create a folder-level tracking rule  
MailboxTrackingFolder newTrackingFolder = new MailboxTrackingFolder();  

// Set the required attributes  
newTrackingFolder.ExchangeFolderId = "123456"; // Sample value. Retrieve this value using Exchange Web Services (EWS)  
newTrackingFolder.MailboxId = new EntityReference(Mailbox.EntityLogicalName, _mailboxId);  

// Set the optional attributes  
newTrackingFolder.RegardingObjectId = new EntityReference(Account.EntityLogicalName, _accountId);  
newTrackingFolder.RegardingObjectId.Name = _accountName;  
newTrackingFolder.ExchangeFolderName = "Sample Exchange Folder";  

// Execute the request to create the rule   
_folderTrackingId = _serviceProxy.Create(newTrackingFolder);  
Console.WriteLine("Created folder-level tracking rule for '{0}'.\n", _mailboxName);  
```  

 Sie können ein Maximum von 25 Nachverfolgungsregeln auf Ordnerebene pro Postfach erstellen. Die Ordner-ID des Microsoft Exchange-Ordners kann zum Zeitpunkt des Erstellens der Zuordnung mithilfe des SDK nicht überprüft werden. Sobald Sie jedoch eine Zuordnungsregel erstellen und wenn die Ordner-ID ungültig ist, wird Sie in der Benutzeroberfläche in Common Data Service angezeigt, um anzugeben, dass die Zuordnung ungültig ist.  

 Alle manuellen Änderungen am Bezugs-Objekt in den nachverfolgten Aktivitätsdatensätzen, die in Common Data Service infolge der Nachverfolgungsregel auf Ordnerebene erstellt werden, werden bei der nächsten serverseitigen Synchronisierung überschrieben. Wenn Sie beispielsweise eine Zuordnung zwischen dem `Adventure Works`-Ordner und dem `Adventure Works`-Konto erstellt haben, werden alle E-Mails im `Adventure Works`Microsoft Exchange-Ordner als Aktivitäten in Common Data Service nachverfolgt, wobei der Bezug auf den `Adventure Works`-Kontodatensatz festgelegt wird. Wenn Sie den Bezug einiger Aktivtäten in einen anderen Datensatz ändern, wird er automatisch bei der nächsten serverseitigen Synchronisierung überschrieben.  

<a name="Retrieve"></a>   

## <a name="retrieve-folder-level-tracking-rules-for-a-mailbox"></a>Abrufen von Nachverfolgungsregeln auf Ordnerebene für ein Postfach  

 Sie können alle Nachverfolgungsregeln auf Ordnerebene für Postfach abrufen, indem Sie die Meldung <xref:Microsoft.Crm.Sdk.Messages.RetrieveMailboxTrackingFoldersRequest> verwenden. Führen Sie das Postfach ID, für die Sie die Regeln in anzeigen möchten <xref:Microsoft.Crm.Sdk.Messages.RetrieveMailboxTrackingFoldersRequest>.<xref:Microsoft.Crm.Sdk.Messages.RetrieveMailboxTrackingFoldersRequest.MailboxId> Eigenschaft und die Nachticht ausführen.  

 Der folgende Beispielcode zeigt, wie Sie eine Nachverfolgungsregel auf Ordnerebene für ein Postfach abrufen können.  

```csharp  
// Retrieve the folder mapping rules for a mailbox  
RetrieveMailboxTrackingFoldersRequest req = new RetrieveMailboxTrackingFoldersRequest  
{  
    MailboxId = _mailboxId.ToString()  
};  

RetrieveMailboxTrackingFoldersResponse resp = (RetrieveMailboxTrackingFoldersResponse_serviceProxy.Execute(req);  
Console.WriteLine("Retrieved folder-level tracking rules for {0}:", _mailboxName);  
int n = 1;  
foreach (var folderMapping in resp.MailboxTrackingFolderMappings)  
{  
    Console.WriteLine("\tRule {0}: '{1}' is mapped to '{2}'.",   
        n, folderMapping.ExchangeFolderName, folderMapping.RegardingObjectName);  
    n++;  
}  
```  

### <a name="see-also"></a>Siehe auch  
 <xref href="Microsoft.Dynamics.CRM.RetrieveMailboxTrackingFolders?text=RetrieveMailboxTrackingFolders Function" /><br />
 [MailboxTrackingFolder-Entität](/reference/entities/mailboxtrackingfolder.md)<br />
 [Postfach-Entität](/reference/entities/mailbox.md)<br />
 [Nachverfolgung auf Ordnerebene konfigurieren](/dynamics365/customer-engagement/admin/configure-outlook-exchange-folder-level-tracking)<br />
 [Serverseitige Synchronisierungsentitäten](server-side-synchronization-entities.md)<br />
