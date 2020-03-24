<template>
  <div id="bodi" >
    <div id="container">
      <h3 style="margin: 20px">Entry Stage</h3>

      <form id="entryStage" @submit.prevent >  

        <div id="fieldset1">
          <div class='field' v-for="field in invoiceFields" :key="field.id">
            <combobox-field v-if="field.type === 'combobox'"
                :id='field.id' :data='field.data' 
                :fields='field.fields' :text='field.text'>
            </combobox-field>
            <action-field v-else-if="field.id === 'inputInvoiceNo'"
                :id='field.id' :type='field.type' :text='field.text' :action='getInvoiceAndFill'>
            </action-field>
            <input-field v-else
                :id='field.id' :type='field.type' :text='field.text'>
            </input-field>
          </div>         
        </div>

        <line-div></line-div>
        <line-div></line-div>
        <line-div></line-div>

        <div id="fieldsetMiddle">
          <div class='field' v-for="field in entryFields" :key="field.id">
              <combobox-field v-if="field.type === 'combobox'"
                  :id='field.id' :data='field.data' 
                  :fields='field.fields' :text='field.text'>
              </combobox-field>
              <input-field v-else
                  v-bind:id='field.id' v-bind:type='field.type' v-bind:text='field.text'>
              </input-field>
          </div>
        </div>
          
        <form @submit.prevent>
          <div id="fieldset2" >
            <div class='field' v-for="field of tableFields" :key="field.id">
              <combobox-field v-if="field.type === 'combobox'"
                  :id='field.id' :data='field.data' 
                  :fields='field.fields' :text='field.text'>
              </combobox-field>
              <input-field v-else
                  :id='field.id' :type='field.type' :text='field.text' :clas='field.clas'>
              </input-field>
            </div>            
          </div>        
        </form>
          
        <div id="addItem" @click="addItem()" style="cursor: pointer; margin: 15px">Add item</div>


        <div id="tableContainer">

          <DataTable v-for='field of tableFields' :key="field.id"
              class="Datatable" :header-fields="headerFields" 
              :data="field.column || []" not-found-msg="" >   
              <div slot="F1New" slot-scope="props">
                <textarea
                    type="text"
                    :value="props.rowData.F1"
                    @keyup="change($event, props.rowData.ID, field.column);"
                    class="form-control">
                </textarea> 
              </div>
          </Datatable>

        </div>
        
          
        <div id="divConfirm">
          <label>Confirm Entry</label>
          <button id="yes" value="sendEntry" @click="sendEntry()" onkeydown="return (event.keyCode!=13);" >Yes</button>
          <button id="no" value="cancel" onClick="window.location.reload()" onkeydown="return (event.keyCode!=13);">No</button>
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

//=============================Data=================================

var fetchData = function(namePath) {
    return new DataManager({
        url: 'http://localhost:8080/'.concat(namePath, '/all'),
        adaptor: new WebApiAdaptor,
        crossDomain: true
    });
}

//=============================Fields=================================\\
class Field {
    constructor(id, type, text, clas, data, fields) {
        this.id = id;
        this.type = type;
        this.text = text;
        this.clas = clas;
        this.data = data;
        this.fields = fields;
        this.column = [];
    }
}

const simpleField = {value:'id', text:'name'};

const invoiceFields = [
    new Field("financialyear", "combobox", "Financial year", "", fetchData("financialyear"), simpleField),
    new Field("inputDateOfEntry", "date", "Date of entry"),
    new Field("inputvendor", "combobox", "Vendor name", "", fetchData("vendor"), simpleField),
    new Field("inputAssetType", "combobox", "Asset type", "", fetchData("assettype"), simpleField),
    new Field("inputFund", "combobox", "Fund", "", fetchData("invoice"), simpleField),
    new Field("inputInvoiceNo", "number", "Invoice n°"),
    new Field("inputDateOfInvoice", "date", "Date of invoice"),
];

const entryFields = [
    new Field("fieldInputSN", "number", "S.N°"),
    new Field("fieldInputPO", "text", "PO Number/ Requisition below 25000/-"),
    new Field("fieldPurchasefor", "combobox", "Purchase for", "", fetchData("department"), simpleField),
    new Field("inputTotalAmount", "number", "Total Amount")
];

const itemNameField = {value: 'id' ,text:'finalCode'};

const tableFields = [
    new Field("mainCat", "combobox", "Stock Register/ Main Category", "", fetchData("maincategory"), simpleField),
    new Field("subCat", "combobox", "Stock Register/ sub Category", "", fetchData("subcategory"), simpleField),
    new Field("nameInvoice", "text", "Item name as per Invoice", "paddedinput"),
    new Field("nameCoding", "combobox", "Item name for coding", "", fetchData("item"), itemNameField),
    new Field("assetCode", "text", "Asset Code", "paddedinput"),
    new Field("invoiceQty", "number", "Item Quantity (Recd. Via Invoice)", "paddedinput"),
    new Field("prevQty", "number", "Item Quantity (Previous available to Store)", "paddedinput"),
    new Field("totalQty", "number", "Total Item Quantity", "paddedinput"),
    new Field("prevSrlNo", "number", "Previous available Sr.No", "paddedinput"),
    new Field("lastSrlAssigned", "number", "Item Last Sr. No. (As per coding)", "paddedinput"),
    new Field("newNumber", "number", "Item New Number", "paddedinput"),
    new Field("itemMake", "text", "Item Make", "paddedinput"),
    new Field("itemSrlNo", "number", "Item S.N°", "paddedinput"),
    new Field("basicRate", "number", "Basic Rate", "paddedinput"),
    new Field("discount", "number", "Discount", "paddedinput"),
    new Field("tax", "number", "Tax (%)", "paddedinput"),
    new Field("amount", "number", "Amount", "paddedinput"),
    new Field("stockRegPage", "number", "Stock Register Page No.", "paddedinput")
];

var mapTable = function() {
    let map = new Map();
    for (var field of tableFields) {
        map.set(field.id, field.column);
    }
    return map;
};

const tableMap = mapTable();

//=============================Components=================================\\

Vue.component('line-div', {
  template: '\
      <div style="width: 100%; height:10px;  border-bottom: 1px solid; opacity: 0.3"></div>'
});

Vue.component('input-field', {
    props: ['id', 'type', 'text', 'clas'],
    template: "\
        <div class='field'>\
            <label v-bind:for='id'>{{text}}</label>\
            <input v-bind:type='type' v-bind:id='id'\
                v-bind:class='clas' v-bind:name='id'\
                autocomplete='off'\
                onkeydown='return (event.keyCode!=13);'>\
            <span class=\"bar\"></span>\
        </div>"
});

Vue.component('action-field', {
    props: ['id', 'type', 'text', 'clas', 'action'],
    template: "\
        <div class='field'>\
            <label v-bind:for='id'>{{text}}</label>\
            <input v-bind:type='type' v-bind:id='id'\
                :class='clas' v-bind:name='id'\
                autocomplete='off' v-on:keyup.enter='action'\
                onkeydown='return (event.keyCode!=13);'>\
            <span class=\"bar\"></span>\
        </div>"
});

Vue.component('combobox-field', {
    props: ['id', 'data', 'fields', 'text'],
    template: "\
        <div>\
            <label v-bind:for='id'>{{text}}</label>\
            <ejs-combobox v-bind:dataSource='data'\
                mode='Delimiter' v-bind:id='id' allowCustom=\"false\"\
                :hideSelectedItem='false' :allowFiltering='true'\
                v-bind:fields='fields' placeholder=\"Select an item\"\
                popupWidth=\"250px\" popupHeight=\"200px\">\
            </ejs-combobox>\
            <span class='bar'></span>\
        </div>"
});

/*
<div class="field">
  <label for="mainCat">Stock Register/ Main Category</label>
  <ejs-combobox  id="mainCat"  onkeydown="return (event.keyCode!=13);"
      :hideSelectedItem='false'  :allowMultiSelection='true'   v-model="mc"
      :fields='remoteFields' placeholder='select an item' @submit.prevent
      popupWidth="250px" popupHeight="200px">
  </ejs-combobox>
  <p id="StockRegMainCatp" style="display: none; padding: 5px ">{{mc}}</p>
</div>
*/

//===================================================================================

var getInvoiceFromServer = function(invoiceNo, callback) {
    var xhttp = new XMLHttpRequest();
    xhttp.onreadystatechange = function() {
 
      if (this.readyState == 4 && this.status == 200) {
          console.log({"Fetched invoice": JSON.parse(xhttp.responseText)});
          callback(JSON.parse(xhttp.responseText));
      } else if (this.status == 404){
          alert("Invoice n° " + invoiceNo + " not found.")
      }
    };
    xhttp.open("GET", "http://localhost:8080/invoice/findno/".concat(invoiceNo), true);
    xhttp.send();
};


//=================================================================================

var sendItems = [];

var slotIndex = 0;

class Item {
    constructor(itemId, args) {
        this.itemId = itemId; 
        this.args = args;
    }   

    pushToTable() {
        for (var field of tableFields) {
            field.column.push({F1: this.args.get(field.id), ID: slotIndex});
            slotIndex++;
        }

        let item = {
          "item": {
              "id": this.itemId
          },
          "itemNewSerialNumber": this.args.get("newNumber"),
          "basicRate": this.args.get("basicRate"),
          "discount": this.args.get("discount"),
          "tax": this.args.get("tax"),
          "amount": this.args.get("amount")
        }
        sendItems.push(item);
    }
}

//=====================================================0

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
  name: 'formEntry', 
  components: {
    DataTable
  },
  
  data: function() {
    return {

      invoiceFields: invoiceFields,
      entryFields: entryFields,
      tableFields: tableFields,
     
      headerFields: [
        {
          name: "F1",
          label: "",
          customElement: "F1New"
        },
      ],
    
      F1: null,     
  };
},

methods: {

  change: function(event, slotId, column) {
      console.log("Slot ID", slotId);
      column.forEach(item => {
          if (item.ID === slotId) {
              item.F1 = event.target.value;
          }
      });
      console.log("column changed", column);
  },

  getCbx(elementId) {
    return this.getElem(elementId).ej2_instances[0];
  },

  getElem(elementId) {
    return document.getElementById(elementId);
  },

  getRowValues() {
    let row = new Map();

    for (var field of tableFields) {
        if (field.type === 'combobox') {
            row.set(field.id, this.getCbx(field.id).element.value);
        } else {
            if (field.id !== "itemId") { //hidden value has no element
                row.set(field.id, this.getElem(field.id).value);
            }
        }
    }

    console.log({"Row elements": row});
    return row;
  },

  validateInput(row) {
      for (var field of tableFields) {
          if (isBlank(row.get(field.id))) {
              alert('No blank field allowed ' + field.id);
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

    console.log({"Items in table": tableFields[0].column})
  },

  clearColumns() {
      for (var field of tableFields) {
          field.column = [];
      }
      sendItems = [];
  },

  getInvoiceAndFill() {
       
    getInvoiceFromServer(
          this.getElem("inputInvoiceNo").value,
          resInvoice => {
            this.fillInvoice(resInvoice);
          });
  },
  
  fillInvoice(invoice) {   

    if (isBlank(invoice)) {
        return;
    }
    this.clearColumns();

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
        var index = 0;
        for (var field of tableFields) {
            args.set(field.id, values[index]);
            index++;
        }

        let item = new Item(invItem.id, args);
        item.pushToTable();
    }
    
  },

  validateNumber() {
    for (var field of tableFields) {
      if (field.id === 'basicRate'
          || field.id === 'discount'
          || field.id === 'tax'
          || field.id === 'amount') {
            for (var slot of field.column) {
              if (isBlank(slot.F1)) {
                alert(field.id + ' expects number');
                return false;
              }
            }
          }
    }
    return true;
  },

  validateAllColumns() {
      for (var field of tableFields) {
          for (var slot of field.column) {
              if (isBlank(slot.F1)) {
                let msg = "Blank field: ".concat(field.text);
                alert(msg);
                return false;
              }
          }
      }
      return true;
  },

  udapteSendItems() {
    for (var index in sendItems) {
        sendItems[index].basicRate = tableMap.get("basicRate")[index];
        sendItems[index].discount = tableMap.get("discount")[index];
        sendItems[index].tax = tableMap.get("tax")[index];
        sendItems[index].amount = tableMap.get("amount")[index];
        console.log("updated item", sendItems[index]);
    }
    return sendItems;
  },

  sendEntry() {
    
    if (!this.validateNumber()) {
        return;
    }
    
    let poNumber = this.getElem('fieldInputPO').value;   
    let purchaseFor = this.getCbx("fieldPurchasefor").value;
        
    if (isBlank(purchaseFor)) {
      alert("Puchase for is missing!");
      return;
    }

    if (isBlank(poNumber)) {
      alert("PO number for is missing!");
      return;
    }

    if (!this.validateAllColumns()) {
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
                "items": this.udapteSendItems()
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
      console.log({"Entry sent": entry});
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
#fieldInputSN,
#fieldInputPO,
#inputTotalAmount,
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
#inputTotalAmount{
  margin-top: 20px; 
}
#fieldset2{
  width: 100%;
  display: grid;
  grid-template-columns: 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px 70px;
  margin-top: 20px;  
}
#fieldset2 label{
  height: 70px;
}
#fieldset2 >>> .input-field{
  height: 70px;
  width: 70px;
}
#fieldset2 >>> .combobox-field{
  width: 70px;
}
#fieldset2 >>> .paddedinput {
  padding: 5px;
  margin-top: -2px; 
  height: 70px;
  width: 70px;
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
