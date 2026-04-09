## HTML 
```
<template>
        <input id="text-input-id-47" placeholder="Placeholder text…" required="" type="text" class="slds-input Name" />
        <button class="slds-button slds-button_brand" onclick={handleClick}>Brand Button</button>


</template>
```


## JS to take Data from UI and make JSON and then create

```
import { LightningElement } from 'lwc';
import { createRecord } from 'lightning/uiRecordApi';
import { deleteRecord } from 'lightning/uiRecordApi';

export default class LdsExample extends LightningElement {
    recid='';


    handleClick(){
        let name=this.template.querySelector('.Name').value;
        let data={
            "apiName":"Account",
            "fields":{
                "Name":name
            }
        }
        /// creating record of accout
        createRecord(data).then(r=>{
                console.log(r);
                this.recid=r.id;
                console.log(r.id);
        })

        console.log(JSON.stringify(data));
    }





    handledelete(){
        deleteRecord(' '+ this.recid)
    }
}
```
