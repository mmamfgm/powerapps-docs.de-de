---
title: " Web-API-Komponente | Microsoft Docs"
description: Implementieren einer Web-API-Komponente
ms.custom: ''
manager: kvivek
ms.date: 10/01/2019
ms.service: powerapps
ms.topic: article
ms.author: nabuthuk
author: nkrb
ms.openlocfilehash: 4e893466a5a7404926942b4e297cdc4ecb1affef
ms.sourcegitcommit: 8185f87dddf05ee256491feab9873e9143535e02
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/01/2019
ms.locfileid: "2748309"
---
# <a name="implementing-web-api-component"></a>Implementieren einer Web-API-Komponente

Die Web-API-Komponente wurde entworfen, um Aktionen auszuführen, zu erstellen, abzurufen, zu aktualisieren und zu löschen. Die Komponente rendert vier Schalflächen, die angeklickt werden können, um verschiedene Web-API-Aktionen aufzurufen. Das Ergebnis des Web-API-Aufrufs wird in ein HTML-Div-Element am unteren Rand der Codekomponente injiziert.  

> [!div class="mx-imgBorder"]
> ![Web-API-Komponente](../media/web-api-control.png "Web-API-Komponente")

## <a name="available-for"></a>Verfügbar für 

Modellgestützte Apps

## <a name="manifest"></a>Manifest

 ```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest>
    <control namespace="SampleNamespace" constructor="TSWebAPI" version="1.0.0" display-name-key="TS_WebAPI_Display_Key" description-key="TS_WebAPI_Desc_Display_Key" control-type="standard">
        <property name="stringProperty" display-name-key="stringProperty_Display_Key" description-key="stringProperty_Desc_Key" of-type="SingleLine.Text" usage="bound" required="true" />
        <resources>
            <code path="index.ts" order="1" />
            <css path="css/TS_WebAPI.css" order="2" />
        </resources>
        <feature-usage>
            <uses-feature name="WebAPI" required="true" />
        </feature-usage>
    </control>
</manifest>
```

## <a name="code"></a>Code

```TypeScript
import { IInputs, IOutputs } from "./generated/ManifestTypes";
export class TSWebAPI
  implements ComponentFramework.StandardControl<IInputs, IOutputs> {
  // reference to the control container HTMLDivElement
  // This element contains all elements of our custom control example
  private _container: HTMLDivElement;
  // reference to ComponentFramework Context object
  private _context: ComponentFramework.Context<IInputs>;
  // Name of entity to use for example Web API calls performed by this control
  private static _entityName: string = "account";
  // Required field on _entityName of type 'single line of text'
  // Example Web API calls performed by example custom control will set this field for new record creation examples
  private static _requiredAttributeName: string = "name";
  // Value the _requiredAttributeName field will be set to for new created records
  private static _requiredAttributeValue: string =
    "Web API Custom Control (Sample)";
  // Name of currency field on _entityName to populate during record create
  // Example Web API calls performed by example custom control will set and read this field
  private static _currencyAttributeName: string = "revenue";
  // Friendly name of currency field (only used for control UI - no functional impact)
  private static _currencyAttributeNameFriendlyName: string = "annual revenue";
  // Flag if control view has been rendered
  private _controlViewRendered: Boolean;
  // references to button elements rendered by example custom control
  private _createEntity1Button: HTMLButtonElement;
  private _createEntity2Button: HTMLButtonElement;
  private _createEntity3Button: HTMLButtonElement;
  private _deleteRecordButton: HTMLButtonElement;
  private _fetchXmlRefreshButton: HTMLButtonElement;
  private _oDataRefreshButton: HTMLButtonElement;
  // references to div elements rendered by the example custom control
  private _odataStatusContainerDiv: HTMLDivElement;
  private _resultContainerDiv: HTMLDivElement;
  /**
   * Used to initialize the control instance. Controls can kick off remote server calls and other initialization actions here.
   * Data-set values are not initialized here, use updateView.
   * @param context The entire property bag available to control via Context Object; It contains values as set up by the customizer mapped to property names defined in the manifest, as well as utility functions.
   * @param notifyOutputChanged A callback method to alert the framework that the control has new outputs ready to be retrieved asynchronously.
   * @param state A piece of data that persists in one session for a single user. Can be set at any point in a controls life cycle by calling 'setControlState' in the Mode interface.
   * @param container If control is marked control-type='standard', it receives an empty div element within which it can render its content.
   */
  public init(
    context: ComponentFramework.Context<IInputs>,
    notifyOutputChanged: () => void,
    state: ComponentFramework.Dictionary,
    container: HTMLDivElement
  ) {
    this._context = context;
    this._controlViewRendered = false;
    this._container = document.createElement("div");
    this._container.classList.add("TSWebAPI_Container");
    container.appendChild(this._container);
  }
  /**
   * Called when any value in the property bag has changed. This includes field values, data-sets, global values such as container height and width, offline status, control metadata values such as label, visible, etc.
   * @param context The entire property bag available to control via Context Object; It contains values as set up by the customizer mapped to names defined in the manifest, as well as utility functions
   */
  public updateView(context: ComponentFramework.Context<IInputs>): void {
    if (!this._controlViewRendered) {
      this._controlViewRendered = true;
      // Render Web API Examples
      this.renderCreateExample();
      this.renderDeleteExample();
      this.renderFetchXmlRetrieveMultipleExample();
      this.renderODataRetrieveMultipleExample();
      // Render result div to display output of Web API calls
      this.renderResultsDiv();
    }
  }
  /**
   * It is called by the framework prior to a control receiving new data.
   * @returns an object based on nomenclature defined in manifest, expecting object[s] for property marked as “bound” or “output”
   */
  public getOutputs(): IOutputs {
    // no-op: method not leveraged by this example custom control
    return {};
  }
  /**
   * Called when the control is to be removed from the DOM tree. Controls should use this call for cleanup.
   * i.e. canceling any pending remote calls, removing listeners, etc.
   */
  public destroy() {}
  /**
   * Renders example use of CreateRecord Web API
   */
  private renderCreateExample() {
    // Create header label for Web API sample
    let headerDiv: HTMLDivElement = this.createHTMLDivElement(
      "create_container",
      true,
      "Click to create " + TSWebAPI._entityName + " record"
    );
    this._container.appendChild(headerDiv);
    // Create button 1 to create record with revenue field set to 100
    let value1: string = "100";
    this._createEntity1Button = this.createHTMLButtonElement(
      this.getCreateRecordButtonLabel(value1),
      this.getCreateButtonId(value1),
      value1,
      this.createButtonOnClickHandler.bind(this)
    );
    // Create button 2 to create record with revenue field set to 200
    let value2: string = "200";
    this._createEntity2Button = this.createHTMLButtonElement(
      this.getCreateRecordButtonLabel(value2),
      this.getCreateButtonId(value2),
      value2,
      this.createButtonOnClickHandler.bind(this)
    );
    // Create button 3 to create record with revenue field set to 300
    let value3: string = "300";
    this._createEntity3Button = this.createHTMLButtonElement(
      this.getCreateRecordButtonLabel(value3),
      this.getCreateButtonId(value3),
      value3,
      this.createButtonOnClickHandler.bind(this)
    );
    // Append all button HTML elements to custom control container div
    this._container.appendChild(this._createEntity1Button);
    this._container.appendChild(this._createEntity2Button);
    this._container.appendChild(this._createEntity3Button);
  }
  /**
   * Renders example use of DeleteRecord Web API
   */
  private renderDeleteExample(): void {
    // Create header label for Web API sample
    let headerDiv: HTMLDivElement = this.createHTMLDivElement(
      "delete_container",
      true,
      "Click to delete " + TSWebAPI._entityName + " record"
    );
    // Render button to invoke DeleteRecord Web API call
    this._deleteRecordButton = this.createHTMLButtonElement(
      "Select record to delete",
      "delete_button",
      null,
      this.deleteButtonOnClickHandler.bind(this)
    );
    // Append elements to custom control container div
    this._container.appendChild(headerDiv);
    this._container.appendChild(this._deleteRecordButton);
  }
  /**
   * Renders example use of RetrieveMultiple Web API with OData
   */
  private renderODataRetrieveMultipleExample(): void {
    let containerClassName: string = "odata_status_container";
    // Create header label for Web API sample
    let statusDivHeader: HTMLDivElement = this.createHTMLDivElement(
      containerClassName,
      true,
      "Click to refresh record count"
    );
    this._odataStatusContainerDiv = this.createHTMLDivElement(
      containerClassName,
      false,
      undefined
    );
    // Create button to invoke OData RetrieveMultiple Example
    this._fetchXmlRefreshButton = this.createHTMLButtonElement(
      "Refresh record count",
      "odata_refresh",
      null,
      this.refreshRecordCountButtonOnClickHandler.bind(this)
    );
    // Append HTML elements to custom control container div
    this._container.appendChild(statusDivHeader);
    this._container.appendChild(this._odataStatusContainerDiv);
    this._container.appendChild(this._fetchXmlRefreshButton);
  }
  /**
   * Renders example use of RetrieveMultiple Web API with Fetch XML
   */
  private renderFetchXmlRetrieveMultipleExample(): void {
    let containerName: string = "fetchxml_status_container";
    // Create header label for Web API sample
    let statusDivHeader: HTMLDivElement = this.createHTMLDivElement(
      containerName,
      true,
      "Click to calculate average value of " +
        TSWebAPI._currencyAttributeNameFriendlyName
    );
    let statusDiv: HTMLDivElement = this.createHTMLDivElement(
      containerName,
      false,
      undefined
    );
    // Create button to invoke Fetch XML RetrieveMultiple Web API example
    this._oDataRefreshButton = this.createHTMLButtonElement(
      "Calculate average value of " +
        TSWebAPI._currencyAttributeNameFriendlyName,
      "odata_refresh",
      null,
      this.calculateAverageButtonOnClickHandler.bind(this)
    );
    // Append HTML Elements to custom control container div
    this._container.appendChild(statusDivHeader);
    this._container.appendChild(statusDiv);
    this._container.appendChild(this._oDataRefreshButton);
  }
  /**
   * Renders a 'result container' div element to inject the status of the example Web API calls
   */
  private renderResultsDiv() {
    // Render header label for result container
    let resultDivHeader: HTMLDivElement = this.createHTMLDivElement(
      "result_container",
      true,
      "Result of last action"
    );
    this._container.appendChild(resultDivHeader);
    // Div elements to populate with the result text
    this._resultContainerDiv = this.createHTMLDivElement(
      "result_container",
      false,
      undefined
    );
    this._container.appendChild(this._resultContainerDiv);
    // Init the result container with a notification the control was loaded
    this.updateResultContainerText("Web API sample custom control loaded");
  }
  /**
   * Event Handler for onClick of create record button
   * @param event : click event
   */
  private createButtonOnClickHandler(event: Event): void {
    // Retrieve the value to set the currency field to from the button's attribute
    let currencyAttributeValue: Number = parseInt(
      event.srcElement!.attributes.getNamedItem("buttonvalue")!.value
    );
    // Generate unique record name by appending timestamp to _requiredAttributeValue
    let recordName: string =
      TSWebAPI._requiredAttributeValue + "_" + Date.now();
    // Set the values for the attributes we want to set on the new record
    // If you want to set additional attributes on the new record, add to data dictionary as key/value pair
    var data: any = {};
    data[TSWebAPI._requiredAttributeName] = recordName;
    data[TSWebAPI._currencyAttributeName] = currencyAttributeValue;
    // store reference to 'this' so it can be used in the callback method
    var thisRef = this;
    // Invoke the Web API to creat the new record
    this._context.webAPI.createRecord(TSWebAPI._entityName, data).then(
      function(response: ComponentFramework.Entityreference) {
        // Callback method for successful creation of new record
        // Get the ID of the new record created
        let id: string = response.id;
        // Generate HTML to inject into the result div to showcase the fields and values of the new record created
        let resultHtml: string =
          "Created new " + TSWebAPI._entityName + " record with below values:";
        resultHtml += "<br />";
        resultHtml += "<br />";
        resultHtml += "id: " + id;
        resultHtml += "<br />";
        resultHtml += "<br />";
        resultHtml += TSWebAPI._requiredAttributeName + ": " + recordName;
        resultHtml += "<br />";
        resultHtml += "<br />";
        resultHtml +=
          TSWebAPI._currencyAttributeName + ": " + currencyAttributeValue;
        thisRef.updateResultContainerText(resultHtml);
      },
      function(errorResponse: any) {
        // Error handling code here - record failed to be created
        thisRef.updateResultContainerTextWithErrorResponse(errorResponse);
      }
    );
  }
  /**
   * Event Handler for onClick of delete record button
   * @param event : click event
   */
  private deleteButtonOnClickHandler(): void {
    // Invoke a lookup dialog to allow the user to select an existing record of type _entityName to delete
    var lookUpOptions: any = {
      entityTypes: [TSWebAPI._entityName]
    };
    // store reference to 'this' so it can be used in the callback method
    var thisRef = this;
    var lookUpPromise: any = this._context.utils.lookupObjects(lookUpOptions);
    lookUpPromise.then(
      // Callback method - invoked after user has selected an item from the lookup dialog
      // Data parameter is the item selected in the lookup dialog
      (data: ComponentFramework.Entityreference[]) => {
        if (data && data[0]) {
          // Get the ID and entityType of the record selected by the lookup
          let id: string = data[0].id;
          let entityType: string = data[0].entityType!;
          // Invoke the deleteRecord method of the WebAPI to delete the selected record
          this._context.webAPI.deleteRecord(entityType, id).then(
            function(response: ComponentFramework.Entityreference) {
              // Record was deleted successfully
              let responseId: string = response.id;
              let responseEntityType: string = response.entityType!;
              // Generate HTML to inject into the result div to showcase the deleted record
              thisRef.updateResultContainerText(
                "Deleted " +
                  responseEntityType +
                  " record with ID: " +
                  responseId
              );
            },
            function(errorResponse: any) {
              // Error handling code here
              thisRef.updateResultContainerTextWithErrorResponse(errorResponse);
            }
          );
        }
      },
      (error: any) => {
        // Error handling code here
        thisRef.updateResultContainerTextWithErrorResponse(error);
      }
    );
  }
  /**
   * Event Handler for onClick of calculate average value button
   * @param event : click event
   */
  private calculateAverageButtonOnClickHandler(): void {
    // Build FetchXML to retrieve the average value of _currencyAttributeName field for all _entityName records
    // Add a filter to only aggregate on records that have _currencyAttributeName not set to null
    let fetchXML: string =
      "<fetch distinct='false' mapping='logical' aggregate='true'>";
    fetchXML += "<entity name='" + TSWebAPI._entityName + "'>";
    fetchXML +=
      "<attribute name='" +
      TSWebAPI._currencyAttributeName +
      "' aggregate='avg' alias='average_val' />";
    fetchXML += "<filter>";
    fetchXML +=
      "<condition attribute='" +
      TSWebAPI._currencyAttributeName +
      "' operator='not-null' />";
    fetchXML += "</filter>";
    fetchXML += "</entity>";
    fetchXML += "</fetch>";
    // store reference to 'this' so it can be used in the callback method
    var thisRef = this;
    // Invoke the Web API RetrieveMultipleRecords method to calculate the aggregate value
    this._context.webAPI
      .retrieveMultipleRecords(TSWebAPI._entityName, "?fetchXml=" + fetchXML)
      .then(
        function(response: ComponentFramework.WebApi.RetrieveMultipleResponse) {
          // Retrieve multiple completed successfully -- retrieve the averageValue
          let averageVal: Number = response.entities[0].average_val;
          // Generate HTML to inject into the result div to showcase the result of the RetrieveMultiple Web API call
          let resultHTML: string =
            "Average value of " +
            TSWebAPI._currencyAttributeNameFriendlyName +
            " attribute for all " +
            TSWebAPI._entityName +
            " records: " +
            averageVal;
          thisRef.updateResultContainerText(resultHTML);
        },
        function(errorResponse: any) {
          // Error handling code here
          thisRef.updateResultContainerTextWithErrorResponse(errorResponse);
        }
      );
  }
  /**
   * Event Handler for onClick of calculate record count button
   * @param event : click event
   */
  private refreshRecordCountButtonOnClickHandler(): void {
    // Generate OData query string to retrieve the _currencyAttributeName field for all _entityName records
    // Add a filter to only retrieve records with _requiredAttributeName field which contains _requiredAttributeValue
    let queryString: string =
      "?$select=" +
      TSWebAPI._currencyAttributeName +
      "&$filter=contains(" +
      TSWebAPI._requiredAttributeName +
      ",'" +
      TSWebAPI._requiredAttributeValue +
      "')";
    // store reference to 'this' so it can be used in the callback method
    var thisRef = this;
    // Invoke the Web API Retrieve Multiple call
    this._context.webAPI
      .retrieveMultipleRecords(TSWebAPI._entityName, queryString)
      .then(
        function(response: any) {
          // Retrieve Multiple Web API call completed successfully
          let count1: number = 0;
          let count2: number = 0;
          let count3: number = 0;
          // Loop through each returned record
          for (let entity of response.entities) {
            // Retrieve the value of _currencyAttributeName field
            let value: Number = entity[TSWebAPI._currencyAttributeName];
            // Check the value of _currencyAttributeName field and increment the correct counter
            if (value == 100) {
              count1++;
            } else if (value == 200) {
              count2++;
            } else if (value == 300) {
              count3++;
            }
          }
          // Generate HTML to inject into the fetch xml status div to showcase the results of the OData retrieve example
          let innerHtml: string =
            "Use above buttons to create or delete a record to see count update";
          innerHtml += "<br />";
          innerHtml += "<br />";
          innerHtml +=
            "Count of " +
            TSWebAPI._entityName +
            " records with " +
            TSWebAPI._currencyAttributeName +
            " of 100: " +
            count1;
          innerHtml += "<br />";
          innerHtml +=
            "Count of " +
            TSWebAPI._entityName +
            " records with " +
            TSWebAPI._currencyAttributeName +
            " of 200: " +
            count2;
          innerHtml += "<br />";
          innerHtml +=
            "Count of " +
            TSWebAPI._entityName +
            " records with " +
            TSWebAPI._currencyAttributeName +
            " of 300: " +
            count3;
          // Inject the HTML into the fetch xml status div
          if (thisRef._odataStatusContainerDiv) {
            thisRef._odataStatusContainerDiv.innerHTML = innerHtml;
          }
          // Inject a success message into the result div
          thisRef.updateResultContainerText("Record count refreshed");
        },
        function(errorResponse: any) {
          // Error handling code here
          thisRef.updateResultContainerTextWithErrorResponse(errorResponse);
        }
      );
  }
  /**
   * Helper method to inject HTML into result container div
   * @param statusHTML : HTML to inject into result container
   */
  private updateResultContainerText(statusHTML: string): void {
    if (this._resultContainerDiv) {
      this._resultContainerDiv.innerHTML = statusHTML;
    }
  }
  /**
   * Helper method to inject error string into result container div after failed Web API call
   * @param errorResponse : error object from rejected promise
   */
  private updateResultContainerTextWithErrorResponse(errorResponse: any): void {
    if (this._resultContainerDiv) {
      // Retrieve the error message from the errorResponse and inject into the result div
      let errorHTML: string = "Error with Web API call:";
      errorHTML += "<br />";
      errorHTML += errorResponse.message;
      this._resultContainerDiv.innerHTML = errorHTML;
    }
  }
  /**
   * Helper method to generate Label for Create Buttons
   * @param entityNumber : value to set _currencyAttributeNameFriendlyName field to for this button
   */
  private getCreateRecordButtonLabel(entityNumber: string): string {
    return (
      "Create record with " +
      TSWebAPI._currencyAttributeNameFriendlyName +
      " of " +
      entityNumber
    );
  }
  /**
   * Helper method to generate ID for Create Button
   * @param entityNumber : value to set _currencyAttributeNameFriendlyName field to for this button
   */
  private getCreateButtonId(entityNumber: string): string {
    return "create_button_" + entityNumber;
  }
  /**
   * Helper method to create HTML Button used for CreateRecord Web API Example
   * @param buttonLabel : Label for button
   * @param buttonId : ID for button
   * @param buttonValue : value of button (attribute of button)
   * @param onClickHandler : onClick event handler to invoke for the button
   */
  private createHTMLButtonElement(
    buttonLabel: string,
    buttonId: string,
    buttonValue: string | null,
    onClickHandler: (event?: any) => void
  ): HTMLButtonElement {
    let button: HTMLButtonElement = document.createElement("button");
    button.innerHTML = buttonLabel;
    if (buttonValue) {
      button.setAttribute("buttonvalue", buttonValue);
    }
    button.id = buttonId;
    button.classList.add("SampleControl_WebAPI_ButtonClass");
    button.addEventListener("click", onClickHandler);
    return button;
  }
  /**
   * Helper method to create HTML Div Element
   * @param elementClassName : Class name of div element
   * @param isHeader : True if 'header' div - adds extra class and post-fix to ID for header elements
   * @param innerText : innerText of Div Element
   */
  private createHTMLDivElement(
    elementClassName: string,
    isHeader: boolean,
    innerText?: string
  ): HTMLDivElement {
    let div: HTMLDivElement = document.createElement("div");
    if (isHeader) {
      div.classList.add("SampleControl_WebAPI_Header");
      elementClassName += "_header";
    }
    if (innerText) {
      div.innerText = innerText.toUpperCase();
    }
    div.classList.add(elementClassName);
    return div;
  }
}
```

## <a name="resources"></a>Ressourcen

```css
.SampleNamespace\.TSWebAPI {
  font-family: "SegoeUI-Semibold", "Segoe UI Semibold", "Segoe UI Regular",
    "Segoe UI";
  color: #1160b7;
}
.SampleNamespace\.TSWebAPI .TSWebAPI_Container {
  overflow-x: auto;
}
.SampleNamespace\.TSWebAPI .SampleControl_WebAPI_Header {
  color: rgb(51, 51, 51);
  font-size: 1rem;
  padding-top: 20px;
}
.SampleNamespace\.TSWebAPI .result_container {
  padding-bottom: 20px;
}
.SampleNamespace\.TSWebAPI .SampleControl_WebAPI_ButtonClass {
  text-decoration: none;
  display: inline-block;
  font-size: 14px;
  cursor: pointer;
  color: #1160b7;
  background-color: #ffffff;
  border: 1px solid black;
  padding: 5px;
  text-align: center;
  min-width: 300px;
  margin-top: 10px;
  margin-bottom: 5px;
  display: block;
}
```

Standardmäßig wird die im Beispiel Komponente so konfiguriert, dass Aktionen "Erstellen", "Abrufen", "Aktualisieren" für die `Account`-Entität durchgeführt und der die Felder "Name" und "Umsatz" in den Web-API-Beispielen festgelegt werden.

Um die Standardkonfiguration zu einer beliebigen Entität oder einen Feld zu ändern, aktualisieren Sie die Konfigurationswerte wie dargestellt.  

 ```TypeScript
  private static _entityName:string = "account";  
  private static _requiredAttributeName: string = "name";  
  private static _requiredAttributeValue: string = "Web API code component (Sample)";  
  private static _currencyAttributeName: string = "revenue";  
 ```

Die `createRecord`-Methode rendert drei Schaltflächen, mit denen Sie einen Firmendatensatz erstellen können, bei dem das Umsatzfeld auf verschiedene Werte (100, 200, 300) festgelegt werden kann.

Wenn Sie auf eine der Erstellen-Schaltflächen klicken, prüft der `onClick`-Ereignishandler der Schaltfläche den Wert der geklickten Schaltfläche und verwendet die Web-API-Aktion, um einen Firmendatensatz zu erstellen, bei dem das Umsatzfeld auf den Wert der Schaltfläche festgelegt ist. Der Namensfeld des Firmendatensatzes wird auf `Web API code component (Sample)` festgelegt und ein zufälliges `int`-Element wird dem Ende der Zeichenfolge angehängt. Die Rückrufmethode des Web-API-Aufrufs bringt das Ergebnis des Web-API-Aufrufs in das Ergebnis-div (Erfolg oder Fehler) des benutzerdefinierten Steuerelements ein.  
 
Die `deleteRecord`-Methode rendert eine Schaltfläche, mit der bei Aufurf ein Suchdialog geöffnet wird. Mit dem Suchdialog können Sie den Firmendatensatz auswählen, den Sie löschen möchten. Sobald ein Firmendatensatz aus dem Suchdialog ausgewählt wurde, wird er an `deleteRecord` übergeben, damit der Datensatz aus der Datenbank gelöscht wird. Die Rückrufmethode des Web-API-Aufrufs bringt das Ergebnis des Web-API-Aufrufs in das Ergebnis-div (Erfolg oder Fehler) des benutzerdefinierten Steuerelements ein.  

Die Methode FetchXML `retrieveMultiple` rendert eine Schaltfläche in der Codekomponente. Bei `onClick` auf diese Schaltfläche wird FetchXML generiert und an die `retrieveMultiple`-Funktion übergeben, um den Durchschnittswert des Umsatzfelds für alle Firmendatensätze zu berechnen. Die Rückrufmethode des Web-API-Aufrufs bringt das Ergebnis des Web-API-Aufrufs in das Ergebnis-div (Erfolg oder Fehler) des benutzerdefinierten Steuerelements ein.  

Die OData `retrieveMultiple`-Methode stellt eine Schaltfläche in der Codekomponente dar. `onClick` dieser Schaltfläche wird eine OData-Zeichenkette erzeugt und an die Funktion `retrieveMultiple` übergeben, um alle Kontendatensätze mit einem Namensfeld abzurufen, das wie die "Codekomponente Web API (Sample)" aussieht, was für alle Kontendatensätze gilt, die von diesem Codekomponentenbeispiel erstellt wurden.  

Nach erfolgreichem Abruf der Datensätze hat die Codekomponente die Logik, um zu zählen, wie viele Kontensätze das Erlösfeld auf 100, 200 oder 300 gesetzt haben, und diese Zählung in einen Odata-Statuscontainer div auf der Codekomponente anzuzeigen.  Die Rückrufmethode des Web-API-Aufrufs bringt das Ergebnis des Web-API-Aufrufs in das Ergebnis-div (Erfolg oder Fehler) des benutzerdefinierten Steuerelements ein.  

### <a name="related-topics"></a>Verwandte Themen

[Beispielkomponenten herunterladen](https://go.microsoft.com/fwlink/?linkid=2088525)<br/>
[PowerApps component framework-API-Referenz](../reference/index.md)<br/>
[Manifestschemareferenz des PowerApps component framework](../manifest-schema-reference/index.md)
