---
title: Behandlung von Ausnahmen in Ihrem Code (Common Data Service) | Microsoft Docs
description: In diesem Artikel werden die Ausnahmen erläutert, die von einem Common Data Service-Webdienst-Methodenaufruf zurückgegeben werden. Durch das Beispiel in diesem Artikel werden die allgemeinen Fehler und Ausnahmen hervorgehoben, die Ihr Anwendungsentwurf behandeln sollte.
ms.custom: ''
ms.date: 06/17/2019
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: JimDaly
ms.author: jdaly
manager: ryjones
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 1888da184a7452ddaee79bdcf9dad0817a36befa
ms.sourcegitcommit: d9cecdd5a35279d78aa1b6c9fc642e36a4e4612c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "2752934"
---
# <a name="handle-exceptions-in-your-code"></a>Behandlung von Ausnahmen in Ihrem Code

Es gibt mehrere Ausnahmen, die von einem Common Data Service Webdienstmethodenaufruf zurückgegeben werden können. Ihr Anwendungsentwurf muss diese Ausnahmen abfangen und geeignet behandeln. In SDK .NET-Assemblys verwenden alle Webdienstmethodenanrufe einen Kommunikationskanal zum Server auf Basis der Windows Communication Foundation-Technologie. In WCF-Begriffen werden heißen die vom Kanal zurückgegebenen Ausnahmen *Fehler*.  

<a name="BKMK_Common"></a>   

## <a name="common-exceptions-and-faults"></a>Häufige Ausnahmen und Fehler  

Der folgende Code ist in den meisten Common Data Service-Webdienstbeispielen verwendet. Es werden die allgemeinen Fehler und Ausnahmen hervorgehoben, die Ihr Anwendungsentwurf behandeln sollte.  
  
```csharp
catch (FaultException<Microsoft.Xrm.Sdk.OrganizationServiceFault> ex)
{
    Console.WriteLine("The application terminated with an error.");
    Console.WriteLine("Timestamp: {0}", ex.Detail.Timestamp);
    Console.WriteLine("Code: {0}", ex.Detail.ErrorCode);
    Console.WriteLine("Message: {0}", ex.Detail.Message);
    Console.WriteLine("Inner Fault: {0}",
        null == ex.Detail.InnerFault ? "No Inner Fault" : "Has Inner Fault");
}
catch (System.TimeoutException ex)
{
    Console.WriteLine("The application terminated with an error.");
    Console.WriteLine("Message: {0}", ex.Message);
    Console.WriteLine("Stack Trace: {0}", ex.StackTrace);
    Console.WriteLine("Inner Fault: {0}",
        null == ex.InnerException.Message ? "No Inner Fault" : ex.InnerException.Message);
}
catch (System.Exception ex)
{
    Console.WriteLine("The application terminated with an error.");
    Console.WriteLine(ex.Message);

    // Display the details of the inner exception.
    if (ex.InnerException != null)
    {
        Console.WriteLine(ex.InnerException.Message);

        FaultException<Microsoft.Xrm.Sdk.OrganizationServiceFault> fe = ex.InnerException
            as FaultException<Microsoft.Xrm.Sdk.OrganizationServiceFault>;
        if (fe != null)
        {
            Console.WriteLine("Timestamp: {0}", fe.Detail.Timestamp);
            Console.WriteLine("Code: {0}", fe.Detail.ErrorCode);
            Console.WriteLine("Message: {0}", fe.Detail.Message);
            Console.WriteLine("Trace: {0}", fe.Detail.TraceText);
            Console.WriteLine("Inner Fault: {0}",
                null == fe.Detail.InnerFault ? "No Inner Fault" : "Has Inner Fault");
        }
    }
}
```
  
> [!NOTE]
>  Wenn Sie auf den Suchdienst-Webdienst zugreifen, sollte Ihr Code <xref:Microsoft.Xrm.Sdk.DiscoveryServiceFault> anstelle des Fehlers <xref:Microsoft.Xrm.Sdk.OrganizationServiceFault> abfangen, zuvor angezeigt wurde.  
  
Neben zu diesen Fehlern und Ausnahmen muss Ihr Code die folgenden Ausnahmen behandeln:  
  
- [SecurityTokenValidationException](/dotnet/api/system.identitymodel.tokens.securitytokenvalidationexception)  
- [ExpiredSecurityTokenException](/dotnet/api/system.servicemodel.security.expiredsecuritytokenexception)  
- [SecurityAccessDeniedException](/dotnet/api/system.servicemodel.security.securityaccessdeniedexception)  
- [MessageSecurityException](/dotnet/api/system.servicemodel.security.messagesecurityexception)  
- [SecurityNegotiationException](/dotnet/api/system.servicemodel.security.securitynegotiationexception)  
  
Wenn Sie sich mit Common Data Service verbinden, wird eine `SecurityAccessDeniedException`-Ausnahme ausgelöst, wenn Sie ein gültiges Microsoft-Konto verwenden und Ihr Konto nicht einer Common Data Service-Organisation zugeordnet ist. Ein  `MessageSecurityException`  kann ausgelöst werden, wenn das  Microsoft-Konto nicht gültig ist, oder ein Authentifizierungsfehler vorlag.  
  
<a name="BKMK_BusinessRuleErrors"></a>

## <a name="custom-errors-from-business-rules"></a>Benutzerdefinierte Fehler von Unternehmensregeln
 
Mit Common Data Service können Anpasser Geschäftsregeln erstellen, die auf dem Server ausgewertet werden. Anpasser können Fehlermeldungen basierend auf den Anforderungen, die in der Geschäftsregel festgelegt wurden. Entwickler können darauf achten,  robuste Fehlerbehandlung in ihrem Code einzuschließen, um diese Ausnahmen abzufangen und zu behandeln.  
  
Das Folgende ist ein Beispiel für das Ablaufverfolgungsprotokoll, das erstellt wird, wenn einer dieser Fehler von einer Geschäftsregel namens **Name der entitätsweiten Geschäftsregel, die eine Fehler zurückgibt** und die Fehlermeldung **benutzerdefinierte Fehlermeldung**.  
  
```csharp
Unhandled Exception: System.ServiceModel.FaultException`1[[Microsoft.Xrm.Sdk.OrganizationServiceFault, Microsoft.Xrm.Sdk, Version=7.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35]]: custom error messageDetail:   
<OrganizationServiceFault xmlns:i="https://www.w3.org/2001/XMLSchema-instance" xmlns="https://schemas.microsoft.com/xrm/2011/Contracts">  
  <ErrorCode>-2147220891</ErrorCode>  
  <ErrorDetails xmlns:d2p1="https://schemas.datacontract.org/2004/07/System.Collections.Generic">  
    <KeyValuePairOfstringanyType>  
      <d2p1:key>OperationStatus</d2p1:key>  
      <d2p1:value xmlns:d4p1="https://www.w3.org/2001/XMLSchema" i:type="d4p1:string">0</d2p1:value>  
    </KeyValuePairOfstringanyType>  
    <KeyValuePairOfstringanyType>  
      <d2p1:key>SubErrorCode</d2p1:key>  
      <d2p1:value xmlns:d4p1="https://www.w3.org/2001/XMLSchema" i:type="d4p1:string">-2146233088</d2p1:value>  
    </KeyValuePairOfstringanyType>  
  </ErrorDetails>  
  <Message>custom error message</Message>  
  <Timestamp>2014-09-04T17:43:16.8197965Z</Timestamp>  
  <InnerFault i:nil="true" />  
  <TraceText>  
  
[Microsoft.Crm.ObjectModel: Microsoft.Crm.ObjectModel.SyncWorkflowExecutionPlugin]  
[cf6a25a9-5a34-e411-80b9-00155dd8c20f: ]  
Starting sync workflow 'Name of Entity Scope Business Rule returning Error', Id: c76a25a9-5a34-e411-80b9-00155dd8c20f  
Entering ConditionStep1_step:   
Entering SetMessage_step:   
Sync workflow 'Name of Entity Scope Business Rule returning Error' terminated with error 'custom error message'  
  
</TraceText>  
</OrganizationServiceFault>  
```  
  
Weitere Informationen finden Sie unter [Erstellen einer Geschäftsregel für eine Entität](../../../maker/common-data-service/data-platform-create-business-rule.md)  
  
<a name="BKMK_AdditionalInfo"></a>

## <a name="additional-information-about-exceptions"></a>Zusätzliche Informationen zu Ausnahmen

Falls eine nicht abgefangene Ausnahme ausgelöst wird, die vertrauliche Informationen enthält, für die der Benutzer nicht über die Berechtigung zum Anzeigen besitzt, werden die vertraulichen Informationen für den Benutzer ausgeblendet und eine Referenznummer wird bereitgestellt. Diese Referenznummer verweist auf den zugehörigen Serverereignisprotokolleintrag und Serverablaufverfolgungseintrag. Ein Systemadministrator kann die Einträge aufsuchen und weitere Informationen zu der Ausnahme finden.  
  
### <a name="see-also"></a>Siehe auch  

 [Webdienst-Fehlercodes](web-service-error-codes.md)   
 [Behandlung von Ausnahmen in Plug-ins](../handle-exceptions.md)   
 [.NET Framework Developer Center](https://docs.microsoft.com/dotnet/framework/development-guide)