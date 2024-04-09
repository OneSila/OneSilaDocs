# Show Pages

## Introduction

Show pages in Vue.js applications are designed to display detailed information about a specific item or entity. This guide covers how to set up and configure show pages effectively, focusing on the use of constructors for consistent configuration.

## Show Configuration

### Creating Show Page Configurations
A `showConfigConstructor` function is utilized to create configurations for the show pages. This setup defines the fields and the layout for displaying detailed information.

You can find out more about the show component [here](./../shared_utilities/components/organisms/general-show/index.md) and the used fields [here](./../shared_utilities/components/organisms/general-show/show_fields.md) 

### Example of `showConfigConstructor`
Here's an example of `showConfigConstructor` that configures a company details page:

```typescript
export const showConfigConstructor = (t: Function, id): ShowConfig => ({
  cols: 1,
  subscription: getCompanySubscription,
  subscriptionKey: 'company',
  subscriptionVariables: {id: id},
  addBack: false,
  backUrl:  {name: 'contacts.companies.list' },
  addEdit: false,
  editUrl: {name: 'contacts.companies.edit', params: {id: id} },
  addDelete: false,
  deleteMutation: deleteCompanyMutation,
  deleteVariables: {id: id},
  fields: [
 {
    name: 'name',
    type: FieldType.Text,
    label:  t('shared.labels.name'),
    showLabel: true
  },
  {
    name: 'vatNumber',
    type: FieldType.Text,
    label: t('contacts.companies.labels.vat'),
    showLabel: true
  },
  {
    name: 'eoriNumber',
    type: FieldType.Text,
    label: t('contacts.companies.labels.eori'),
    showLabel: true
  },
  {
    type: FieldType.Boolean,
    label: t('contacts.companies.labels.supplier'),
    name: 'isSupplier',
    showLabel: true

  },
  {
    type: FieldType.Boolean,
    label: t('contacts.companies.labels.customer'),
    name: 'isCustomer',
    showLabel: true
  },
  {
    type: FieldType.Boolean,
    label: t('contacts.companies.labels.influencer'),
    name: 'isInfluencer',
    showLabel: true
  },
  {
    type: FieldType.Boolean,
    label: t('contacts.companies.labels.internalCompany'),
    name: 'isInternalCompany',
    showLabel: true
  },
  {
    type: FieldType.Array,
    name: 'relatedCompanies',
    label: t('contacts.companies.labels.relatedCompanies'),
    clickable: true,
    clickUrl: {name: 'contacts.companies.show'},
    clickIdentifiers: [{id: ['id']}],
    keys: ['name'],
    showLabel: true
  }
  ]

});
```

This configuration sets up a show page for a company, defining each field that should be displayed, including its type and label. It also sets up navigation and action buttons like edit and delete, as per the requirements.

## Implementing the Show Page

In the Vue component, where the show page is implemented, the configuration is instantiated and passed to the `GeneralShow` component.

```typescript
import { ref } from "vue";
import { useRoute } from "vue-router";
import { useI18n } from 'vue-i18n';
import { showConfigConstructor } from '../configs';

const { t } = useI18n();
const route = useRoute();
const id = ref(String(route.params.id));
const showConfig = showConfigConstructor(t, id.value);
```

```vue
<template>
  <GeneralShow :config="showConfig" />
</template>
```

In this example, the `showConfig` is created based on the ID from the route parameters. This ID is then used to fetch and display the relevant details for the company.

## Conclusion
Show pages are a powerful way to present detailed information about a specific item in a Vue.js application. By configuring show pages through a showConfigConstructor, developers can easily define and adjust the display of data, ensuring a consistent and efficient user experience.

This approach allows for a high level of customization and functionality, including links to related data and integrated actions like edit or delete, making it an ideal solution for detailed data presentation in Vue.js applications. Also it's based on subscription so we have real-time updates.