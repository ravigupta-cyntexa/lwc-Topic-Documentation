## lightning-combobox

### A widget that provides an input field that is readonly, accompanied by a dropdown list of selectable options.
## html code 
```
 <lightning-combobox name="progress" label="Status" value={value} placeholder="Select Progress" options={options}
        onchange={handleChange} required></lightning-combobox>
    <p>Selected value is: {value}</p>

```

## JS Code

```
value = 'inProgress';

    get options() {
        return [
            { label: 'New', value: 'new' },
            { label: 'In Progress', value: 'inProgress' },
            { label: 'Finished', value: 'finished' },
        ];
    }

    handleChange(event) {
        this.value = event.detail.value;
    }
```
