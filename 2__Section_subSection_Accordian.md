## lightning-accordion

#### A collection of vertically stacked sections with multiple content areas.

### For Use In

#### Lightning Experience, Experience Builder Sites, Salesforce Mobile App, Lightning Out (Beta), Standalone Lightning App, Mobile Offline

```
<div class="slds-box">

        <lightning-accordion active-section-name="B">
            <lightning-accordion-section name="A" label="Array"><lightning-accordion active-section-name="B">
                    <lightning-accordion-section name="A" label="Array Lecture- 1">Array
                        Lec-1</lightning-accordion-section>
                    <lightning-accordion-section name="B" label="Array Lecture- 2">Array
                        Lec-3</lightning-accordion-section>
                    <lightning-accordion-section name="C" label="Array Lecture- 3">Array
                        Lec-3</lightning-accordion-section>
                </lightning-accordion></lightning-accordion-section>
            <lightning-accordion-section name="A" label="String"><lightning-accordion active-section-name="B">
                    <lightning-accordion-section name="A" label="String Lecture-1 Title A">String
                        Lec-1</lightning-accordion-section>
                    <lightning-accordion-section name="B" label="String Lecture-2 Title B">String
                        Lec-3</lightning-accordion-section>
                    <lightning-accordion-section name="C" label="String Lecture-3 Title C">String
                        Lec-3</lightning-accordion-section>
                </lightning-accordion></lightning-accordion-section>
            <lightning-accordion-section name="A" label="Recurssion"><lightning-accordion active-section-name="B">
                    <lightning-accordion-section name="A" label="Recurssion Lect-1">Recurssion
                        Lec-1</lightning-accordion-section>
                    <lightning-accordion-section name="B" label="Recurssion Lect-2">Recurssion
                        Lec-3</lightning-accordion-section>
                    <lightning-accordion-section name="C" label="Recurssion Lect-2">Recurssion
                        Lec-3</lightning-accordion-section>
                </lightning-accordion></lightning-accordion-section>
        </lightning-accordion>
    </div>

```
