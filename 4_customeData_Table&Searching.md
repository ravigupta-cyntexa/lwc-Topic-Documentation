## Custom DataTable HTML

```
<div class="slds-box">

        <div style="display: flex; justify-content:space-between">
            <p>Account List</p>
            <div class="slds-form-element">
                <label class="slds-form-element__label" for="text-input-id-46">
                    <abbr class="slds-required" title="required" aria-hidden="true">* </abbr>Input Label</label>
                <div class="slds-form-element__control">
                    <input id="text-input-id-46" placeholder="Placeholder text…" required="" type="text"
                        class="slds-input inputValue"  oninput={handleSearch}/>
                </div>
            </div>

        </div>

        <table class="slds-table slds-table_cell-buffer slds-table_bordered slds-table_col-bordered"
            aria-label="Account Table">
            <thead>
                <tr class="slds-line-height_reset">
                    <th scope="col">
                        <div class="slds-truncate" title="Account Name">Account Name</div>
                    </th>
                    <th scope="col">
                        <div class="slds-truncate" title="Number Of Employees">Number Of Employees</div>
                    </th>
                    <th scope="col">
                        <div class="slds-truncate" title="Id">Id</div>
                    </th>
                </tr>
            </thead>
            <tbody>
                <template for:each={data} for:item="acc">
                    <tr key={acc.Id} class="slds-hint-parent">
                        <td data-label="Account Name">
                            <div class="slds-truncate">{acc.Name}</div>
                        </td>
                        <td data-label="Number Of Employees">
                            <div class="slds-truncate">{acc.NumberOfEmployees}</div>
                        </td>
                        <td data-label="Id">
                            <div class="slds-truncate">{acc.Id}</div>
                        </td>
                    </tr>
                </template>
            </tbody>
        </table>
    </div>
```

## JS( where we get records from apex class an dapply filter based searching)
#### where we get records from apex class an dapply filter based searching
```
import getRec from '@salesforce/apex/getRecordforDataTable.getRec';
import { LightningElement, wire, track } from 'lwc';
export default class CustomDataTableHTML extends LightningElement {

    allData = [];
    error;
    data = [];

    @wire(getRec)
    wiredRecords(result) {

        if (result.data) {
            this.allData = result.data;
            this.data = result.data;

        } else if (result.error) {
            this.error = result.error;
        }
    }


    
    



    handleSearch(event) {
        let inp = event.target.value.toLowerCase();

        if (inp === '') {
            this.data = [...this.allData];
            return;
        }

        const filtered = this.allData.filter(item =>
            item.Name && item.Name.toLowerCase().includes(inp)
        );

        this.data = [...filtered];
    }
}
```
