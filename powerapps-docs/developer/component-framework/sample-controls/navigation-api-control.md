---
title: " Navigations-API-Komponente | Microsoft Docs"
description: Implementieren der Navigations-API-Komponente
ms.custom: ''
manager: kvivek
ms.date: 10/01/2019
ms.service: powerapps
ms.topic: article
ms.author: nabuthuk
author: Nkrb
ms.openlocfilehash: 85dd665f7a3dc92b5198cfd8429b59af0896d5cc
ms.sourcegitcommit: 8185f87dddf05ee256491feab9873e9143535e02
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2019
ms.locfileid: "2748311"
---
# <a name="implementing-navigation-api-component"></a>Implementieren der Navigations-API-Komponente

Diese Beispielkomponente untersucht die verschiedenen Methoden, die als Teil der Formatierungs-API des PowerApps component framework zur Verfügung stehen. Im vorliegenden Beispiel, erstellen Sie eine Reihe von Eingabeelementen des Typs Schaltfläche , die in die jeweiligen Methoden der Navigations-API anrufen, die dem angezeigten Wert entsprechen.  

> [!div class="mx-imgBorder"]
> ![Navigations-API-Komponente](../media/navigation-api-control.png "Navigations-API-Komponente")

## <a name="available-for"></a>Verfügbar für 

Modellgestützte Apps

## <a name="manifest"></a>Manifest

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest>
    <control namespace="SampleNamespace" constructor="TSNavigationAPI" version="1.0.0" display-name-key="TS_NavigationAPI_Display_Key" description-key="TS_NavigationAPI_Desc_Key" control-type="standard">
        <type-group name="numbers">
            <type>Whole.None</type>
            <type>Currency</type>
            <type>FP</type>
            <type>Decimal</type>
        </type-group>
        <property name="controlValue" display-name-key="controlValue_Display_Key" description-key="controlValue_Desc_Key" of-type-group="numbers" usage="bound" required="true" />
        <resources>
            <code path="index.ts" order="1" />
            <css path="css/TS_NavigationAPI.css" order="1" />
        </resources>
    </control>
</manifest>
```

## <a name="code"></a>Code

```TypeScript
import {IInputs, IOutputs} from "./generated/ManifestTypes";
export class TSNavigationAPI implements ComponentFramework.StandardControl<IInputs, IOutputs> {
// PowerApps component framework framework delegate which will be assigned to this object which would be called whenever an update happens. 
private _notifyOutputChanged: () => void;
// Reference to the div element that hold together all the HTML elements that we are creating as part of this control
private divElement: HTMLDivElement;
// Reference to the button that invokes the openAlertDialog command
private openAlertDialogButton: HTMLButtonElement;
// Reference to the button that invokes the openConfirmDialog command
private openConfirmDialogButton: HTMLButtonElement;
// Reference to the button that invokes the openFile command
private openFileButton: HTMLButtonElement;
// Reference to the button that invokes the openUrl command
private openUrlButton: HTMLButtonElement;
// Reference to the control container HTMLDivElement
// This element contains all elements of our custom control example
private _container: HTMLDivElement;
// Reference to ComponentFramework Context object
private _context : ComponentFramework.Context<IInputs>;
/**
* Empty constructor.
*/
constructor()
{
}
/**
* Used to initialize the control instance. Controls can kick off remote server calls and other initialization actions here.
* Data-set values are not initialized here, use updateView.
* @param context The entire property bag available to control via Context Object; It contains values as set up by the customizer mapped to property names defined in the manifest, as well as utility functions.
* @param notifyOutputChanged A callback method to alert the framework that the control has new outputs ready to be retrieved asynchronously.
* @param state A piece of data that persists in one session for a single user. Can be set at any point in a controls life cycle by calling 'setControlState' in the Mode interface.
* @param container If control is marked control-type='standard', it receives an empty div element within which it can render its content.
*/
public init(context: ComponentFramework.Context<IInputs>, notifyOutputChanged: () => void, state: ComponentFramework.Dictionary, container:HTMLDivElement)
{
this._notifyOutputChanged = notifyOutputChanged;
this._context = context;
this._container = container;
this.divElement = document.createElement("div");
this.divElement.setAttribute("class","TSNavigationAPI");
// Create the HTML button elements for openAlertDialog button
this.openAlertDialogButton = document.createElement("button");
this.openAlertDialogButton.setAttribute("id","openAlertDialogButton");
this.openAlertDialogButton.innerHTML = "openAlertDialogButton";
// Create the HTML button elements for openConfirmDialog button
this.openConfirmDialogButton = document.createElement("button");
this.openConfirmDialogButton.setAttribute("id","openConfirmDialogButton");
this.openConfirmDialogButton.innerHTML = "openConfirmDialogButton";
// Create the HTML button elements for openFile button
this.openFileButton = document.createElement("button");
this.openFileButton.setAttribute("id","openFileButton");
this.openFileButton.innerHTML = "openFileButton";
// Create the HTML button elements for openUrl button
this.openUrlButton = document.createElement("button");
this.openUrlButton.setAttribute("id","openUrlButton");
this.openUrlButton.innerHTML = "openUrlButton";
// bind the function which invokes the respective API's to each of the buttons
this.openAlertDialogButton.addEventListener("click",this.raiseEvent.bind(this));
this.openConfirmDialogButton.addEventListener("click",this.raiseEvent.bind(this));
this.openFileButton.addEventListener("click",this.raiseEvent.bind(this));
this.openUrlButton.addEventListener("click",this.raiseEvent.bind(this));
// append all the button elements to the parent div element for control.
this.divElement.appendChild(this.openAlertDialogButton);
this.divElement.appendChild(this.openConfirmDialogButton);
this.divElement.appendChild(this.openFileButton);
this.divElement.appendChild(this.openUrlButton);
// append the parent div element in the control to the control's container
this._container.appendChild(this.divElement);
}
/**
* Handles the events raised by each of the buttons that are binded according to their id
* @param event : event object that contains all the properties regarding the raised event
*/
public raiseEvent(event: Event,)
{
var inputSource = (event.srcElement! as Element)!.id;
switch(inputSource)
{
    case "openAlertDialogButton": this._context.navigation.openAlertDialog({text:"This is an alert.", confirmButtonLabel : "Yes",}).then(
        function success()
        {
            document.getElementById("openAlertDialogButton")!.innerHTML = "Alert dialog closed";
        },
        function()
        {
            document.getElementById("openAlertDialogButton")!.innerHTML = "Error in Alert Dialog";
        }
    );
    break;
    case "openConfirmDialogButton": this._context.navigation.openConfirmDialog({title:"Confirmation Dialog", text:"This is a confirmation.",},{height:200, width:450}).then(
        function(success)
        {
            if(success.confirmed)
            {
                document.getElementById("openConfirmDialogButton")!.innerHTML = "Ok button clicked.";
            }
            else
            {
                document.getElementById("openConfirmDialogButton")!.innerHTML = "Cancel or X button clicked.";
            }
        }
    );
    break;
    case "openFileButton": 
        var file = {
                    fileContent: "U2FtcGxlIGNvbnRlbnQgZm9yIERlbW8=", //Contents of the file in base64 encoded format. 
                    fileName: "Sample.txt", //Name of the file.
                    fileSize: 29, //Size of the file in KB.
                    mimeType: "text/plain" //MIME type of the file.
                    };
        this._context.navigation.openFile(file,{openMode:2});
    break;
    case "openUrlButton": this._context.navigation.openUrl("https://www.microsoft.com");
    break;
};
//this._notifyOutputChanged();
}
/**
* Called when any value in the property bag has changed. This includes field values, data-sets, global values such as container height and width, offline status, control metadata values such as label, visible, etc.
* @param context The entire property bag available to control via Context Object; It contains values as set up by the customizer mapped to names defined in the manifest, as well as utility functions
*/
public updateView(context: ComponentFramework.Context<IInputs>,): void
{
this._context = context;
}
/** 
* It is called by the framework prior to a control receiving new data. 
* @returns an object based on nomenclature defined in manifest, expecting object[s] for property marked as “bound” or “output”
*/
public getOutputs(): IOutputs
{
// no-op: method not leveraged by this example custom control
return { };
}
/** 
* Called when the control is to be removed from the DOM tree. Controls should use this call for cleanup.
* i.e. canceling any pending remote calls, removing listeners, etc.
*/
public destroy()
{
}
}
```

## <a name="resources"></a>Ressourcen

```css
.SampleNamespace\.TSNavigationAPI button {
  background-color: rgb(59, 121, 183);
  border: 1px solid black;
  color: white;
  padding: 10px 24px;
  cursor: pointer;
  width: 100%;
  display: block;
}
.SampleNamespace\.TSNavigationAPI button:not(:last-child) {
  border-bottom: none;
}
.SampleNamespace\.TSNavigationAPI button:hover {
  background-color: #c2c2c2;
}
```

Die `openAlertDialog`-Methode bietet die Möglichkeit einen Warnungsdialog anzuzeigen, der eine Nachricht und eine Schaltfläche enthält. Sie können auch Rückrufmethoden implementieren, wenn der Warndialog geschlossen wird, oder wenn beim Laden des Dialogs ein Fehler auftritt.
  
Wenn Sie in diesem Beispiel auf `openAlertDialogButton` klicken, wird ein Warndialog geöffnet und der Wert davon wird auf `Alert dialog closed` festgelegt, wenn der Dialog entweder mit der Schaltfläche `OK` oder der Schaltfläche `X` geschlossen wird.

> [!NOTE]
> Dies gleicht dem Aufruf der [Xrm.Navigation.openAlertDialog](https://docs.microsoft.com/dynamics365/customer-engagement/developer/clientapi/reference/xrm-navigation/openalertdialog)-Methode in ClientAPI.  

Die `openConfirmDialog`-Methode bietet die Möglichkeit einen Warnungsdialog anzuzeigen, der eine Nachricht und zwei Schaltflächen enthält. Sie können diese Methode verwenden, um unterschiedliche Logik anhand der geklickten Schaltfläche zu implementieren. Sie können den Erfolgsrückruf implementieren, der aufgerufen wird, wenn der Dialog geschlossen wird, indem auf eine der Schaltflächen geklickt wird.
  
In diesem Beispiel wird der Bestätigungsdialog gezeigt, wenn Sie auf `openConfirmDialogButton` klicken und der Wert davon wird auf `Ok` oder `Cancel` oder `X` festgelegt, je nach der Schaltfläche, auf die geklickt wurde.

> [!NOTE]
> Dies gleicht dem Aufruf der [Xrm.Navigation.openConfirmDialog](https://docs.microsoft.com/dynamics365/customer-engagement/developer/clientapi/reference/xrm-navigation/openconfirmdialog)-Methode in ClientAPI.
  
Die `openFile`-Methode bietet die Möglichkeit, eine Datei zu öffnen. Sie müssen das Dateiobjekt übergeben, das den Dateinamen, den Inhalt den mimetype und die Dateigröße enthält. Sie können auch den optionalen Parameter des Modus übergeben, für den die Datei als 1 oder 2 geöffnet werden soll. Dabei ist 1 der Standard, der die Datei im Lese- oder Öffnen-Modus öffnet.
  
In diesem Beispiel wird eine Datei namens `SampleDemo.txt` im sicheren Modus beim Klicken auf `openFileButton` geöffnet.

> [!NOTE]
> Dies gleicht dem Aufruf der [Xrm.Navigation.openFile](https://docs.microsoft.com/dynamics365/customer-engagement/developer/clientapi/reference/xrm-navigation/openfile)-Methode in ClientAPI.

Die `openUrl`-Methode bietet die Möglichkeit, eine URL zu öffnen. Sie müssen die URL als eine Zeichenfolge an die Methode übergeben und auch die optionalen Parameter für Höhe, Breite und openInNewWindow als wahr übergeben, wenn die URL in einem neuen Fenster geöffnet werden soll.
  
In diesem Beispiel wird ein neues Fenster geöffnet und die microsoft.com home page wird beim Klicken auf `openUrlButton` geladen.

> [!NOTE]
> Dies gleicht dem Aufruf der [Xrm.Navigation.openUrl](https://docs.microsoft.com/dynamics365/customer-engagement/developer/clientapi/reference/xrm-navigation/openurl)-Methode in ClientAPI.

### <a name="related-topics"></a>Verwandte Themen

[Beispielkomponenten herunterladen](https://go.microsoft.com/fwlink/?linkid=2088525)<br/>
[PowerApps component framework-API-Referenz](../reference/index.md)<br/>
[Manifestschemareferenz des PowerApps component framework](../manifest-schema-reference/index.md)

