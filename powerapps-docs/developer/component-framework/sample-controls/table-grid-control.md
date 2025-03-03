---
title: " Tabellenrasterkomponente | Microsoft Docs"
description: Implementieren der Tabellenrasterkomponente
ms.custom: ''
manager: kvivek
ms.date: 10/01/2019
ms.service: powerapps
ms.topic: article
ms.author: nabuthuk
author: Nkrb
ms.openlocfilehash: 6a8c8dd1ef90203901ec4a675620a91ae1431f13
ms.sourcegitcommit: d9cecdd5a35279d78aa1b6c9fc642e36a4e4612c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/04/2019
ms.locfileid: "2754066"
---
# <a name="implementing-table-grid-component"></a>Implementieren der Tabellenrasterkomponente

Dieses Beispiel demonstriert, wie eine einfache Dataset-Komponente erstellt wird, Spaltenmetadatenbindung einer Ansicht, Datensatzbindung, mehrere Datensätze vom Blättern und Datensatznavigation zum Formular.
Die Komponentenüberschriftspalten die internen Datensatzwerte werden an vorhandene Ansichten gebunden.

> [!div class="mx-imgBorder"]
> ![Tabellenrasterkomponente](../media/table-grid-control.png "Tabellenrasterkomponente")

## <a name="available-for"></a>Verfügbar für 

Modellgestützte Apps  

## <a name="manifest"></a>Manifest 

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest>
    <control namespace="SampleNamespace" constructor="TSTableGrid" version="1.0.0" display-name-key="TS_TableGrid_Display_Key" description-key="TSTableGrid_Desc_Key" control-type="standard">
        <data-set name="simpleTableGrid" display-name-key="SimpleTableGridProperty_Display_Key">
        </data-set>
        <resources>
            <code path="index.ts" order="1" />
            <css path="css/TS_TableGrid.css" order="1" />
            <resx path="strings/TSTableGrid.1033.resx" version="1.0.0" />
        </resources>
    </control>
</manifest>
```

## <a name="code"></a>Code

```TypeScript
import { IInputs, IOutputs } from "./generated/ManifestTypes";
import DataSetInterfaces = ComponentFramework.PropertyHelper.DataSetApi;
type DataSet = ComponentFramework.PropertyTypes.DataSet;
// Define const here
const RowRecordId: string = "rowRecId";
// Style name of Load More Button
const LoadMoreButton_Hidden_Style = "LoadMoreButton_Hidden_Style";
export class TSTableGrid
  implements ComponentFramework.StandardControl<IInputs, IOutputs> {
  // Cached context object for the latest updateView
  private contextObj: ComponentFramework.Context<IInputs>;
  // Div element created as part of this control's main container
  private mainContainer: HTMLDivElement;
  // Table element created as part of this control's table
  private dataTable: HTMLTableElement;
  // Button element created as part of this control
  private loadPageButton: HTMLButtonElement;
  /**
   * Empty constructor.
   */
  constructor() {}
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
    // Need to track container resize so that control could get the available width. The available height won't be provided even this is true
    context.mode.trackContainerResize(true);
    // Create main table container div.
    this.mainContainer = document.createElement("div");
    this.mainContainer.classList.add("SimpleTable_MainContainer_Style");
    // Create data table container div.
    this.dataTable = document.createElement("table");
    this.dataTable.classList.add("SimpleTable_Table_Style");
    // Create data table container div.
    this.loadPageButton = document.createElement("button");
    this.loadPageButton.setAttribute("type", "button");
    this.loadPageButton.innerText = context.resources.getString(
      "PCF_TSTableGrid_LoadMore_ButtonLabel"
    );
    this.loadPageButton.classList.add(LoadMoreButton_Hidden_Style);
    this.loadPageButton.classList.add("LoadMoreButton_Style");
    this.loadPageButton.addEventListener(
      "click",
      this.onLoadMoreButtonClick.bind(this)
    );
    // Adding the main table and loadNextPage button created to the container DIV.
    this.mainContainer.appendChild(this.dataTable);
    this.mainContainer.appendChild(this.loadPageButton);
    container.appendChild(this.mainContainer);
  }
  /**
   * Called when any value in the property bag has changed. This includes field values, data-sets, global values such as container height and width, offline status, control metadata values such as label, visible, etc.
   * @param context The entire property bag available to control via Context Object; It contains values as set up by the customizer mapped to names defined in the manifest, as well as utility functions
   */
  public updateView(context: ComponentFramework.Context<IInputs>): void {
    this.contextObj = context;
    this.toggleLoadMoreButtonWhenNeeded(context.parameters.simpleTableGrid);
    if (!context.parameters.simpleTableGrid.loading) {
      // Get sorted columns on View
      let columnsOnView = this.getSortedColumnsOnView(context);
      if (!columnsOnView || columnsOnView.length === 0) {
        return;
      }
      let columnWidthDistribution = this.getColumnWidthDistribution(
        context,
        columnsOnView
      );
      while (this.dataTable.firstChild) {
        this.dataTable.removeChild(this.dataTable.firstChild);
      }
      this.dataTable.appendChild(
        this.createTableHeader(columnsOnView, columnWidthDistribution)
      );
      this.dataTable.appendChild(
        this.createTableBody(
          columnsOnView,
          columnWidthDistribution,
          context.parameters.simpleTableGrid
        )
      );
      this.dataTable.parentElement!.style.height =
        window.innerHeight - this.dataTable.offsetTop - 70 + "px";
    }
  }
  /**
   * It is called by the framework prior to a control receiving new data.
   * @returns an object based on nomenclature defined in manifest, expecting object[s] for property marked as “bound” or “output”
   */
  public getOutputs(): IOutputs {
    return {};
  }
  /**
   * Called when the control is to be removed from the DOM tree. Controls should use this call for cleanup.
   * i.e. canceling any pending remote calls, removing listeners, etc.
   */
  public destroy(): void {}
  /**
   * Get sorted columns on view
   * @param context
   * @return sorted columns object on View
   */
  private getSortedColumnsOnView(
    context: ComponentFramework.Context<IInputs>
  ): DataSetInterfaces.Column[] {
    if (!context.parameters.simpleTableGrid.columns) {
      return [];
    }
    let columns = context.parameters.simpleTableGrid.columns.filter(function(
      columnItem: DataSetInterfaces.Column
    ) {
      // some column are supplementary and their order is not > 0
      return columnItem.order >= 0;
    });
    // Sort those columns so that they will be rendered in order
    columns.sort(function(
      a: DataSetInterfaces.Column,
      b: DataSetInterfaces.Column
    ) {
      return a.order - b.order;
    });
    return columns;
  }
  /**
   * Get column width distribution
   * @param context context object of this cycle
   * @param columnsOnView columns array on the configured view
   * @returns column width distribution
   */
  private getColumnWidthDistribution(
    context: ComponentFramework.Context<IInputs>,
    columnsOnView: DataSetInterfaces.Column[]
  ): string[] {
    let widthDistribution: string[] = [];
    // Considering need to remove border & padding length
    let totalWidth: number = context.mode.allocatedWidth - 250;
    let widthSum = 0;
    columnsOnView.forEach(function(columnItem) {
      widthSum += columnItem.visualSizeFactor;
    });
    let remainWidth: number = totalWidth;
    columnsOnView.forEach(function(item, index) {
      let widthPerCell = "";
      if (index !== columnsOnView.length - 1) {
        let cellWidth = Math.round(
          (item.visualSizeFactor / widthSum) * totalWidth
        );
        remainWidth = remainWidth - cellWidth;
        widthPerCell = cellWidth + "px";
      } else {
        widthPerCell = remainWidth + "px";
      }
      widthDistribution.push(widthPerCell);
    });
    return widthDistribution;
  }
  private createTableHeader(
    columnsOnView: DataSetInterfaces.Column[],
    widthDistribution: string[]
  ): HTMLTableSectionElement {
    let tableHeader: HTMLTableSectionElement = document.createElement("thead");
    let tableHeaderRow: HTMLTableRowElement = document.createElement("tr");
    tableHeaderRow.classList.add("SimpleTable_TableRow_Style");
    columnsOnView.forEach(function(columnItem, index) {
      let tableHeaderCell = document.createElement("th");
      tableHeaderCell.classList.add("SimpleTable_TableHeader_Style");
      let innerDiv = document.createElement("div");
      innerDiv.classList.add("SimpleTable_TableCellInnerDiv_Style");
      innerDiv.style.maxWidth = widthDistribution[index];
      innerDiv.innerText = columnItem.displayName;
      tableHeaderCell.appendChild(innerDiv);
      tableHeaderRow.appendChild(tableHeaderCell);
    });
    tableHeader.appendChild(tableHeaderRow);
    return tableHeader;
  }
  private createTableBody(
    columnsOnView: DataSetInterfaces.Column[],
    widthDistribution: string[],
    gridParam: DataSet
  ): HTMLTableSectionElement {
    let tableBody: HTMLTableSectionElement = document.createElement("tbody");
    if (gridParam.sortedRecordIds.length > 0) {
      for (let currentRecordId of gridParam.sortedRecordIds) {
        let tableRecordRow: HTMLTableRowElement = document.createElement("tr");
        tableRecordRow.classList.add("SimpleTable_TableRow_Style");
        tableRecordRow.addEventListener("click", this.onRowClick.bind(this));
        // Set the recordId on the row dom
        tableRecordRow.setAttribute(
          RowRecordId,
          gridParam.records[currentRecordId].getRecordId()
        );
        columnsOnView.forEach(function(columnItem, index) {
          let tableRecordCell = document.createElement("td");
          tableRecordCell.classList.add("SimpleTable_TableCell_Style");
          let innerDiv = document.createElement("div");
          innerDiv.classList.add("SimpleTable_TableCellInnerDiv_Style");
          innerDiv.style.maxWidth = widthDistribution[index];
          innerDiv.innerText = gridParam.records[
            currentRecordId
          ].getFormattedValue(columnItem.name);
          tableRecordCell.appendChild(innerDiv);
          tableRecordRow.appendChild(tableRecordCell);
        });
        tableBody.appendChild(tableRecordRow);
      }
    } else {
      let tableRecordRow: HTMLTableRowElement = document.createElement("tr");
      let tableRecordCell: HTMLTableCellElement = document.createElement("td");
      tableRecordCell.classList.add("No_Record_Style");
      tableRecordCell.colSpan = columnsOnView.length;
      tableRecordCell.innerText = this.contextObj.resources.getString(
        "PCF_TSTableGrid_No_Record_Found"
      );
      tableRecordRow.appendChild(tableRecordCell);
      tableBody.appendChild(tableRecordRow);
    }
    return tableBody;
  }
  /**
   * Row Click Event handler for the associated row when being clicked
   * @param event
   */
  private onRowClick(event: Event): void {
    let rowRecordId = (event.currentTarget as HTMLTableRowElement).getAttribute(
      RowRecordId
    );
    if (rowRecordId) {
      let entityreference = this.contextObj.parameters.simpleTableGrid.records[
        rowRecordId
      ].getNamedreference();
      let entityFormOptions = {
        entityName: entityreference.entityType!,
        entityId: entityreference.id
      };
      this.contextObj.navigation.openForm(entityFormOptions);
    }
  }
  /**
   * Toggle 'LoadMore' button when needed
   */
  private toggleLoadMoreButtonWhenNeeded(gridParam: DataSet): void {
    if (
      gridParam.paging.hasNextPage &&
      this.loadPageButton.classList.contains(LoadMoreButton_Hidden_Style)
    ) {
      this.loadPageButton.classList.remove(LoadMoreButton_Hidden_Style);
    } else if (
      !gridParam.paging.hasNextPage &&
      !this.loadPageButton.classList.contains(LoadMoreButton_Hidden_Style)
    ) {
      this.loadPageButton.classList.add(LoadMoreButton_Hidden_Style);
    }
  }
  /**
   * 'LoadMore' Button Event handler when load more button clicks
   * @param event
   */
  private onLoadMoreButtonClick(event: Event): void {
    this.contextObj.parameters.simpleTableGrid.paging.loadNextPage();
    this.toggleLoadMoreButtonWhenNeeded(
      this.contextObj.parameters.simpleTableGrid
    );
  }
}
```

## <a name="resources"></a>Ressourcen

```css
.SampleNamespace\.TSTableGrid table.SimpleTable_Table_Style {
  border-spacing: 0;
  text-align: left;
  width: 100%;
  margin: 0 auto;
  overflow: auto;
  height: 94%;
  display: block;
}
.SampleNamespace\.TSTableGrid div.SimpleTable_TableCellInnerDiv_Style {
  word-wrap: break-word;
  overflow: hidden;
  text-overflow: ellipsis;
  line-height: 1.5rem;
  max-height: 1.5rem;
}
.SampleNamespace\.TSTableGrid th.SimpleTable_TableHeader_Style {
  height: 3rem;
  font-family: "Segoe UI Regular", "Segoe UI", Arial, Sans-Serif;
  font-size: 1rem;
  line-height: 1.384;
  background-color: rgb(0, 0, 0);
  color: #fff;
  text-align: left;
  padding: 0.5rem;
  border-left: 0.1rem solid rgba(255, 255, 255, 0.1);
  vertical-align: middle;
  width: 100vw;
}
.SampleNamespace\.TSTableGrid tr.SimpleTable_TableRow_Style {
  height: 3.5rem;
  background-color: #fff;
  color: #333;
}
.SampleNamespace\.TSTableGrid tr.SimpleTable_TableRow_Style:hover {
  cursor: pointer;
  border: solid thin rgb(59, 121, 183);
  background: rgba(160, 160, 160, 0.15);
}
.SampleNamespace\.TSTableGrid td.SimpleTable_TableCell_Style {
  font-size: 1rem;
  line-height: 1.467;
  padding: 0 0.5rem;
  vertical-align: middle;
  width: 100vw;
  font-weight: bold;
  font-family: "Segoe UI Light";
  color: rgb(59, 121, 183);
}
.SampleNamespace\.TSTableGrid td.No_Record_Style {
  text-align: center;
  padding: 20px;
}
.SampleNamespace\.TSTableGrid table.SimpleIncrement_Button_Style {
  text-decoration: none;
  display: inline-block;
  font-size: 14px;
  margin: 4px 6px;
  cursor: pointer;
  color: white;
  border-radius: 10px;
  background-color: black;
  border: none;
  padding: 5px;
  text-align: center;
}
.SampleNamespace\.TSTableGrid input.SimpleIncrement_Input_Error_Style {
  color: red;
}
.SampleNamespace\.TSTableGrid button.LoadMoreButton_Hidden_Style {
  display: none;
}
.SampleNamespace\.TSTableGrid button.LoadMoreButton_Style {
  background-color: #e5e5e5;
  font-size: 1.3rem;
  font-weight: bold;
  height: 6%;
  text-align: center;
  width: 100%;
  border: none;
}
```

```xml
<?xml version="1.0" encoding="utf-8"?>
<root>
<xsd:schema id="root" xmlns="" xmlns:xsd="https://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata">
<xsd:import namespace="https://www.w3.org/XML/1998/namespace" />
<xsd:element name="root" msdata:IsDataSet="true">
  <xsd:complexType>
    <xsd:choice maxOccurs="unbounded">
      <xsd:element name="metadata">
        <xsd:complexType>
          <xsd:sequence>
            <xsd:element name="value" type="xsd:string" minOccurs="0" />
          </xsd:sequence>
          <xsd:attribute name="name" use="required" type="xsd:string" />
          <xsd:attribute name="type" type="xsd:string" />
          <xsd:attribute name="mimetype" type="xsd:string" />
          <xsd:attribute ref="xml:space" />
        </xsd:complexType>
      </xsd:element>
      <xsd:element name="assembly">
        <xsd:complexType>
          <xsd:attribute name="alias" type="xsd:string" />
          <xsd:attribute name="name" type="xsd:string" />
        </xsd:complexType>
      </xsd:element>
      <xsd:element name="data">
        <xsd:complexType>
          <xsd:sequence>
            <xsd:element name="value" type="xsd:string" minOccurs="0" msdata:Ordinal="1" />
            <xsd:element name="comment" type="xsd:string" minOccurs="0" msdata:Ordinal="2" />
          </xsd:sequence>
          <xsd:attribute name="name" type="xsd:string" use="required" msdata:Ordinal="1" />
          <xsd:attribute name="type" type="xsd:string" msdata:Ordinal="3" />
          <xsd:attribute name="mimetype" type="xsd:string" msdata:Ordinal="4" />
          <xsd:attribute ref="xml:space" />
        </xsd:complexType>
      </xsd:element>
      <xsd:element name="resheader">
        <xsd:complexType>
          <xsd:sequence>
            <xsd:element name="value" type="xsd:string" minOccurs="0" msdata:Ordinal="1" />
          </xsd:sequence>
          <xsd:attribute name="name" type="xsd:string" use="required" />
        </xsd:complexType>
      </xsd:element>
    </xsd:choice>
  </xsd:complexType>
</xsd:element>
</xsd:schema>
<resheader name="resmimetype">
<value>text/microsoft-resx</value>
</resheader>
<resheader name="version">
<value>2.0</value>
</resheader>
<resheader name="reader">
<value>System.Resources.ResXResourceReader, System.Windows.Forms, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089</value>
</resheader>
<resheader name="writer">
<value>System.Resources.ResXResourceWriter, System.Windows.Forms, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089</value>
</resheader>
<data name="PCF_TSTableGrid_LoadMore_ButtonLabel" xml:space="preserve">
<value>Load More</value>
<comment>Label for TSTableGrid's Load More Paging Button</comment>
</data>
<data name="PCF_TSTableGrid_No_Record_Found" xml:space="preserve">
<value>No records found.</value>
<comment>No records found if no records</comment>
</data>
</root>
```

Spaltenüberschriftbindung an die Ansicht:

Ansichtsspalteninformationen liegen bei `context.parameters.[dataset_property_name].columns`. Es ist ein Array-Typ.

Datensatzbindung:

- Die sortierten Datensatz-IDs befinden sich bei `context.parameters.[dataset_property_name].sortedRecordIds`
- Alle Datensatzinformationen befinden sich bei `context.parameters.[dataset_property_name].records` 
- Für jedes Datensatzobjekt, `context.parameters.[dataset_property_name].records[record_Id]` 
- Formatierter Wert kann bei `getFormattedValue` abgerufen werden 

Nach Bedarf mehr Datenseiten laden:

`context.parameters.[dataset_property_name].paging` bietet Blätterfunktion wie `hasNextPage` und `loadNextPage`. Die `Load More`-Schaltfläche wird angezeigt, wenn sie Daten für die nächste Seite hat.

Dieses Beispiel demonstriert auch, wie die Komponente der Container-Anpassung lauscht. 

Die `trackContainerResize`-Methode soll in der [init](../reference/control/init.md)-Methode aufgerufen werden, damit `mode.allocatedWidth` und `mode.allocatedHeight` jedes Mal bereitgestellt werden, wenn [updateView](../reference/control/updateview.md) aufgerufen wird. Wenn diese Methode nicht anfänglich aufgerufen wird, wird `allocatedWidth` und `allocatedHeight` nicht bereitgestellt.

Wenn allocatedHeight –1 ist, bedeutet das, das die Höhe nicht begrenzt ist. Die Komponente soll ihre Höhe anhand der bereitgestellte Breite anpassen.

### <a name="related-topics"></a>Verwandte Themen

[Beispielkomponenten herunterladen](https://go.microsoft.com/fwlink/?linkid=2088525)<br/>
[PowerApps component framework-API-Referenz](../reference/index.md)<br/>
[Manifestschemareferenz des PowerApps component framework](../manifest-schema-reference/index.md)