## html
```
<template>
    <!-- lightning record create form  -->
    <lightning-record-form object-api-name={objectApiName} fields={fields} onsuccess={handleSuccess}>
    </lightning-record-form>


    <!-- ///read only  -->
    <lightning-record-form record-id={recordId} object-api-name={objectApiName}  columns="2" layout-type="Full" mode="readonly">
    </lightning-record-form>

<!-- /// edit  -->
    <lightning-record-form record-id={recordId} object-api-name={objectApiName} onsuccess={handleSuccess} columns="2" layout-type="Full" mode="edit">
    </lightning-record-form>

    <!-- // view -->

     <lightning-record-form record-id={recordId} object-api-name={objectApiName}  columns="2" layout-type="Full" mode="view">
    </lightning-record-form>

    <!-- /// record edit form  -->
    <!-- <lightning-record-edit-form object-api-name={objectApiName} record-id={recordId}>
        <lightning-input-field field-name={nameField}> </lightning-input-field>
        <lightning-input-field field-name={NOEField}> </lightning-input-field>

        <div class="slds-var-m-top_medium">
            <lightning-button variant="brand"  type="submit" label="Save">
            </lightning-button>
        </div>
    </lightning-record-edit-form> -->

    <!-- record view only form  -->
    <!-- <lightning-record-view-form object-api-name={objectApiName} record-id={recordId}>
        <lightning-output-field field-name={nameField}> </lightning-output-field>
        <lightning-input-field field-name={NOEField}> </lightning-input-field>

    </lightning-record-view-form> -->



</template>
```

## Javascript
important -> @api, @objectApiName is used to get the objectName and recordId on opening any record in Object 
```
import { LightningElement, api } from "lwc";
import { ShowToastEvent } from "lightning/platformShowToastEvent";

import NAME_FIELD from "@salesforce/schema/Account.Name";
import NOE_FIELD from "@salesforce/schema/Account.NumberOfEmployees";
import REVENUE_FIELD from "@salesforce/schema/Account.AnnualRevenue";
import INDUSTRY_FIELD from "@salesforce/schema/Account.Industry";
export default class RecordFormExample extends LightningElement {
  // Expose a field to make it available in the template
  fields = [NAME_FIELD, NOE_FIELD,  REVENUE_FIELD, INDUSTRY_FIELD];
  
  // Flexipage provides recordId and objectApiName
  @api recordId;
  @api objectApiName;


  /// for record edit form 

  nameField=NAME_FIELD;
  NOEField=NOE_FIELD;

  // on creation
  handleSuccess(event) {
    const evt = new ShowToastEvent({
      title: "Account created",
      message: "Record ID: " + event.detail.id,
      variant: "success",
    });
    this.dispatchEvent(evt);
  }
}
```
