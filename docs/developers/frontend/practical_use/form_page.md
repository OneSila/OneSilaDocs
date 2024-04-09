
# Form Pages

## Introduction

Form pages in Vue.js applications are central to data entry and management. This documentation provides a deep dive into creating and managing forms, focusing on a constructor logic for streamlined configuration.

## Base Form Configuration Constructor

A `baseFormConfigConstructor` function is used to build form configurations for both creation and editing. This approach allows for shared configurations while permitting specific customizations where necessary.

You can find more about where we should create it, in the config.ts file of each app [here](./index.md).

### Constructor Logic Explained

Here's an example of `baseFormConfigConstructor` function, breaking down its components:

```typescript
export const baseFormConfigConstructor = (
  t: Function,
  type: FormType,
  mutation: any,
  mutationKey: string,
  companyId: string | null = null
): FormConfig => ({
  cols: 1,
  type: type,
  mutation: mutation,
  mutationKey: mutationKey,
  submitUrl: { name: 'contacts.people.list' },
  deleteMutation: deletePersonMutation,
  fields: [
    {
      type: FieldType.Text,
      name: 'firstName',
      label: t('shared.labels.firstName'),
      placeholder: t('shared.placeholders.firstName')
    },
    {
      type: FieldType.Text,
      name: 'lastName',
      label: t('shared.labels.lastName'),
      placeholder: t('shared.placeholders.lastName')
    },
    {
      type: FieldType.Email,
      name: 'email',
      label: t('shared.labels.email'),
      placeholder: t('shared.placeholders.email'),
      optional: true
    },
    {
      type: FieldType.Phone,
      name: 'phone',
      label: t('shared.labels.phone'),
      optional: true
    },
    {
      type: FieldType.Query,
      name: 'language',
      label: t('shared.placeholders.language'),
      labelBy: 'name',
      valueBy: 'code',
      query: customerLanguagesQuery,
      dataKey: 'customerLanguages',
      isEdge: false,
      multiple: false,
      filterable: true,
    },
    getCompanyField(companyId, t)
  ],
});
```

***IMPORTANT NOTE:*** The order of the fields in the frontend is given by the order we give in this config.

You can find more about the form component [here](./../shared_utilities/components/organisms/general-form/index.md) and about the used fields [here](./../shared_utilities/components/organisms/general-form/form_fields.md).

### Using the Constructor for Create Form

For creating a new entity (e.g., person), the `baseFormConfigConstructor` is invoked with specific parameters:

```typescript
import { baseFormConfigConstructor } from "../configs";

onst formConfig = {
  ...baseFormConfigConstructor(
    t,
    FormType.CREATE,
    createPersonMutation,
    'createPerson'
  ),
  submitAndContinueUrl: { name: 'contacts.people.edit' }
};
```

In this case the submitAndContinueUrl we can add as the edit page but this needs an ID. But because is a create page it will automatically be added from the create mutation.

### Using the Constructor for Edit Form

Similarly, for editing an existing entity, the function is called with the `FormType.EDIT` and relevant mutation:

```typescript
import { baseFormConfigConstructor } from "../configs";

const baseForm = baseFormConfigConstructor(
  t,
  FormType.EDIT,
  updatePersonMutation,
  'updatePerson'
);

const formConfig = {
  ...baseForm,
  mutationId: id.value.toString(),
  query: getPersonQuery,
  queryVariables: { id: id.value },
  queryDataKey: 'person',
  fields: [
    {
      type: FieldType.Hidden,
      name: 'id',
      value: id.value.toString()
    },
    ...baseForm.fields
  ]
};
```

The approach is a little different. We crete the baseForm and hen we add some extra fields like the mutationId, the query to get the data, variables for that query, and we also add an extra field that is the id (needed in the mutation).

## Dynamic Field Logic

Forms can dynamically display fields based on certain conditions or user input. For example, a company field can be shown or hidden based on whether the company ID is available.

### Conditional Field Display Example

```typescript
const getCompanyField = (companyId, t): FormField => {
  if (companyId) {
    return {
      type: FieldType.Hidden,
      name: 'company',
      value: { "id": companyId }
    };
  } else {
    return {
      type: FieldType.Query,
      name: 'company',
      label: t('contacts.people.labels.company'),
      labelBy: 'name',
      valueBy: 'id',
      query: companiesQuery,
      dataKey: 'companies',
      isEdge: true,
      multiple: false,
      filterable: true,
      createOnFlyConfig: companyOnTheFlyConfig(t),
    };
  }
}
```

Basically if in the constructor we give a company id (which we will take from the url query params) then we hide the selector of the companies because we already have it.

## On-the-Fly Configuration

In situations where related entities need to be created within the form, On-the-Fly configurations are used.

### Company Creation On-the-Fly Example

```typescript
import { baseFormConfigConstructor as baseCompanyConfigConstructor } from '../companies/configs'

const companyOnTheFlyConfig = (t: Function): CreateOnTheFly => ({
  config: baseCompanyConfigConstructor(
    t,
    FormType.CREATE,
    createCompanyMutation,
    'createCompany'
  )
});
```

This setup allows users to create a company directly from the person form, streamlining the data entry process by using the company form constructor but to build a onTheFly element in the query field. 

## Advanced usage

This section demonstrates a practical example of dynamically updating form fields using our Vue.js application's advanced features. This real-world example shows how to use updateFieldConfigs in conjunction with a form update event to dynamically change field properties based on user interactions.

### Scenario: Updating Address Fields Based on Customer Selection
In this example, we'll focus on a form used for managing customer information. Specifically, we'll look at how the form dynamically updates the 'invoiceAddress' and 'shippingAddress' fields when a different customer is selected.

### Usage example:

```vue
<GeneralForm v-if="formConfig" :config="formConfig as FormConfig" :fields-to-clear="fieldsToClear" @form-updated="handleFormUpdate" />
```

In our form declaration we add handler for the form-updated that occurs when anything is changed inside the form. Also we add fieldToClear where in the parent component we have a listener that will clear that fields if we update that.

```typescript
const handleFormUpdate = (form) => {
  fieldsToClear.value = []

  const newCustomerId = typeof form.customer === 'object' && form.customer !== null? form.customer.id : form.customer;
  if (newCustomerId !== customerId.value) {
    const initialCustomerId = customerId.value;
    customerId.value = newCustomerId;

    const fieldConfigs: FieldConfigs = {
      'invoiceAddress': {
        enabled: {
          disabled: false,
          queryVariables: { "filter": { "company": {"id": {"exact": customerId.value }}}},
          createOnFlyConfig: invoiceAddressOnTheFlyConfig(t, customerId.value)
        },
        disabled: {
          disabled: true,
          queryVariables: null,
          createOnFlyConfig: null
        }
      },
    };

    updateFieldConfigs(customerId, fieldConfigs, formConfig);

    if (initialCustomerId === null) {
      return;
    }
    fieldsToClear.value = ['invoiceAddress']
  }
};
```

#### Step-by-Step Walkthrough
1. Customer Selection Change: The user selects a different customer from a dropdown in the form.
2. Triggering Form Update: This selection change triggers the handleFormUpdate method, which is set to listen for any updates in the form.
3. Dynamic Field Update: Inside handleFormUpdate, updateFieldConfigs is called with the new customer ID, the specific field configurations for 'invoiceAddress' and 'shippingAddress', and the current form configuration.
   - If a new customer is selected (i.e., customerId changes), the 'enabled' configuration is applied. 
   - If no customer is selected, the 'disabled' configuration is applied.
   
So the `updateFieldConfigs` is a magic method that will check the value of the target (in our case customerId if this was provided or not). And are 2 scenarios:
- the customerId has a value in this case it will add to the filed (that has the name as the key) the 'enabled' configs
- if the value is undefined or null we simple add the 'disabled' configs to that field

### Practical Outcome
Enabled Configuration: When a customer is selected, the 'invoiceAddress' field become active and are populated with relevant query variables tailored to the selected customer. This allows for a more streamlined and relevant user experience, as the addresses displayed are specific to the chosen customer.

Disabled Configuration: If no customer is selected, the field become disabled and are cleared of any specific queries, preventing the user from entering irrelevant or incorrect information.