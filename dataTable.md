## A table that displays rows and columns of data.

##### For Use In
##### Lightning Experience, Experience Builder Sites, Lightning Out (Beta), Standalone Lightning App

## let suppose let a component named(dataTableComponent)
### this has 3 file 
```
dataTableComponent.html
dataTableComponent.js
dataTableComponent.xml

```

## dataTableComponent.html
```
<template>
    <button class="slds-button slds-button_brand" onclick={deleteHandle}>bulk Delete </button>
    <lightning-card title="Account List" icon-name="standard:contact">
        <lightning-datatable key-field="Id" data={data} columns={columns} show-row-number-column="true"
            onrowaction={handleRowAction} onrowselection={selected}>
        </lightning-datatable>
    </lightning-card>
</template>
```

## dataTableComponent.js
```
import { LightningElement, wire } from 'lwc';
import getRecordforDataTable from '@salesforce/apex/getRecordforDataTable.getRec'
import deleterecordInit from '@salesforce/apex/deleterecord.deleteRec';
import { refreshApex } from '@salesforce/apex';
import { NavigationMixin } from "lightning/navigation";


const actions = [
    { label: 'Show details', name: 'show_details' },

    { label: 'Delete', name: 'delete' },
    { label: 'Edit', name: 'edit' },
];

const columns_P = [
    { label: "Name", type: "text", fieldName: "Name" },
    { label: "Number Of Employee", type: "phone", fieldName: "NumberOfEmployees" },
    {
        type: 'action',
        typeAttributes: { rowActions: actions },
    },
]


export default class DataTableComponent extends NavigationMixin(LightningElement) {


    columns = columns_P;
    // data = [
    //     { Name: "John Doe2", number: "1234567890" },
    //     { name: "Jane Smith", number: "9876543210" },
    //     { name: "Alice Johnson", number: "5555555555" }
    // ]

    wiredData;
    data;
    error;
    flag = false;
    @wire(getRecordforDataTable)
    wiredRecords(result) {
        // if (this.flag === false) {
        //     getRecordforDataTable().then(result => {
        //         console.log(result);
        //         this.data = result;
        //         this.flag = true;
        //     })
        // }
        // console.log("data is", this.data);
        this.wiredData = result;
        console.log(result);
        if (result.data) {
            this.data = result.data;
            console.log(this.data);
            this.error = undefined;
        } else if (result.error) {
            this.error = result.error;
            this.data = undefined;
        }
    }

    tempselected;
    selected(event) {
        console.log("event details is ", event.detail);

        console.log("selected ropws are ", JSON.parse(JSON.stringify(event.detail.selectedRows)));
        this.tempselected = event.detail.selectedRows;


    }


    deleteHandle() {
        try {
            console.log("handle deleyte button working ", this.tempselected)

            this.tempselected.forEach(element => {
                console.log(element.Id);
                deleterecordInit({ 'i': element.Id }).then(() => {
                    return refreshApex(this.wiredData);

                });;

            })
            console.log("deleteed successfully ");
        } catch (error) {
            console.log(error);
        }

    }



 


    handleRowAction(event) {
        console.log("event details is ", event.detail);
        const actionName = event.detail.action.name;
        const serow = event.detail.row;
        console.log("Dataa is ", JSON.parse(JSON.stringify(event.detail.row)));
        switch (actionName) {
            case 'delete':
                console.log("id is", serow.Id)
                console.log('in delete : ', serow.Id);
                // let i=serow.Id;
                deleterecordInit({ 'i': serow.Id }).then(() => {
                    return refreshApex(this.wiredData);

                });
                console.log('Deletion completed ');
                break;
            case 'show_details':
                console.log("Modal Open called ",serow.Id);
                this[NavigationMixin.Navigate]({
                    type: "standard__recordPage",
                    attributes: {
                        recordId: serow.Id,
                        actionName: "view"
                       
                    },
                })
                break;
            case 'edit':
                console.log("Modal Open called ",serow.Id);
                this[NavigationMixin.Navigate]({
                    type: "standard__recordPage",
                    attributes: {
                        recordId: serow.Id,
                        actionName: "edit"
                       
                    },
                })
                break;
            default:
        }
    }
}
```
