<template>
  <div id="bodi" >
    <div id="container">
        <h3 style="margin: 20px">Entry Stage</h3>
        <form id="entryStage" @submit.prevent >
        
            <div id="fieldset1">
                <div id="FSchild1">
                    <div class="field">
                        <label for="inputYear">Financial year</label>
                        <ejs-combobox :dataSource='remoteData1'   mode='Delimiter'  id="financialyear" allowCustom="true"
                        :hideSelectedItem='false'  :allowMultiSelection='true'  :allowFiltering='allowFiltering' 
                        :fields='remoteFields' placeholder='select an item' 
                        popupWidth="250px" popupHeight="200px">
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
                        <ejs-combobox :dataSource='remoteData2'  allowCustomValue='allowCustomValue' id="inputvendor"  mode='Delimiter'  
                        :hideSelectedItem='false'  :allowMultiSelection='true' onkeydown="return (event.keyCode!=13);"
                            :fields='remoteFields' placeholder='select an item'
                            popupWidth="250px" popupHeight="200px">
                        </ejs-combobox>
                        <span class="bar"></span>
                    </div>
                    <div class="field">
                        <label for="inputInvoiceN°">Invoice n°</label>
                        <input  type="number"  id="inputInvoiceN°" name="invoiceN°" onkeydown="return (event.keyCode!=13);" v-on:keyup.enter="autofill()" >
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
                        <ejs-combobox :dataSource='remoteData4'   allowCustomValue='allowCustomValue' id="inputAssetType" mode='Delimiter'  
                        :hideSelectedItem='false'  :allowMultiSelection='true' onkeydown="return (event.keyCode!=13);"
                            :fields='remoteFields' placeholder='select an item'
                            popupWidth="250px" popupHeight="200px">
                        </ejs-combobox>
                    </div>
                    <div class="field">
                        <label for="inputFund">Fund</label>
                        <ejs-combobox :dataSource='remoteData3' allowCustomValue='allowCustomValue' id="inputFund" mode='Delimiter'  
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
                        <ejs-combobox :dataSource='remoteData7' id="purchasefor" mode='Delimiter'  onkeydown="return (event.keyCode!=13);"
                          :allowMultiSelection='true'     v-model="pf"  @submit.prevent 
                            :fields='remoteFields' placeholder='select an item' 
                            popupWidth="250px" popupHeight="200px">
                        </ejs-combobox>
                </div>

            </div>
            <form @submit.prevent>
            <div id="fieldset2" >
                
                
                <div class="field">
                    <label for="inputStockReg/MainCat">Stock Register/ Main Category</label>
                    <ejs-combobox :dataSource='remoteData5' mode='Delimiter' id="StockRegMainCat"  onkeydown="return (event.keyCode!=13);"
                        :hideSelectedItem='false'  :allowMultiSelection='true'   v-model="mc"
                            :fields='remoteFields' placeholder='select an item' @submit.prevent
                            popupWidth="250px" popupHeight="200px">
                        </ejs-combobox>
                        <p  id="StockRegMainCatp" style="display: none; padding: 5px ">{{mc}}</p>
                </div>
                <div class="field">
                    <label for="inputStockReg/SubC">Stock Register/ sub Category</label>
                    <ejs-combobox :dataSource='remoteData6' mode='Delimiter'  id="StockRegSubC" 
                        :hideSelectedItem='false'  :allowMultiSelection='true'  @submit.prevent
                            :fields='remoteFields' placeholder='select an item' v-model="sc" onkeydown="return (event.keyCode!=13);"
                            popupWidth="250px" popupHeight="200px">
                    </ejs-combobox>
                    
                        <p  id="StockRegSubCp" style="display: none; padding: 5px ">{{sc}}</p>
                </div>
                <div class="field">
                    <label for="inputItemNameAsPerInvoice">Item name as per Invoice</label>
                    <input  type="text" class="paddedinput"  id="inputItemNameAsPerInvoice" name="itemNameAsPerInvoice" autocomplete="off"  onkeydown="return (event.keyCode!=13);"> 
                    <span class="bar"></span>
                </div>
                <div class="field">
                    <label for="inputItemNameAsForCoding">Item name for coding</label>
                    <ejs-combobox :dataSource='remoteData8' mode='Delimiter'  id="ItemNameAsForCoding" onkeydown="return (event.keyCode!=13);"
                        :hideSelectedItem='false'  :allowMultiSelection='true'  @submit.prevent
                            :fields='remoteFieldsItemNameCoding' placeholder='select an item'  v-model="ic"
                            popupWidth="250px" popupHeight="200px">
                        </ejs-combobox>
                        
                        <p  id="ItemNameAsForCodingp" style="display: none; padding: 5px ">{{ic}}</p>
                        
                </div>
                <div class="field">
                    <label for="inputAssetCode">Asset Code</label>
                    <input type="text" id="inputAssetCode" class="paddedinput"  name="assetCode" autocomplete="off"  onkeydown="return (event.keyCode!=13);">  
                    <span class="bar"></span>
                </div>
                <div class="field">
                    <label for="inputItemQ(RECD.viaInvoice)">Item Quantity (Recd. Via Invoice)</label>
                    <input type="number" id="inputItemQ(RECD.viaInvoice)" class="paddedinput"  name="itemQ(RECD.viaInvoice)"  autocomplete="off" onkeydown="return (event.keyCode!=13);"> 
                    <span class="bar"></span>
                </div>
                <div class="field">
                    <label for="inputItemQ(Prev.AvailableStore)">Item Quantity (Previous available to Store)</label>
                    <input  type="number" id="inputItemQ(Prev.AvailableStore)" class="paddedinput"  name="itemQ(Prev.AvailableStore)"  autocomplete="off" onkeydown="return (event.keyCode!=13);">
                    <span class="bar"></span>
                </div>
                <div class="field">
                    <label for="inputTotaltemQ">Total Item Quantity</label>
                    <input  type="number"  id="inputTotaltemQ" class="paddedinput"  name="totaltemQ" onkeydown="return (event.keyCode!=13);" >
                    <span class="bar"></span>
                </div>
                <div class="field">
                    <label for="inputPrevAvailableSr.No">Previous available Sr.No</label>
                    <input  type="number"  id="inputPrevAvailableSr.No" class="paddedinput"  name="prevAvailableSr.No" onkeydown="return (event.keyCode!=13);">
                    <span class="bar"></span>
                </div>
                <div class="field">
                    <label for="lastSrlNoAssigned">Item Last Sr. No. (As per coding)</label>
                    <input  type="number"  id="lastSrlNoAssigned" class="paddedinput"  name="itemItemLastSr.N°" onkeydown="return (event.keyCode!=13);">
                    <span class="bar"></span>
                </div>
                <div class="field">
                    <label for="inputItemNewNumber">Item New Number</label>
                    <input  type="number"  id="inputItemNewNumber" class="paddedinput"  name="itemNewNumber" onkeydown="return (event.keyCode!=13);">
                    <span class="bar"></span>
                </div>

                <div class="field">
                    <label for="inputItemMake">Item Make</label>
                    <input  type="text"  id="inputItemMake" class="paddedinput"  name="itemMake" autocomplete="off" onkeydown="return (event.keyCode!=13);">
                    <span class="bar"></span>
                </div>
                <div class="field">
                    <label for="inputItemS.N°">Item S.N°</label>
                    <input type="number" id="inputItemS.N°" class="paddedinput"   name="itemS.N°" autocomplete="off" onkeydown="return (event.keyCode!=13);">  
                    <span class="bar"></span>
                </div>
                <div class="field">
                    <label for="inputBasicRate">Basic Rate</label>
                    <input type="number" id="inputBasicRate" class="paddedinput"   name="basicRate"  autocomplete="off" onkeydown="return (event.keyCode!=13);"> 
                    <span class="bar"></span>
                </div>
                <div class="field">
                    <label for="inputDiscount(%)">Discount (%)</label>
                    <input  type="number" id="inputDiscount(%)" class="paddedinput"  name="discount(%)"  autocomplete="off" onkeydown="return (event.keyCode!=13);">
                    <span class="bar"></span>
                </div>
                <div class="field">
                    <label for="inputTax(%)">Tax (%)</label>
                    <input  type="number"  id="inputTax(%)" class="paddedinput"  name="tax(%)" onkeydown="return (event.keyCode!=13);">
                    <span class="bar"></span>
                </div>
                <div class="field">
                    <label for="inputAmount">Amount</label>
                    <input  type="number"  id="inputAmount" class="paddedinput"  name="amount" onkeydown="return (event.keyCode!=13);">
                    <span class="bar"></span>
                </div>
               
                <div class="field">
                    <label for="inputStockRegPageN°">Stock Register Page No.</label>
                    <input  type="number"  id="inputStockRegPageN°" class="paddedinput"  name="stockRegPageN°" onkeydown="return (event.keyCode!=13);">
                    <span class="bar"></span>
                </div>
        </div>
        </form>
            <div id="addItem" @click="addItem()" style="cursor: pointer; margin: 15px">Add item</div>
        <div id="tableContainer">
                
                <DataTable class="Datatable" :header-fields="headerFields" :data="data2 || []" not-found-msg="" >   
                  <div slot="F1New" slot-scope="props">
                                      <textarea
                                        type="text"
                                        :value="props.rowData.F1"
                                        @keyup="changeF1a($event, props.rowData.id);"
                                        class="form-control"
                                      ></textarea>
                                    </div>
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="data3 || []" not-found-msg=" " >  
                      <div slot="F1New" slot-scope="props">
                    <textarea id= "textarea1"
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="changeF1b($event, props.rowData.id);"
                      class="form-control"
                    ></textarea>
                  </div>        
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="data4 || []" not-found-msg=" " > 
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="changeF1c($event, props.rowData.id);"
                      class="form-control"
                    ></textarea>
                  </div>             
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="data5 || [] " not-found-msg=""  > 
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="changeF1d($event, props.rowData.id);"
                      class="form-control"
                    ></textarea>
                  </div>          
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="data6 || []" not-found-msg=""  >   
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="changeF1e($event, props.rowData.id);"
                      class="form-control"
                    ></textarea>
                  </div>        
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="data7 || []" not-found-msg=""  > 
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="changeF1f($event, props.rowData.id);"
                      class="form-control"
                    ></textarea>
                  </div>        
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="data8 || []" not-found-msg=""  >   
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="changeF1g($event, props.rowData.id);"
                      class="form-control"
                    ></textarea>
                  </div>      
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="data9 || []" not-found-msg=""  > 
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="changeF1h($event, props.rowData.id);"
                      class="form-control"
                    ></textarea>
                  </div>      
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="data10 || []" not-found-msg=""  > 
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="changeF1i($event, props.rowData.id);"
                      class="form-control"
                    ></textarea>
                  </div> 
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="data11 || []" not-found-msg="">
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="changeF1j($event, props.rowData.id);"
                      class="form-control"
                    ></textarea>
                  </div>
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="data12 || []" not-found-msg="" >
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="changeF1k($event, props.rowData.id);"
                      class="form-control"
                    ></textarea>
                  </div>
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="data13 || []" not-found-msg="" > 
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="changeF1l($event, props.rowData.id);"
                      class="form-control"
                    ></textarea>
                  </div>
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="data14 || []" not-found-msg="" > 
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="changeF1m($event, props.rowData.id);"
                      class="form-control"
                    ></textarea>
                  </div>
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="data15 || []" not-found-msg=""  > 
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="changeF1n($event, props.rowData.id);"
                      class="form-control"
                    ></textarea>
                  </div> 
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="data16 || []" not-found-msg="">
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="changeF1o($event, props.rowData.id);"
                      class="form-control"
                    ></textarea>
                  </div>
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="data17 || []" not-found-msg="" >
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="changeF1p($event, props.rowData.id);"
                      class="form-control"
                    ></textarea>
                  </div>
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="data18 || []" not-found-msg="" > 
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="changeF1q($event, props.rowData.id);"
                      class="form-control"
                    ></textarea>
                  </div>
                </Datatable>
                <DataTable class="Datatable" :header-fields="headerFields" :data="data19 || []" not-found-msg="" > 
                  <div slot="F1New" slot-scope="props">
                    <textarea
                      type="text"
                      :value="props.rowData.F1"
                      @keyup="changeF1r($event, props.rowData.id);"
                      class="form-control"
                    ></textarea>
                  </div>
                </Datatable>
                
        </div>
                
    
         <div class="field" id="fieldInputTA">
                <label for="inputTotalAmount">Total Amount</label>
                <input  type="number"  id="inputTotalAmount" name="totalamount" onkeydown="return (event.keyCode!=13);">
                <span class="bar"></span>
        </div>
          
         <div id="divConfirm">
                <label>Confirm Entry</label>
                <button id="yes"  value="sendEntry" @click="sendJSON()" onkeydown="return (event.keyCode!=13);" >Yes</button>
                <button id="no"  value="cancel" onClick="window.location.reload()" onkeydown="return (event.keyCode!=13);">No</button>
        </div>
          
        </form>
    </div>
  </div>

</template>

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



var initData1 = [];var initData2 = [];var initData3 = [];var initData4 = [];var initData5 = [];var initData6 = [];
var initData7 = [];var initData8 = [];var initData9 = [];var initData10 = [];var initData11 = [];var initData12 = [];
var initData13 = [];var initData14 = [];var initData15 = [];var initData16 = [];var initData17 = [];var initData18 = [];
var initData19 = []; 

var remoteDataSource1 = new DataManager({
  url: 'http://zumaran.tech/store-app/financialyear/all',
  adaptor: new WebApiAdaptor,
  crossDomain: true
});
var remoteDataSource2= new DataManager({
  url: 'http://zumaran.tech/store-app/vendor/all',
  adaptor: new WebApiAdaptor,
  crossDomain: true
});
var remoteDataSource3 = new DataManager({
  url: 'http://zumaran.tech/store-app/invoice/all',
  adaptor: new WebApiAdaptor,
  crossDomain: true
});
var remoteDataSource4 = new DataManager({
  url: 'http://zumaran.tech/store-app/assettype/all',
  adaptor: new WebApiAdaptor,
  crossDomain: true
});
var remoteDataSource5 = new DataManager({
  url: 'http://zumaran.tech/store-app/maincategory/all',
  adaptor: new WebApiAdaptor,
  crossDomain: true
});
var remoteDataSource6 = new DataManager({
  url: 'http://zumaran.tech/store-app/subcategory/all',
  adaptor: new WebApiAdaptor,
  crossDomain: true
});
var remoteDataSource7 = new DataManager({
  url: 'http://zumaran.tech/store-app/department/all',
  adaptor: new WebApiAdaptor,
  crossDomain: true
});
var remoteDataSource8 = new DataManager({
  url: 'http://zumaran.tech/store-app/items/all',
  adaptor: new WebApiAdaptor,
  crossDomain: true
});
var remoteDataSource9 = new DataManager({
  url: 'http://zumaran.tech/store-app/invoice/findno/2001',
  adaptor: new WebApiAdaptor,
  crossDomain: true
});


window.onload=function(){

 
    
    
}

    

      var rds;
                var xhttp = new XMLHttpRequest();
                xhttp.onreadystatechange = function() {
                    if (this.readyState == 4 && this.status == 200) {
                    rds = JSON.parse(xhttp.responseText);
                    
                    }
                };
                xhttp.open("GET", "http://zumaran.tech/store-app/invoice/findno/2001", true);
                xhttp.send();

     




export default Vue.extend({
  name: 'form1', 
  components: {
    DataTable
  },
  data: function() {
    return {
    
      remoteData1: remoteDataSource1,
      remoteData2: remoteDataSource2,
      remoteData3: remoteDataSource3,
      remoteData4: remoteDataSource4,
      remoteData5: remoteDataSource5,
      remoteData6: remoteDataSource6,
      remoteData7: remoteDataSource7,
      remoteData8: remoteDataSource8,
      remoteData9: remoteDataSource9,

      remoteFields: {value: 'id' ,text:'name'},
      remoteFieldsInvoiceN: {value: 'id' ,text:'number'  },
      remoteFieldsInvoiceDateEntry: {value: 'id' ,text:'entryDate' },
      remoteFieldsInvoiceDate: {value: 'id' ,text:'date' },
      remoteFieldsInvoiceFinancialYear: {value: 'financialYear.id' ,text:'financialYear.name' },
      remoteFieldsInvoiceVendor: {value: 'vendor.id' ,text:'vendor.name' },
      remoteFieldsInvoiceAssetType: {value: 'assetType.id' ,text:'assetType.name' },
      remoteFieldsInvoiceFund: {value: 'id' ,text:'fund'  },
      remoteFieldsInvoiceTotalAmount: {value: 'id' ,text:'totalAmount'},
      remoteFieldsItemNameCoding: {value: 'id' ,text:'itemCode'},

       keySettings: {
                        saveRequest: "",
         },
    
      
      localData:[
        { Id: '1', item: 'a'},
        { Id: '2', item: 'b'},
        { Id: '3', item: 'c'}
      ],
      localFields:{value: 'Id', text: 'item'},

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

      data1: initData1,  data2: initData2,  data3: initData3,  data4: initData4,  data5: initData5,  data6: initData6,
      data7: initData7,  data8: initData8,  data9: initData9,  data10: initData10,  data11: initData11,  data12: initData12,
      data13: initData13,  data14: initData14,  data15: initData15,  data16: initData16,  data17: initData17,  data18: initData18,
      data19: initData19,
    allowFiltering: true,
    customValue: '',
    newItem: '',
    query: '',
    F1: null,     
     

    };
    },
   
    methods: {
         
          changeF1a: function(event, id) {
          this.data = this.data2.map(item =>
            item.id === id ? { ...item, F1: event.target.value } : item
          );
        },
          changeF1b: function(event, id) {
          this.data = this.data3.map(item =>
            item.id === id ? { ...item, F1: event.target.value } : item
          );
        },
          changeF1c: function(event, id) {
          this.data= this.data4.map(item =>
            item.id === id ? { ...item, F1: event.target.value } : item
          );
        },
          changeF1d: function(event, id) {
          this.data = this.data5.map(item =>
            item.id === id ? { ...item, F1: event.target.value } : item
          );
        },
          changeF1e: function(event, id) {
          this.data = this.data6.map(item =>
            item.id === id ? { ...item, F1: event.target.value } : item
          );
        },
          changeF1f: function(event, id) {
          this.data = this.data7.map(item =>
            item.id === id ? { ...item, F1: event.target.value } : item
          );
        },
          changeF1g: function(event, id) {
          this.data = this.data8.map(item =>
            item.id === id ? { ...item, F1: event.target.value } : item
          );
        },
          changeF1h: function(event, id) {
          this.data = this.data9.map(item =>
            item.id === id ? { ...item, F1: event.target.value } : item
          );
        },
          changeF1i: function(event, id) {
          this.data = this.data10.map(item =>
            item.id === id ? { ...item, F1: event.target.value } : item
          );
        },
          changeF1j: function(event, id) {
          this.data = this.data11.map(item =>
            item.id === id ? { ...item, F1: event.target.value } : item
          );
        },
          changeF1k: function(event, id) {
          this.data = this.data12.map(item =>
            item.id === id ? { ...item, F1: event.target.value } : item
          );
        },
          changeF1l: function(event, id) {
          this.data = this.data13.map(item =>
            item.id === id ? { ...item, F1: event.target.value } : item
          );
        },
          changeF1m: function(event, id) {
          this.data = this.data14.map(item =>
            item.id === id ? { ...item, F1: event.target.value } : item
          );
        },
          changeF1n: function(event, id) {
          this.data = this.data15.map(item =>
            item.id === id ? { ...item, F1: event.target.value } : item
          );
        },
          changeF1o: function(event, id) {
          this.data = this.data16.map(item =>
            item.id === id ? { ...item, F1: event.target.value } : item
          );
        },
          changeF1p: function(event, id) {
          this.data = this.data17.map(item =>
            item.id === id ? { ...item, F1: event.target.value } : item
          );
        },
          changeF1q: function(event, id) {
          this.data = this.data18.map(item =>
            item.id === id ? { ...item, F1: event.target.value } : item
          );
        },
          changeF1r: function(event, id) {
          this.data = this.data19.map(item =>
            item.id === id ? { ...item, F1: event.target.value } : item
          );
        },
          sendJSON(){
            for (var i = 0; i < initData15.length; i++){
                if (isNaN(initData15[i].F1) == true){
                    alert(' Basic Rate expects number ')
                }
             }
             for (var iN = 0; iN < initData16.length; iN++){
                if (isNaN(initData16[iN].F1) == true){
                    alert(' Basic Rate expects number ')
                }
             }

            let getpoNumber = document.getElementById('inputPO').value;
            let items = [];
            let itemID = 0;
            let item  = {
                    "item" : {
                        "id":1
                    },
                    "itemQuantity":initData7[itemID].F1,
                    "itemNewSerialNumber":initData12[itemID].F1,
                    "basicRate":initData15[itemID].F1,
                    "discount":initData16[itemID].F1,
                    "tax": initData17[itemID].F1,
                    "amount":initData18[itemID].F1,
            }
            for ( var ix = 1; ix <= initData2.length; ix++) {
            items.push(item);
            itemID + 1;
            }
            var pfvalue1id = document.getElementById("purchasefor").ej2_instances[0].value;

            var sendItem = {
                    "invoice":
                        {
                            "id": rds.id,
                        },
                    "poNumber": getpoNumber,
                    "purchaseFor":
                    {
                        "id": pfvalue1id
                        },
                    "items":    items
                                   

          }


            
            const url = 'http://zumaran.tech/store-app/fixedasset/entry/new';
            const options = {
                method: 'POST',
                body: JSON.stringify(sendItem),
                headers: {
                    'Content-Type': 'application/json'
                }
            }
            

            if (pfvalue1id == null){
              alert("A field is missing")
            }
            
            else{
              fetch(url, options)
                .then(res => res.json())
                .then(res => console.log(res));
             console.log("Items sent:" + initData1.length, sendItem);
              alert("Sent successfully");
              window.location.reload();

            }
            

                   
    
                

          },
          addItem(){
                var inputvalue2 = document.getElementById("StockRegMainCat").ej2_instances[0].element.value;
                
                var inputvalue3 = document.getElementById("StockRegSubC").ej2_instances[0].element.value;
                
                var inputvalue4 = document.getElementById("inputItemNameAsPerInvoice").value;
               
                var inputvalue5 = document.getElementById("ItemNameAsForCoding").ej2_instances[0].element.value;
               
                var inputvalue6 = document.getElementById("inputAssetCode").value;
               
                var inputvalue7 = document.getElementById("inputItemQ(RECD.viaInvoice)").value;
                
                var inputvalue8 = document.getElementById("inputItemQ(Prev.AvailableStore)").value;
               
                var inputvalue9 = document.getElementById("inputTotaltemQ").value;
                
                var inputvalue10 = document.getElementById("inputPrevAvailableSr.No").value;
                
                var inputvalue11 = document.getElementById("lastSrlNoAssigned").value;
             
                var inputvalue12 = document.getElementById("inputItemNewNumber").value;
         
                var inputvalue13 = document.getElementById("inputItemMake").value;
     
                var inputvalue14 = document.getElementById("inputItemS.N°").value;
       
                var inputvalue15 = document.getElementById("inputBasicRate").value;
                
                var inputvalue16 = document.getElementById("inputDiscount(%)").value;
         
                var inputvalue17 = document.getElementById("inputTax(%)").value;
     
                var inputvalue18 = document.getElementById("inputAmount").value;
       
                var inputvalue19 = document.getElementById("inputStockRegPageN°").value;

               
                if(inputvalue2 == null && inputvalue3 == null && inputvalue4 == null && inputvalue5 == null && 
                inputvalue6 == null && inputvalue7 == null && inputvalue8 == null && inputvalue9 == null && 
                inputvalue10 == null && inputvalue11 == null && inputvalue12 == null && inputvalue13 == null && 
                inputvalue14 == null && inputvalue15 == null && inputvalue16 == null && inputvalue17 == null && 
                inputvalue18 == null && inputvalue19 == null ){
                     alert('No blank item allowed');
                }
                
                else {
   
                initData2.push({F1 : inputvalue2});
              
                initData3.push({F1 : inputvalue3});
          
                initData4.push({F1 : inputvalue4});
               
                initData5.push({F1 : inputvalue5});
               
                initData6.push({F1 : inputvalue6});
  
                initData7.push({F1 : inputvalue7});       
                
                initData8.push({F1 : inputvalue8});
               
                initData9.push({F1 : inputvalue9});
                
                initData10.push({F1 : inputvalue10});
            
                initData11.push({F1 : inputvalue11});
              
                initData12.push({F1 : inputvalue12});

                initData13.push({F1 : inputvalue13});
     
                initData14.push({F1 : inputvalue14});
            
                initData15.push({F1 : inputvalue15});

                initData16.push({F1 : inputvalue16});
            
                initData17.push({F1 : inputvalue17});
            
                initData18.push({F1 : inputvalue18});
    
                initData19.push({F1 : inputvalue19});

                }
                },
         autofill(){
                
                var invoiceN = document.getElementById("inputInvoiceN°"); 
                var fyear = document.getElementById("financialyear");
                var vendor = document.getElementById("inputvendor");
                var assettype = document.getElementById("inputAssetType");
                var fund = document.getElementById("inputFund");
                var totalamount = document.getElementById("inputTotalAmount");
                var dateOfInvoice = document.getElementById("inputDateOfInvoice");

                /*var maincat = document.getElementById("StockRegMainCat");
                var subcat = document.getElementById("StockRegSubC");
                var itemname = document.getElementById("inputItemNameAsPerInvoice");
                var itemcode = document.getElementById("ItemNameAsForCoding");
                var lastSrlNoAssigned = document.getElementById("lastSrlNoAssigned");
                var stock = document.getElementById("inputItemQ(Prev.AvailableStore)");
                var itemNewNumber = document.getElementById("inputItemNewNumber");
                */
                
                var obj = rds.items;
                
    
                if (invoiceN.value == 2001){
                    fyear.ej2_instances[0].element.value = rds.financialYear.name;
                    vendor.ej2_instances[0].element.value =rds.vendor.name ;
                    assettype.ej2_instances[0].element.value = rds.assetType.name;
                    fund.ej2_instances[0].element.value = rds.fund;
                    totalamount.value = rds.totalAmount;
                    dateOfInvoice.value = rds.date;
                    

                    for (var i = 0; i < obj.length; i++)
                {       
                        initData2.push({F1 : obj[i].item.mainCategory.name});
                        initData3.push({F1 : obj[i].item.subCategory.name});
                        initData4.push({F1 : obj[i].item.name});
                        initData5.push({F1 : obj[i].item.itemCode});
                        initData6.push({F1 : obj[i].item.finalCode});
                        initData7.push({F1 : ''});
                        initData8.push({F1 : obj[i].item.stock});
                        initData9.push({F1 : ''});
                        initData10.push({F1 : ''});
                        initData11.push({F1 : obj[i].item.lastSrlNoAssigned});
                        initData12.push({F1 : obj[i].item.lastSrlNoAssigned + i + 1});
                        initData13.push({F1 : ''});
                        initData14.push({F1 : ''});
                        initData15.push({F1 : ''});
                        initData16.push({F1 : ''});
                        initData17.push({F1 : ''});
                        initData18.push({F1 : ''});
                        initData19.push({F1 : ''});
         
                }
                
                    }
                }  
                
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
 #fieldPurchasefor
 
 {  display: inline-block;
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
.bar 	{ position:relative; display:block; width:100%; }
.bar:before, .bar:after 	{
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
