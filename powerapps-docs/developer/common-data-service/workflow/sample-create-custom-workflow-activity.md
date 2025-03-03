---
title: 'Beispiel: Eine benutzerdefinierte Workflowaktivität erstellen (Common Data Service) | Microsoft-Dokumentation'
description: Dieses Beispiel zeigt, wie Sie eine benutzerdefinierte Workflowaktivität schreiben, die eine neue Firma sowie eine Aufgabe für die Firma erstellen kann. Dieses Beispiel verwendet frühere Bindungen.
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: samples
applies_to:
- Dynamics 365 (online)
ms.assetid: 6d498e86-8702-43ed-bf76-96d1b4246dfd
caps.latest.revision: 26
author: JimDaly
ms.author: jdaly
manager: amyla
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: f903726480068d0d5796ee51a9f442093d472290
ms.sourcegitcommit: 8185f87dddf05ee256491feab9873e9143535e02
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2019
ms.locfileid: "2748336"
---
# <a name="sample-create-a-custom-workflow-activity"></a>Beispiel: Eine benutzerdefinierte Workflowaktivität erstellen

Laden Sie hier das vollständige Beispiel herunter [Benutzerdefiniertes Workflowaktivitätsbeispiel](https://code.msdn.microsoft.com/Custom-Workflow-Activities-eee57285). 

## <a name="prerequisites"></a>Voraussetzungen

[!INCLUDE [sdk-prerequisite](../../../includes/sdk-prerequisite.md)]

  
## <a name="requirements"></a>Anforderungen  

<!-- TODO: This sample will not use the SDK helper classes -->
  
## <a name="demonstrates"></a>Demonstriert  

Dieses Beispiel zeigt, wie Sie eine benutzerdefinierte Workflowaktivität schreiben, die eine neue Firma sowie eine Aufgabe für die Firma erstellen kann. Dieses Beispiel verwendet frühere Bindungen.  
  
## <a name="example"></a>Beispiel  

```csharp
using System;
using System.Activities;
using System.Collections.ObjectModel;

using Microsoft.Crm.Sdk.Messages;

using Microsoft.Xrm.Sdk;
using Microsoft.Xrm.Sdk.Messages;
using Microsoft.Xrm.Sdk.Query;
using Microsoft.Xrm.Sdk.Workflow;

namespace Microsoft.Crm.Sdk.Samples
{
    public sealed class SimpleSdkActivity : CodeActivity
    {
        protected override void Execute(CodeActivityContext executionContext)
        {
            //Create the tracing service
            ITracingService tracingService = executionContext.GetExtension<ITracingService>();

            //Create the context
            IWorkflowContext context = executionContext.GetExtension<IWorkflowContext>();
            IOrganizationServiceFactory serviceFactory = executionContext.GetExtension<IOrganizationServiceFactory>();
            IOrganizationService service = serviceFactory.CreateOrganizationService(context.UserId);

            tracingService.Trace("Creating Account");

            Account entity = new Account();
            entity.Name = AccountName.Get<string>(executionContext);
            Guid entityId = service.Create(entity);

            tracingService.Trace("Account created with Id {0}", entityId.ToString());

            tracingService.Trace("Create a task for the account");
            Task newTask = new Task();
            newTask.Subject = TaskSubject.Get<string>(executionContext);
            newTask.RegardingObjectId = new EntityReference(Account.EntityLogicalName, entityId);

            Guid taskId = service.Create(newTask);

            tracingService.Trace("Task has been created");

            tracingService.Trace("Retrieve the task using QueryByAttribute");
            QueryByAttribute query = new QueryByAttribute();
            query.Attributes.AddRange(new string[] { "regardingobjectid" });
            query.ColumnSet = new ColumnSet(new string[] { "subject" });
            query.EntityName = Task.EntityLogicalName;
            query.Values.AddRange(new object[] { entityId });

            tracingService.Trace("Executing the Query for entity {0}", query.EntityName);

            //Execute using a request to test the OOB (XRM) message contracts
            RetrieveMultipleRequest request = new RetrieveMultipleRequest();
            request.Query = query;
            Collection<Entity> entityList = ((RetrieveMultipleResponse)service.Execute(request)).EntityCollection.Entities;

            //Execute a request from the CRM message assembly
            tracingService.Trace("Executing a WhoAmIRequest");
            service.Execute(new WhoAmIRequest());

            if (1 != entityList.Count)
            {
                tracingService.Trace("The entity list was too long");
                throw new InvalidPluginExecutionException("Query did not execute correctly");
            }
            else
            {
                tracingService.Trace("Casting the Task from RetrieveMultiple to strong type");
                Task retrievedTask = (Task)entityList[0];

                if (retrievedTask.ActivityId != taskId)
                {
                    throw new InvalidPluginExecutionException("Incorrect task was retrieved");
                }

                tracingService.Trace("Retrieving the entity from IOrganizationService");

                //Retrieve the task using Retrieve
                retrievedTask = (Task)service.Retrieve(Task.EntityLogicalName, retrievedTask.Id, new ColumnSet("subject"));
                if (!string.Equals(newTask.Subject, retrievedTask.Subject, StringComparison.Ordinal))
                {
                    throw new InvalidPluginExecutionException("Task's subject did not get retrieved correctly");
                }

                //Update the task
                retrievedTask.Subject = UpdatedTaskSubject.Get<string>(executionContext);
                service.Update(retrievedTask);
            }
        }

        [Input("Account Name")]
        [Default("Test Account: {575A8B41-F8D7-4DCE-B2EA-3FFDE936AB1B}")]
        public InArgument<string> AccountName { get; set; }

        [Input("Task Subject")]
        [Default("Task related to account {575A8B41-F8D7-4DCE-B2EA-3FFDE936AB1B}")]
        public InArgument<string> TaskSubject { get; set; }

        [Input("Updated Task Subject")]
        [Default("UPDATED: Task related to account {575A8B41-F8D7-4DCE-B2EA-3FFDE936AB1B}")]
        public InArgument<string> UpdatedTaskSubject { get; set; }
    }

    public sealed class SdkWithLooselyTypesActivity : CodeActivity
    {
        protected override void Execute(CodeActivityContext executionContext)
        {
            //Create the tracing service
            ITracingService tracingService = executionContext.GetExtension<ITracingService>();

            //Create the context
            IWorkflowContext context = executionContext.GetExtension<IWorkflowContext>();
            IOrganizationServiceFactory serviceFactory = executionContext.GetExtension<IOrganizationServiceFactory>();
            IOrganizationService service = serviceFactory.CreateOrganizationService(context.UserId);

            tracingService.Trace("Creating Account");

            tracingService.Trace("Creating Account");

            Entity entity = new Entity("account");
            entity.Attributes["name"] = AccountName.Get<string>(executionContext);
            Guid entityId = service.Create(entity);

            tracingService.Trace("Account created with Id {0}", entityId.ToString());

            tracingService.Trace("Create a task for the account");
            Entity newTask = new Entity("task");
            newTask["subject"] = TaskSubject.Get<string>(executionContext);
            newTask["regardingobjectid"] = new EntityReference("account", entityId);

            Guid taskId = service.Create(newTask);

            tracingService.Trace("Task has been created");

            Entity updateTask = new Entity("task");
            updateTask.Id = taskId;
            updateTask["subject"] = UpdatedTaskSubject.Get<string>(executionContext);
            service.Update(updateTask);

            tracingService.Trace("Task has been updated");
        }

        [Input("Account Name")]
        [Default("Test Account: {575A8B41-F8D7-4DCE-B2EA-3FFDE936AB1B}")]
        public InArgument<string> AccountName { get; set; }

        [Input("Task Subject")]
        [Default("Task related to account {575A8B41-F8D7-4DCE-B2EA-3FFDE936AB1B}")]
        public InArgument<string> TaskSubject { get; set; }

        [Input("Updated Task Subject")]
        [Default("UPDATED: Task related to account {575A8B41-F8D7-4DCE-B2EA-3FFDE936AB1B}")]
        public InArgument<string> UpdatedTaskSubject { get; set; }
    }

    public sealed class SimpleSdkWithRelatedEntitiesActivity : CodeActivity
    {
        protected override void Execute(CodeActivityContext executionContext)
        {
            //Create the tracing service
            ITracingService tracingService = executionContext.GetExtension<ITracingService>();

            //Create the context
            IWorkflowContext context = executionContext.GetExtension<IWorkflowContext>();
            IOrganizationServiceFactory serviceFactory = executionContext.GetExtension<IOrganizationServiceFactory>();
            IOrganizationService service = serviceFactory.CreateOrganizationService(context.UserId);

            Relationship primaryContactRelationship = new Relationship("account_primary_contact");

            Guid primaryContactId = service.Create(new Contact() { LastName = RootContactLastName.Get<string>(executionContext) });

            //tracingService.Trace("Create an Account with an existing primary contact");
            Account rootAccount = new Account() { Name = RelatedAccountName.Get<string>(executionContext) };
            Contact primaryContact = new Contact()
            {
                EntityState = EntityState.Changed,
                Id = primaryContactId,
                FirstName = RootContactFirstName.Get<string>(executionContext)
            };

            rootAccount.RelatedEntities[primaryContactRelationship] =
                new EntityCollection(new Entity[] { primaryContact }) { EntityName = Contact.EntityLogicalName };

            tracingService.Trace("Execute the Create/Update");
            rootAccount.Id = service.Create(rootAccount);

            //Create the related entities query
            RelationshipQueryCollection retrieveRelatedEntities = new RelationshipQueryCollection();
            retrieveRelatedEntities[primaryContactRelationship] = new QueryExpression(Account.EntityLogicalName)
            {
                ColumnSet = new ColumnSet("name"),
                Criteria = new FilterExpression()
            };

            //Create the request
            RetrieveResponse response = (RetrieveResponse)service.Execute(new RetrieveRequest()
            {
                ColumnSet = new ColumnSet("firstname"),
                RelatedEntitiesQuery = retrieveRelatedEntities,
                Target = new EntityReference(primaryContact.LogicalName, primaryContact.Id)
            });

            tracingService.Trace("Retrieve the record with its related entities");
            Contact retrievedContact = (Contact)response.Entity;
            Account retrievedAccount = (Account)retrievedContact.RelatedEntities[primaryContactRelationship][0];

            tracingService.Trace("Ensure the first name was updated");
            if (retrievedContact.FirstName == primaryContact.FirstName)
            {
                tracingService.Trace("Primary Contact name is correct");
            }
            else
            {
                tracingService.Trace("First Name is \"{0}\", expected \"{1}\".", retrievedContact.FirstName, primaryContact.FirstName);
                throw new InvalidPluginExecutionException("The first name was not changed");
            }
        }

        [Input("Related Account Name")]
        [Default("Related Account")]
        public InArgument<string> RelatedAccountName { get; set; }

        [Input("Root Contact First Name")]
        [Default("New FirstName")]
        public InArgument<string> RootContactFirstName { get; set; }

        [Input("Root Contact Last Name")]
        [Default("Root LastName")]
        public InArgument<string> RootContactLastName { get; set; }
    }
}
```
  
### <a name="see-also"></a>Siehe auch 
 
[Workflowerweiterungen](workflow-extensions.md)<br />
[Lernprogramm: Erstellen einer Workflow-Erweiterung](tutorial-create-workflow-extension.md)<br />
[Beispiel: Aktualisieren des nächsten Geburtstags mithilfe einer benutzerdefinierten Workflowaktivität](sample-update-next-birthday-using-custom-workflow-activity.md)<br />
[Beispiel: Berechnen Sie mit einer benutzerdefinierten Workflowaktivität einen Kreditscore](sample-calculate-credit-score-custom-workflow-activity.md)

