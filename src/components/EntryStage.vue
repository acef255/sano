
<template>
  <div id="bodi" >
    <div id="container">
        <h3 style="margin: 20px">Entry Stage</h3>
        <form id="entryStage" @submit.prevent >
          
          <div id="fieldset1">

            <div id="FSchild1">
              <div class="field">
                <label for="financialyear">Financial year</label>
                <ejs-combobox :dataSource='financialYearSrc'   mode='Delimiter'  id="financialyear" allowCustom="true"
                      :hideSelectedItem='false'  :allowMultiSelection='true'  :allowFiltering='allowFiltering' 
                      :fields='remoteFields' placeholder='select an item' popupWidth="250px" popupHeight="200px">
                </ejs-combobox>
                <span class="bar"></span>  
              </div>
              <div class="field">
                <label for="inputDateOfEntry">Date of entry</label>
                <input type="date" id="inputDateOfEntry"  name="dateOfEntry"  placeholder="DD/MM/YY" autocomplete="off" onkeydown="return (event.keyCode!=13);"> 
                <span class="bar"></span>
              </div>                
            </div>

            <div id="FSchild2">
              <div class="field">
                <label for="inputVendorField">Vendor name</label>
                <ejs-combobox :dataSource='vendorSrc'  allowCustomValue='allowCustomValue' id="inputvendor"  mode='Delimiter'  
                    :hideSelectedItem='false'  :allowMultiSelection='true' onkeydown="return (event.keyCode!=13);"
                    :fields='remoteFields' placeholder='select an item'
                    popupWidth="250px" popupHeight="200px">
                </ejs-combobox>
                <span class="bar"></span>
              </div>
              <div class="field">
                <label for="inputInvoiceNo">Invoice n°</label>
                <input  type="number"  id="inputInvoiceNo" name="invoiceN°" onkeydown="return (event.keyCode!=13);" v-on:keyup.enter="getInvoiceAndFill()" >
                <span class="bar"></span>
              </div>
              <div class="field">
                <label for="inputDateOfInvoice"> Date of invoice</label>
                <input  type="text"  id="inputDateOfInvoice" name="dateOfInvoice" onkeydown="return (event.keyCode!=13);">
                <span class="bar"></span>
              </div>
            </div>

            <div id="FSchild3">
              <div class="field">
                <label for="inputAssetType">Asset type</label>
                <ejs-combobox :dataSource='assetTypeSrc'   allowCustomValue='allowCustomValue' id="inputAssetType" mode='Delimiter'  
                    :hideSelectedItem='false'  :allowMultiSelection='true' onkeydown="return (event.keyCode!=13);"
                    :fields='remoteFields' placeholder='select an item'
                    popupWidth="250px" popupHeight="200px">
                </ejs-combobox>
              </div>
              <div class="field">
                <label for="inputFund">Fund</label>
                <ejs-combobox :dataSource='invoiceSrc' allowCustomValue='allowCustomValue' id="inputFund" mode='Delimiter'  
                    :hideSelectedItem='false'  :allowMultiSelection='true' onkeydown="return (event.keyCode!=13);"
                    :fields='remoteFieldsInvoiceFund' placeholder='select an item'
                    popupWidth="250px" popupHeight="200px">
                </ejs-combobox>
              </div>
            </div>
          
          </div>
          
          <div style="width: 100%; height:10px;  border-bottom: 1px solid; opacity: 0.3"></div>
          <div style="width: 100%; height:10px;  border-bottom: 1px solid; opacity: 0.3"></div>
          <div style="width: 100%; height:10px;  border-bottom: 1px solid; opacity: 0.3"></div>
          
          <div id="fieldsetMiddle">
            <div class="field" id="fieldInputSN°">
              <label for="inputS.N°">S.N°</label>
              <input type="number" id="inputS.N°"  name="S.N°" autocomplete="off" onkeydown="return (event.keyCode!=13);">  
              <span class="bar"></span>
            </div>
            
            <div class="field" id="fieldInputPO">
              <label for="inputPO">PO Number/ Requisition below 25000/-</label>
              <input type="text" id="inputPO"  name="PO"  autocomplete="off" onkeydown="return (event.keyCode!=13);"> 
              <span class="bar"></span>
            </div>
            
            <div class="field" id=fieldPurchasefor>
              <label for="purchasefor">Purchase for</label>
              <ejs-combobox :dataSource='departmentSrc' id="purchasefor" mode='Delimiter'  onkeydown="return (event.keyCode!=13);"
                  :allowMultiSelection='true'     v-model="pf"  @submit.prevent 
                  :fields='remoteFields' placeholder='select an item' 
                  popupWidth="250px" popupHeight="200px">
              </ejs-combobox>
            </div>

          </div>
          
          <form @submit.prevent>
            <div id="fieldset2" >
              <div class="field">
                <label for="mainCat">Stock Register/ Main Category</label>
                <ejs-combobox :dataSource='mainCategorySrc' mode='Delimiter' id="mainCat"  onkeydown="return (event.keyCode!=13);"
                    :hideSelectedItem='false'  :allowMultiSelection='true'   v-model="mc"
                    :fields='remoteFields' placeholder='select an item' @submit.prevent
                    popupWidth="250px" popupHeight="200px">
                </ejs-combobox>
                <p id="StockRegMainCatp" style="display: none; padding: 5px ">{{mc}}</p>
              </div>
              
              <div class="field">
                <label for="subCat">Stock Register/ sub Category</label>
                <ejs-combobox :dataSource='subCategorySrc' mode='Delimiter'  id="subCat" 
                    :hideSelectedItem='false'  :allowMultiSelection='true'  @submit.prevent
                    :fields='remoteFields' placeholder='select an item' v-model="sc" onkeydown="return (event.keyCode!=13);"
                    popupWidth="250px" popupHeight="200px">
                </ejs-combobox>
                <p  id="StockRegSubCp" style="display: none; padding: 5px ">{{sc}}</p>
              </div>
              
              <div class="field">
                <label for="nameInvoice">Item name as per Invoice</label>
                <input  type="text" class="paddedinput"  id="nameInvoice" name="itemNameAsPerInvoice" autocomplete="off"  onkeydown="return (event.keyCode!=13);"> 
                <span class="bar"></span>
              </div>
              
              <div class="field">
                <label for="nameCoding">Item name for coding</label>
                <ejs-combobox :dataSource='itemsSrc' mode='Delimiter'  id="nameCoding" onkeydown="return (event.keyCode!=13);"
                    :hideSelectedItem='false'  :allowMultiSelection='true'  @submit.prevent
                    :fields='remoteFieldsItemNameCoding' placeholder='select an item'  v-model="ic"
                    popupWidth="250px" popupHeight="200px">
                </ejs-combobox>
                <p  id="ItemNameAsForCodingp" style="display: none; padding: 5px ">{{ic}}</p>
              </div>

              <div class="field">
                <label for="assetCode">Asset Code</label>
                <input type="text" id="assetCode" class="paddedinput"  name="assetCode" autocomplete="off"  onkeydown="return (event.keyCode!=13);">  
                <span class="bar"></span>
              </div>
              
              <div class="field">
                <label for="invoiceQty">Item Quantity (Recd. Via Invoice)</label>
                <input type="number" id="invoiceQty" class="paddedinput"  name="itemQ(RECD.viaInvoice)"  autocomplete="off" onkeydown="return (event.keyCode!=13);"> 
                <span class="bar"></span>
              </div>

              <div class="field">
                <label for="prevQty">Item Quantity (Previous available to Store)</label>
                <input  type="number" id="prevQty" class="paddedinput"  name="itemQ(Prev.AvailableStore)"  autocomplete="off" onkeydown="return (event.keyCode!=13);">
                <span class="bar"></span>
              </div>
              
              <div class="field">
                <label for="totalQty">Total Item Quantity</label>
                <input  type="number"  id="totalQty" class="paddedinput"  name="totaltemQ" onkeydown="return (event.keyCode!=13);" >
                <span class="bar"></span>
              </div>
              
              <div class="field">
                <label for="prevSrlNo">Previous available Sr.No</label>
                <input  type="number"  id="prevSrlNo" class="paddedinput"  name="prevAvailableSr.No" onkeydown="return (event.keyCode!=13);">
                <span class="bar"></span>
              </div>
              
              <div class="field">
                <label for="lastSrlAssigned">Item Last Sr. No. (As per coding)</label>
                <input  type="number"  id="lastSrlAssigned" class="paddedinput"  name="itemItemLastSr.N°" onkeydown="return (event.keyCode!=13);">
                <span class="bar"></span>
              </div>
              
              <div class="field">
                <label for="newNumber">Item New Number</label>
                <input  type="number"  id="newNumber" class="paddedinput"  name="itemNewNumber" onkeydown="return (event.keyCode!=13);">
                <span class="bar"></span>
              </div>

              <div class="field">
                <label for="itemMake">Item Make</label>  
                <input  type="text"  id="itemMake" class="paddedinput"  name="itemMake" autocomplete="off" onkeydown="return (event.keyCode!=13);">
                <span class="bar"></span>
              </div>
              
              <div class="field">
                <label for="itemSrlNo">Item S.N°</label>
                <input type="number" id="itemSrlNo" class="paddedinput"   name="itemS.N°" autocomplete="off" onkeydown="return (event.keyCode!=13);">  
                <span class="bar"></span>
              </div>
              
              <div class="field">
                <label for="basicRate">Basic Rate</label>
                <input type="number" id="basicRate" class="paddedinput"   name="basicRate"  autocomplete="off" onkeydown="return (event.keyCode!=13);"> 
                <span class="bar"></span>
              </div>

              <div class="field">
                <label for="discount">Discount (%)</label>
                <input  type="number" id="discount" class="paddedinput"  name="discount(%)"  autocomplete="off" onkeydown="return (event.keyCode!=13);">
                <span class="bar"></span>
              </div>
              
              <div class="field">
                <label for="tax">Tax (%)</label>
                <input  type="number"  id="tax" class="paddedinput"  name="tax(%)" onkeydown="return (event.keyCode!=13);">
                <span class="bar"></span>
              </div>

              <div class="field">
                <label for="amount">Amount</label>
                <input  type="number"  id="amount" class="paddedinput"  name="amount" onkeydown="return (event.keyCode!=13);">
                <span class="bar"></span>
              </div>
               
              <div class="field">
                <label for="stockRegPage">Stock Register Page No.</label>
                <input  type="number"  id="stockRegPage" class="paddedinput"  name="stockRegPageN°" onkeydown="return (event.keyCode!=13);">
                <span class="bar"></span>
              </div>

            </div>
          
          </form>
          
          <div id="addItem" @click="addItem()" style="cursor: pointer; margin: 15px">Add item</div>
          <div id="tableContainer">
            
            <DataTable class="Datatable" :header-fields="headerFields" :data="mainCategoryCol || []" not-found-msg="" >   
              <div slot="F1New" slot-scope="props">
                <ejs-combobox 
                    :dataSource='mainCategorySrc' 
                    mode='Delimiter'  id="subCat" 
                    :value="props.rowData.F1"
                    @keyup="change($event, props.rowData.id, mainCategoryCol);"
                    class="form-control">
                </ejs-combobox>
        <!--        <textarea
                    type="text"
                    :value="props.rowData.F1"
                    @keyup="change($event, props.rowData.id, mainCategoryCol);"
                    class="form-control">
                </textarea> -->
              </div>
            </Datatable>
            
            <DataTable class="Datatable" :header-fields="headerFields" :data="subCategoryCol || []" not-found-msg=" " >  
              <div slot="F1New" slot-scope="props">
                <textarea id= "textarea1"
                    type="text"
                    :value="props.rowData.F1"
                    @keyup="change($event, props.rowData.id, subCategoryCol);"
                    class="form-control">
                </textarea>
              </div>
              
            </Datatable>
            
            <DataTable class="Datatable" :header-fields="headerFields" :data="itemNameCol || []" not-found-msg=" " > 
              <div slot="F1New" slot-scope="props">
                <textarea
                    type="text"
                    :value="props.rowData.F1"
                    @keyup="change($event, props.rowData.F1, itemNameCol);"
                    class="form-control">
                </textarea>
              </div>
              
            </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="nameForCodingCol || [] " not-found-msg=""  > 
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="change($event, props.rowData.id, nameForCodingCol);">
                    </textarea>
                  </div>          
                </Datatable>

                <DataTable class="Datatable" :header-fields="headerFields" :data="assetCodeCol || []" not-found-msg=""  >   
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="change($event, props.rowData.F1, assetCodeCol);"
                      class="form-control"
                    ></textarea>
                  </div>        
                </Datatable>

                <DataTable class="Datatable" :header-fields="headerFields" :data="itemQuantityCol || []" not-found-msg=""  > 
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="change($event, props.rowData.F1, itemQuantityCol);"
                      class="form-control"
                    ></textarea>
                  </div>        
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="itemQuantityPreviousCol || []" not-found-msg=""  >   
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="change($event, props.rowData.F1, itemQuantityPreviousCol);"
                      class="form-control"
                    ></textarea>
                  </div>      
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="totalItemQuantityCol || []" not-found-msg=""  > 
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="change($event, props.rowData.F1, totalItemQuantityCol);"
                      class="form-control"
                    ></textarea>
                  </div>      
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="previousAvailableSerialNoCol || []" not-found-msg=""  > 
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="change($event, props.rowData.F1, previousAvailableSerialNoCol);"
                      class="form-control"
                    ></textarea>
                  </div> 
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="itemLastSerialNoCol || []" not-found-msg="">
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="change($event, props.rowData.F1, itemLastSerialNoCol);"
                      class="form-control"
                    ></textarea>
                  </div>
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="itemNewNumberCol || []" not-found-msg="" >
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="change($event, props.rowData.F1, itemNewNumberCol);"
                      class="form-control"
                    ></textarea>
                  </div>
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="itemMakeCol || []" not-found-msg="" > 
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="change($event, props.rowData.F1, itemMakeCol);"
                      class="form-control"
                    ></textarea>
                  </div>
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="itemSerialNoCol || []" not-found-msg="" > 
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="change($event, props.rowData.F1, itemSerialNoCol);"
                      class="form-control"
                    ></textarea>
                  </div>
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="basicRateCol || []" not-found-msg=""  > 
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="change($event, props.rowData.F1, basicRateCol);"
                      class="form-control"
                    ></textarea>
                  </div> 
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="discountCol || []" not-found-msg="">
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="change($event, props.rowData.F1, discountCol);"
                      class="form-control"
                    ></textarea>
                  </div>
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="taxCol || []" not-found-msg="" >
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="change($event, props.rowData.id, taxCol);"
                      class="form-control"
                    ></textarea>
                  </div>
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="amountCol || []" not-found-msg="" > 
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="change($event, props.rowData.id, amountCol);"
                      class="form-control"
                    ></textarea>
                  </div>
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="stockRegisterPageNoCol || []" not-found-msg="" > 
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="change($event, props.rowData.id, stockRegisterPageNoCol);"
                      class="form-control"
                    ></textarea>
                  </div>
                </Datatable>
                
        </div>
                
    
         <div class="field" id="fieldInputTA">
                <label for="inputTotalAmount">Total Amount</label>
                <input  type="number"  id="inputTotalAmount" name="totalAmount" onkeydown="return (event.keyCode!=13);">
                <span class="bar"></span>
        </div>
          
         <div id="divConfirm">
                <label>Confirm Entry</label>
                <button id="yes"  value="sendEntry" @click="sendEntry()" onkeydown="return (event.keyCode!=13);" >Yes</button>
                <button id="no"  value="cancel" onClick="window.location.reload()" onkeydown="return (event.keyCode!=13);">No</button>
        </div>
          
        </form>
    </div>
  </div>

</template>

 <!--

<template>

  <div>
      <select v-model="financialYear">
        <option v-for="year in financialYear" 
                v-bind:value="year.name"
                v-bind:key="year.id">
            {{ year.name }}
        </option>
      </select>
      <span>Selected: {{ year.name }}</span>

      <div id="vue-root">
          <datatable :columns="columns" :data="rows"></datatable>
      </div>
  </div>
</template>

-->


<script>

import Vue from 'vue';
//import * as data from './dataSource.json';
import{ MultiSelectPlugin, } from '@syncfusion/ej2-vue-dropdowns' ;
Vue.use(MultiSelectPlugin);
import{ DropDownListPlugin, } from '@syncfusion/ej2-vue-dropdowns' ;
Vue.use(DropDownListPlugin);
import{ ComboBoxPlugin, } from '@syncfusion/ej2-vue-dropdowns' ;
Vue.use(ComboBoxPlugin);

import{ DataManager, WebApiAdaptor,} from '@syncfusion/ej2-data' ;

import { DataTable } from 'v-datatable-light';

//=======================================================================================
//Table

const comboboxKeys = [
      "mainCat", "subCat", "nameCoding"
];

const elementKeys = [
      "nameInvoice",
      "assetCode", "invoiceQty", "prevQty", "totalQty", "prevSrlNo",
      "lastSrlAssigned", "newNumber", "itemMake", "itemSrlNo",
      "basicRate", "discount", "tax", "amount", "stockRegPage",
      "itemId" //hidden
];

const columns = comboboxKeys.concat(elementKeys);

var generateTable = function() {
    let tbl = new Map();

    for (var key of columns) {
        tbl.set(key, new Array());
    }
    console.log({"Table": tbl});
    return tbl;
};

var table = generateTable();

//========================================================================================

class ApiURL {
    constructor(type) {
        this.type = type;
    }
    path() {
      return 'http://localhost:8080/'.concat(this.type, '/all');
    }
}

//Fetch all dropdown data
var fetchAllData = function() {

    const api = [
        new ApiURL('financialyear'),
        new ApiURL('vendor'),
        new ApiURL('assettype'),
        new ApiURL('maincategory'),
        new ApiURL('subcategory'),
        new ApiURL('department'),
        new ApiURL('item')
    ]
    console.log({"API directory": api});

    let fetchedData = new Map();

    for (var dir of api) {
      let dataSrc = new DataManager({
            url: dir.path(),
            adaptor: new WebApiAdaptor,
            crossDomain: true
        });

        fetchedData.set(dir.type, dataSrc);
    }

    console.log({"Fetched data": fetchedData});
    return fetchedData;
}

const allFetchedData = fetchAllData();

//==============================================================================

var getInvoiceFromServer = function(invoiceNo, callback) {
    var xhttp = new XMLHttpRequest();
    xhttp.onreadystatechange = function() {
     // let response = JSON.parse(xhttp.responseText);
      if (this.readyState == 4 && this.status == 200) {
          console.log({"Fetched invoice: ": JSON.parse(xhttp.responseText)});
          callback(JSON.parse(xhttp.responseText));
      } else if (this.status == 404){
          console.log("Error");
          alert("Invoice n° " + invoiceNo + " not found.")
      }
    };
    xhttp.open("GET", "http://localhost:8080/invoice/findno/".concat(invoiceNo), true);
    xhttp.send();
};


//=================================================================================

var sendItems = [];

class Item {
    constructor(itemId, args) {
        this.itemId = itemId; 
        this.args = args;
        this.newNumber = args.get("newNumber");
        this.basicRate = args.get("basicRate");
        this.discount = args.get("discount");
        this.tax = args.get("tax");
        this.amount = args.get("amount");
    }   

    pushToTable() {
        for (var key of columns) {
            table.get(key).push({F1: this.args.get(key)});
        }

        let item = {
          "item": {
              "id": this.itemId
          },
          "itemNewSerialNumber": this.newNumber,
          "basicRate": this.basicRate,
          "discount": this.discount,
          "tax": this.tax,
          "amount": this.amount
        }
        sendItems.push(item);
    }
}

//========

var isBlank = function(field) {
    if (field == null || field == undefined
        || field == '' || !field || 0 === field.length) {
        return true;
    }
    return false;
}
//================================


window.onload = function() {   
     
}   

export default Vue.extend({
  name: 'form1', 
  components: {
    DataTable
  },
  
  data: function() {
    return {

      financialYearSrc: allFetchedData.get("financialyear"),
      vendorSrc: allFetchedData.get("vendor"),
      invoiceSrc: allFetchedData.get("invoice"),
      assetTypeSrc: allFetchedData.get("assettype"),
      mainCategorySrc: allFetchedData.get("maincategory"),
      subCategorySrc: allFetchedData.get("subcategory"),
      departmentSrc: allFetchedData.get("department"),
      itemsSrc: allFetchedData.get("item"),

      remoteFields: {value: 'id', text:'name'},
      remoteFieldsInvoiceN: {value: 'id' ,text:'number'  },
      remoteFieldsInvoiceDateEntry: {value: 'id' ,text:'entryDate' },
      remoteFieldsInvoiceDate: {value: 'id' ,text:'date' },
      remoteFieldsInvoiceFinancialYear: {value: 'financialYear.id' ,text:'financialYear.name' },
      remoteFieldsInvoiceVendor: {value: 'vendor.id' ,text:'vendor.name' },
      remoteFieldsInvoiceAssetType: {value: 'assetType.id' ,text:'assetType.name' },
      remoteFieldsInvoiceFund: {value: 'id' ,text:'fund'  },
      remoteFieldsInvoiceTotalAmount: {value: 'id' ,text:'totalAmount'},
      remoteFieldsItemNameCoding: {value: 'id' ,text:'finalCode'},
           
      keySettings: {
        saveRequest: "",
      },
      
      //Vue properties default
      pf : null,
      mc : null,
      sc : null,
      ic : null,
     
      headerFields: [
        {
          name: "F1",
          label: "",
          customElement: "F1New"
        },
      ],
    
      mainCategoryCol: table.get("mainCat"),  
      subCategoryCol: table.get("subCat"),  
      itemNameCol: table.get("nameInvoice"),  
      nameForCodingCol: table.get("nameCoding"),  
      assetCodeCol: table.get("assetCode"),
      itemQuantityCol: table.get("invoiceQty"),  
      itemQuantityPreviousCol: table.get("prevQty"),  
      totalItemQuantityCol: table.get("totalQty"),  
      previousAvailableSerialNoCol: table.get("prevSrlNo"),  
      itemLastSerialNoCol: table.get("lastSrlAssigned"),  
      itemNewNumberCol: table.get("newNumber"),
      itemMakeCol: table.get("itemMake"),  
      itemSerialNoCol: table.get("itemSrlNo"),  
      basicRateCol: table.get("basicRate"),  
      discountCol: table.get("discount"),  
      taxCol: table.get("tax"),  
      amountCol: table.get("amount"),
      stockRegisterPageNoCol: table.get("stockRegPage"),
      hiddenItemId: table.get("itemId"),
    
      allowFiltering: true,
      customValue: '',
      newItem: '',
      query: '',
      F1: null,     
  };
},

methods: {

  change: function(event, cell, column) {
      console.log("cell", cell);
      this.data = column.map(item => {
          console.log("id", item.value);
          return item.id === cell ? { ...item, F1: event.target.value } : item
      });
  },

  getCbx(elementId) {
    return this.getElem(elementId).ej2_instances[0];
  },

  getElem(elementId) {
    return document.getElementById(elementId);
  },

  getRowValues() {
    let row = new Map();

    for (var id of comboboxKeys) {
        row.set(id, this.getCbx(id).element.value);
    }

    for (var elemId of elementKeys) {
        if (elemId !== "itemId") { //hidden value has no element
            row.set(elemId, this.getElem(elemId).value);
        }
    }

    console.log({"Row elements": row});
    return row;
  },

  validateInput(row) {
      for (var key of columns) {
          if (isBlank(row.get(key))) {
              alert('No blank field allowed ' + key);
              return false;
          }
      }
      return true;
  },
  
  addItem() {

    let row = this.getRowValues();
 
    let id = this.getCbx("nameCoding").value;
    row.set("itemId", id)

    if (!this.validateInput(row)) {
        return;
    }

    let newItem = new Item(id, row);
    newItem.pushToTable();

    console.log({"Items in table": table})
  },

  getInvoiceAndFill() {
       
    getInvoiceFromServer(
          this.getElem("inputInvoiceNo").value,
          resInvoice => {
            this.fillInvoice(resInvoice);
          });
  },
  
  fillInvoice(invoice) {   

    if (!isBlank(invoice)) {

      this.getCbx("financialyear").value = invoice.financialYear.name;
      this.getCbx("inputvendor").value = invoice.vendor.name;
      this.getCbx("inputAssetType").value = invoice.assetType.name;
      this.getCbx("inputFund").value = invoice.fund;
      this.getElem("inputTotalAmount").value = invoice.totalAmount;
      this.getElem("inputDateOfInvoice").value = invoice.date;
      this.getElem("inputDateOfEntry").value = invoice.entryDate;

      for (var invItem of invoice.items) {
          let values = [
            invItem.item.mainCategory.name,
            invItem.item.subCategory.name,
            invItem.item.name,
            invItem.item.name,
            invItem.item.finalCode,           
            invItem.itemQuantity,
            invItem.item.stock,
            invItem.itemQuantity, //totalItemQuantity
            "",// previousAvailableSerialNoColumn.push({F1 : ''});
            invItem.item.lastSrlNoAssigned,
            invItem.item.lastSrlNoAssigned + 1,
            "", //itemMake
            invItem.item.lastSrlNoAssigned + 1, //itemSerialNo
            "", //basicRate
            "", //discount
            18, //tax
            "", //amount
            "" //stockRegisterPage
          ];

          let args = new Map();
          for (var key in columns) {
              args.set(columns[key], values[key]);
          }

          let item = new Item(invItem.id, args);
          item.pushToTable();
      }
    }
  },

  validateNumber(column) {
    for (var val of column){
      if (isNaN(val.F1)
          || isBlank(val.F1)) {
          alert(val + ' expects number');
          return false;
      }
    }
    return true;
  },

  validateAllColumns() {
      for (var key of columns) {
          let column = table.get(key);
          for (var value of column) {
                console.log("a column value", value.F1)
            if (isBlank(value.F1)) {
              console.log("Blank field", key, value.F1)
              return false;
            }
          }
      }
      return true;
  },

  sendEntry() {
    /*
    if (!this.validateNumber(this.basicRateCol)
        || !this.validateNumber(this.discountCol)
        || !this.validateNumber(this.taxCol)
        || !this.validateNumber(this.amountCol)) {
            return;
    }
    */
    let poNumber = this.getElem('inputPO').value;   
    let purchaseFor = this.getCbx("purchasefor").value;
        
    if (isBlank(purchaseFor)) {
      alert("Puchase for is missing!");
      return;
    }

    if (isBlank(poNumber)) {
      alert("PO number for is missing!");
      return;
    }

    if (!this.validateAllColumns()) {
        alert("A column value is empty!");
        return;
    }

    if (isBlank(this.getElem("inputInvoiceNo").value)) {
        alert("Invoice number missing!");
        return;
    }

    getInvoiceFromServer(
          this.getElem("inputInvoiceNo").value,
          resInvoice => {
            this.sendEntryToServer({
                "invoice": {
                  "id": resInvoice.id,
                },
                "poNumber": poNumber,
                "purchaseFor": {
                  "id": purchaseFor
                },
                "items": sendItems
            });
          });

     // window.location.reload();  
  },

  sendEntryToServer(entry) {          
      const url = 'http://localhost:8080/fixedasset/entry/new';
      const options = {
          method: 'POST',
          body: JSON.stringify(entry),
          headers: {
            'Content-Type': 'application/json'
          }
      }

      fetch(url, options)
          .then(res => res.json())
          .then(res => console.log(res));
      console.log({"Items sent": entry});
      alert("Sent successfully");
  },
},

});       

</script>

<style scoped >

@import url(https://cdn.syncfusion.com/ej2/material.css);
*{
    scroll-behavior: smooth; 
    font-family: sans-serif; 
}

#bodi{
    display: grid;
    margin: 0;
    padding: 0;
    width: 100%;
    grid-gap: 0px;
    box-sizing: border-box;
   overflow-x: auto;
   overflow-y: hidden;
}
#container{
    display: grid;
    width: 100%;
    height: auto;
    justify-items: center;
    align-items: center;
    
}
#entryStage{
    display: grid;
    width: 90%;
    position: relative;
    justify-content: center;
    justify-items: center;

}
.field{
    display: grid;
    width: 100%;
}
.field > * {
  font-size: 80%;
  width: 100%;
}
#fieldset1{
   width: 100%;
   display: grid;
   grid-template-columns: 1fr 1fr 1fr;
}
#fieldset1 .field{
   
   padding: 10px 20px;
}
#fieldsetMiddle{
    margin-top: 20px ;
    display: flex;
    align-items: flex-end;
}
#fieldInputSN°,
#fieldInputPO,
#fieldInputTA,
#fieldPurchasefor {  
  display: inline-block;
  width: 200px;
  padding: 10px 0px; 
}
#fieldInputPO{
    margin-left: 20px; 
}
#fieldPurchasefor{
    margin-left: 20px; 
}
#fieldInputTA{
  margin-top: 20px; 
}
#fieldset2{
  width: 100%;
  display: grid;
  grid-template-columns:  70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px;
  margin-top: 20px;  
}
#fieldset2 label{
  height: 70px;
}
#fieldset2 >>> .e-multi-select-wrapper{
  width: 70px;
}
#fieldset2  >>> .paddedinput {
  padding: 5px;
  margin-top: -2px; 
}

input:focus ,
input:active {
  outline: none; 
}
input{
    margin-top: 10px;
    display:block;
    width:100%;
    border:none;
    border-bottom:1.5px solid #757575;
    background-color: transparent;
    opacity: 0.5;
}
.bar { 
  position:relative; 
  display:block; 
  width:100%; 
}
.bar:before, .bar:after {
  content:'';
  height:2px; 
  width:0;
  top: 0;
  position:absolute;
  background:#5264AE; 
  transition:0.2s ease all; 
  -moz-transition:0.2s ease all; 
  -webkit-transition:0.2s ease all;
}
.bar:before {
  left:50%;
}
.bar:after {
  right:50%; 
}

input:focus ~ .bar:before, input:focus ~ .bar:after {
  width:50%;
}

#tableContainer{
  width:100%;
  height:auto;
  display: grid;
  background-color: antiquewhite;
  grid-template-columns:  70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px ;
 }


.Datatable {
  cursor: pointer;
  transition: color 0.15s ease-in-out;
  font-size: 80%;
  width: 100%;
  word-wrap: break-word;
  white-space: normal !important;
  overflow-x: hidden; 
  table-layout: fixed;
}
.Datatable  >>> td{
  width: 70px;
  border: 1px dashed rgba(255, 0, 0, .2);
}
.Datatable >>> .tbody-tr{
    display: grid;
    grid-template-columns: 60px 10px;
    min-height: 65px;
    max-height: 100px;
    padding-top: 4px;
}

.Datatable >>> input{
  width: 70px !important;
  border: none !important;
  overflow-x: hidden; 
  word-wrap: break-word;
  word-break: break-all;
  white-space: normal !important;
}

textarea {
  resize: none;
  width: 100%;
  height: 50px ;
}

#divConfirm{
display: grid;
width: 200px;
margin: auto;
grid-template-columns: 1fr 1fr;
grid-template-rows: 1fr 1fr;
grid-template-areas: "confirm confirm"
                     "yes no";
}
#divConfirm label{
text-align: center;
 grid-area: confirm;
}
#divConfirm #yes{
 grid-area: yes;
}
#divConfirm #no{
 grid-area: no;
}

</style>
