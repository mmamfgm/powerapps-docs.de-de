---
title: Schreiben einer Listener-Anwendung für eine Microsoft Azure-Lösung (Common Data Service) | Microsoft Docs
description: In diesem Thema wird beschrieben, wie Sie eine Azure-Lösungs-Listener-Anwendung schreiben, die Common Data Service-Nachrichten lesen und verarbeiten kann, die für Azure Service Bus veröffentlicht werden.
keywords: ''
ms.date: 10/06/2019
ms.service: powerapps
ms.topic: article
ms.assetid: cf68e0a9-c240-59e7-c501-68cbfa0df455
author: JimDaly
ms.author: jdaly
manager: ryjones
ms.reviewer: ''
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: e4247a7561bc0fc2116030737db72f99390f46c3
ms.sourcegitcommit: 8185f87dddf05ee256491feab9873e9143535e02
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2019
ms.locfileid: "2748339"
---
# <a name="write-a-listener-application-for-a-azure-solution"></a>Schreiben einer Listener-Anwendung für eine Azure-Lösung

In diesem Thema wird beschrieben, wie Sie eine Azure-Lösungs-Listener-Anwendung schreiben, die Common Data Service-Nachrichten lesen und verarbeiten kann, die für Azure Service Bus veröffentlicht werden. Sie sollten sich zunächst damit vertraut machen, wie Sie einen Azure Service Bus-Listener schreiben, bevor Sie sich den Besonderheiten eines Common Data Service-Listeners zuwenden. Weitere Informationen bietet die [Dokumentation zu Azure Service Bus](/azure/service-bus/).
  
<a name="bkmk_writequeued"></a>

## <a name="write-a-queue-listener"></a>Warteschlangenlistener schreiben

Eine Nachrichten-*Warteschlange* ist eine Sammlung von Nachrichten, die an einem Servicebusendpunkt empfangen wurden. Ein *Warteschlangenlistener* ist eine Anwendung, die diese Nachrichten in der Warteschlange liest und verarbeitet. Da die Servicebusnachrichten in einer Warteschlange gespeichert werden, muss ein Listener nicht aktiv lauschen, damit Nachrichten in einer Warteschlange empfangen werden können. Ein Warteschlangenlistener kann gestartet werden, nachdem die Nachrichten in der Warteschlange angekommen sind und diese Nachrichten dennoch verarbeiten. Andere im nächsten Abschnitt behandelte Listener müssen aktiv lauschen, oder sie verpassen die Gelegenheit, die Nachricht zu lesen. Diese Meldungen können von Common Data Service oder einer anderen Quelle stammen. 
  
> [!IMPORTANT]
>  Wenn Sie einen Warteschlangenlistener schreiben, überprüfen Sie jede einzelne Nachrichtenkopfaktion, um zu bestimmen, ob die Meldung von Common Data Service stammt. Informationen dazu finden Sie unter [Filtermeldungen](write-listener-application-azure-solution.md#filter).  
  
Mit [Empfangen](/dotnet/api/microsoft.servicebus.messaging.queueclient.receive) im Modus [ReceiveMode.ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) können Sie eine Nachricht destruktiv lesen. Dabei wird die Nachricht gelesen und aus der Warteschlange entfernt. Im Modus [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) wird eine Nachricht nicht destruktiv gelesen. In diesem Fall wird die Nachricht zwar gelesen, bleibt jedoch in der Warteschlange verfügbar. Der in diesem SDK bereitgestellte Beispielcode des persistenten Warteschlangenlisteners führt einen destruktiven Lesevorgang durch. Weitere Informationen zum Lesen von Nachrichten in einer Warteschlange finden Sie unter [How to Receive Messages from a Queue (in englischer Sprache)](/azure/service-bus-messaging/service-bus-dotnet-get-started-with-queues#receive-messages-from-the-queue).  
  
Ein *Thema* ähnelt einer Warteschlange, aber implementiert eine Veröffentlichungs-/Abonnementmodell. Mindestens ein Listener kann ein Thema abonnieren und Nachrichten aus seiner Warteschlange empfangen. Weitere Informationen: [Warteschlangen, Themen und Abonnements](/azure/service-bus-messaging/service-bus-queues-topics-subscriptions)  
  
> [!IMPORTANT]
>  Um diese Warteschlangen oder Themen nutzen zu können, müssen Sie Ihre Listener-Anwendungen mit dem [Azure SDK](https://azure.microsoft.com/downloads/archive-net-downloads/) schreiben.
  
Die Verwendung von Warteschlangen und Themen in Ihrem Multisystem-Software-Entwurf kann zu einem Entkoppeln von Systemen führen. Wenn die Listener-Anwendung ggf. überhaupt nicht verfügbar ist, findet die Nachrichtenzustellung aus Common Data Service dennoch statt. Die Listener-Anwendung kann mit der Verarbeitung der Warteschlangennachricht fortfahren, wenn sie wieder online ist. Weitere Informationen: [Warteschlangen, Themen und Abonnements](/azure/service-bus-messaging/service-bus-queues-topics-subscriptions)  
  
<a name="bkmk_writeoneway"></a>

## <a name="write-a-one-way-two-way-or-rest-listener"></a>Unidirektionalen, bidirektionalen oder REST-Listener schreiben

Neben dem zuvor beschriebenen Warteschlangen-Listener können Sie einen Listener für drei weitere Servicebusverträge schreiben, die wie folgt untersützt werden von Common Data Service: unidirektional, bidirektional und REST. Ein unidirektionaler Listener kann eine vom Servicebus veröffentlichte Meldung lesen und verarbeiten. Ein bidirektionaler Listener kann das ebenso, kann aber auch eine Zeichenfolge mit einigen Informationen an Common Data Service zurückgeben. Ein REST-Listener ist dasselbe wie der bidirektionale Listener, außer dass er mit einem REST-Endpunkt arbeitet. Beachten Sie, dass diese Listener an einem Dienstendpunkt aktiv lauschen müssen, um eine Meldung zu lesen, die über den Servicebus gesendet wurde. Wenn der Listener nicht lauscht, wenn Common Data Service versucht, eine Meldung auf dem Servicebus bereitzustellen, wird die Nachricht nicht gesendet.
  
Das Schreiben eines Listeners strukturiert sich in Aktionen, die unter dem Begriff "ABC" zusammengefasst werden: Adresse, Bindung, Vertrag (engl. Contract). 

### <a name="one-way-listener"></a>Eindirektionaler Listener
  
- Adresse: Service-URI  
  
- Bindung: [WS2007HttpRelayBinding](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding)  
  
- Vertrag: <xref:Microsoft.Xrm.Sdk.IServiceEndpointPlugin>  
  
Nachdem der Listener bei einem Endpunkt registriert ist, wird die <xref:Microsoft.Xrm.Sdk.IServiceEndpointPlugin.Execute*>-Methode des Listeners aufgerufen, wenn von Common Data Service eine Meldung auf dem Servicebus bereitgestellt wird. Die `Execute`-Methode gibt keine Daten vom Methodenaufruf zurück. Weitere Informationen finden Sie unter dem Beispiel für unidirektionalen Listener [Beispiel: Unidirektionaler Listener](org-service/samples/one-way-listener.md)  
  
### <a name="two-way-listener"></a>Zweidirektionaler Listener
  
- Adresse: Service-URI  
  
- Bindung: [WS2007HttpRelayBinding](/dotnet/api/microsoft.servicebus.ws2007httprelaybinding)  
  
- Vertrag: <xref:Microsoft.Xrm.Sdk.ITwoWayServiceEndpointPlugin>  
  
Für diesen bidirektionalen Vertrag gibt die <xref:Microsoft.Xrm.Sdk.ITwoWayServiceEndpointPlugin.Execute*>-Methode eine Zeichenfolge aus dem Methodenaufruf zurück. Weitere Informationen finden Sie unter dem Beispiel für bidirektionalen Listener [Beispiel: Bidirektionaler Listener](org-service/samples/two-way-listener.md)  
  
### <a name="rest-listener"></a>REST-Listener
  
- Adresse: Service-URI  
  
- Bindung: [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.wshttprelaybinding)
  
- Vertrag: <xref:Microsoft.Xrm.Sdk.IWebHttpServiceEndpointPlugin>  
  
Für den REST-Vertrag gibt die <xref:Microsoft.Xrm.Sdk.IWebHttpServiceEndpointPlugin.Execute*>-Methode eine Zeichenfolge aus dem Methodenaufruf zurück. Weitere Informationen bietet das Beispiel für REST-Listener unter [Beispiel: REST-Listener](org-service/samples/rest-listener.md). Beachten Sie, dass im Beispiel für REST-Listener ein <xref:System.ServiceModel.Web.WebServiceHost> instanziiert wird und kein <xref:System.ServiceModel.ServiceHost>, wie im bidirektionalen Beispiel.
  
> [!NOTE]
>  Falls das vordefinierte (ServiceBusPlugin) Plug-In mit einem bidirektionalen Listener oder REST-Listener verwendet wird, verwendet das Plug-In keine vom Listener zurückgegebene Zeichenfolgendaten. Ein benutzerdefiniertes Azure-kompatibles Plug-In kann jedoch diese Informationen nutzen.  
> 
>  Wenn Sie die Listenerbeispiele ausführen, werden Sie aufgefordert, als Ausstellergeheimnis den Azure Service Bus-Verwaltungsschlüssel anzugeben. Die WS2007 Federation HTTP-Bindung verwendet den `token`-Modus und das WS-Trust 1.3-Protokoll.  
  
<a name="filter"></a>

## <a name="filter-messages"></a>Nachrichten filtern

Es gibt einen Eigenschaftenbehälter mit zusätzlichen Informationen, der zu jeder Brokernachricht-[Eigenschaften](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#properties)-Eigenschaft, die von Common Data Service gesendet wird, hinzugefügt wird. Der Eigenschaftenbehälter, der mit den Endpunkten von Warteschlangen, Weiterleitungen und Themenverträgen verfügbar ist, enthält die folgenden Informationen:  
  
- Organisation-URI:
- ID des aufrufenden Benutzers
- ID des initialisierenden Benutzers
- Logischer Entitätsname
- Anforderungsname  
  
Diese Informationen identifizieren die Organisation, den Benutzer, die Entität und die von Common Data Service verarbeitete Nachrichtenanforderung für die Bereitstellung der Servicebusnachricht. Die Verfügbarkeit dieser Eigenschaften zeigt an, dass die Mitteilung von Common Data Service gesendet wurde. Ihr Listener kann entscheiden, wie Mitteilung basierend auf dieser Werte verarbeitet werden.  
  
<a name="bkmk_multiple-formats"></a>
 
## <a name="read-the-data-context-in-multiple-data-formats"></a>Lesen Sie den Datenkontext in mehreren Formaten

Der Datenkontext der aktuellen Common Data Service-Operation wird an Ihre Azure-Lösungslisteneranwendung im Textkörper einer Service-Busmitteilung weitergeleitet. In den vorhergehenden Versionen wurde nur ein binäres .NET-Format unterstützt.  Für plattformübergreifende (nicht .NET) Interoperabilität können Sie jetzt eins von drei Datenformaten für den Nachrichtentextkörper angeben: binär .NET, JSON oder XML.  Dieses Format wird im [MessageFormat](reference/entities/serviceendpoint.md#BKMK_MessageFormat)-Attribut der [ServiceEndpoint Entität](reference/entities/serviceendpoint.md)-Entität angegeben.
  
Wenn sie Mitteilungen empfängt, kann Ihre Listeneranwendung den Datenkontext im Nachrichtentextkörper basierend auf dem contentType der Mitteilung lesen. Beispielcode dafür wird unten angezeigt.  
  
```csharp
var receivedMessage = inboundQueueClient.Receive(TimeSpan.MaxValue);  
  
if (receivedMessage.ContentType = "application/msbin1")  
{  
    RemoteExecutionContext context = receivedMessage.GetBody<RemoteExecutionContext>();  
}  
else if (receivedMessage.ContentType = "application/json")  
{  
    //string jsonBody = new StreamReader(receivedMessage.GetBody<Stream>(), Encoding.UTF8).ReadToEnd();  
    RemoteExecutionContext contextFromJSON = receivedMessage.GetBody<RemoteExecutionContext>(  
        new DataContractJsonSerializer(typeof(RemoteExecutionContext)));  
}  
else if (receivedMessage.ContentType = "application/xml")  
{  
    //string xmlBody = new StreamReader(receivedMessage.GetBody<Stream>(), Encoding.UTF8).ReadToEnd();  
    RemoteExecutionContext contextFromXML = receivedMessage.GetBody<RemoteExecutionContext>(  
        new DataContractSerializer(typeof(RemoteExecutionContext)));  
}  
```  
  
### <a name="see-also"></a>Siehe auch

[Azure-Erweiterungen](azure-integration.md)<br />
[Schreiben eines benutzerdefinierten Azure-Plug-Ins](write-custom-azure-aware-plugin.md)<br />
[Beispiel: Persistenter Warteschlangenlistener](org-service/samples/persistent-queue-listener.md)<br />
[Beispiel: Eindirektionaler Listener](org-service/samples/one-way-listener.md)<br />
[Beispiel: Bidirektionaler Listener](org-service/samples/two-way-listener.md)<br />
[Beispiel: REST-Listener](org-service/samples/rest-listener.md)<br />
[Arbeiten mit Common Data Service-Daten in Ihrer Azure-Lösung](work-data-azure-solution.md)<br />
[Arbeiten mit Common Data Service-Ereignisdaten in Ihrer Azure-Ereignishub-Lösung](work-event-data-azure-event-hub-solution.md)
