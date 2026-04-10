## HTML

```
 <template if:true={isModalOpen}>
        <section role="dialog" class="slds-modal slds-fade-in-open">
            <div class="slds-modal__container">
                <header class="slds-modal__header">
                    <button class="slds-button slds-button_icon slds-modal__close" onclick={closeModal}>
                        <lightning-icon icon-name="utility:close"></lightning-icon>
                    </button>
                    <h2 class="slds-text-heading_medium">Modal Title</h2>
                </header>
                <div class="slds-modal__content slds-p-around_medium">
                    <p>View this site by logging in to your Salesforce org and navigating to
                        https://MyDomainName.my.salesforce.com/docs/component-library.
                        The authenticated site has additional features for the Component Reference.
                        View Aura Lightning components that are unique to your org.
                        View Aura Lightning components that are installed in a managed package. You can filter to view
                        components owned by your org or installed in packages. Find the filtering options at
                        https://MyDomainName.my.salesforce.com/docs/component-library/overview/components and expand the
                        Filters list to find the Owners filters.</p>
                </div>
                <footer class="slds-modal__footer">
                    <lightning-button label="Cancel" onclick={closeModal}></lightning-button>
                    <lightning-button label="Save" variant="brand" onclick={closeModal}></lightning-button>
                </footer>
            </div>
        </section>
        <div class="slds-backdrop slds-backdrop_open"></div>
    </template>
```

## JS

```
import { LightningElement, wire, track } from 'lwc';

@track isModalOpen = false;

    openModal() {
        this.isModalOpen = true;
    }
    closeModal() {
        this.isModalOpen = false;
    }
```
