
# GeneralForm Overview

## Description
`GeneralForm` is a Vue component designed for dynamic form creation and editing. It supports a wide range of field types and is highly configurable to cater to different form requirements in an application.

## Configuration
The `FormConfig` object defines the structure, behavior, and interactions of the form.

### Configuration Elements

| Key                   | Type                | Mandatory | Default                   | Description |
|-----------------------|---------------------|-----------|---------------------------|-------------|
| `cols`                | `1 or 2`            | Optional  | `1`                       | Number of columns in the form layout. |
| `type`                | `FormType`          | Yes       |                           | Form type – `CREATE` for new entries or `EDIT` for editing. |
| `mutation`            | `string`            | Yes       |                           | GraphQL mutation string for form submission. |
| `mutationKey`         | `string`            | Yes       |                           | Key in the GraphQL response for result access. |
| `mutationId`          | `string`            | Optional  |                           | ID for the item being edited (EDIT form only). |
| `query`               | `string`            | Optional  |                           | GraphQL query string for fetching existing data (EDIT forms). |
| `queryVariables`      | `object`            | Optional  |                           | Variables for the query. |
| `queryDataKey`        | `string`            | Optional  |                           | Key to extract data from query response. |
| `submitUrl`           | `Url`               | Yes       |                           | URL for post-operation form submission. |
| `submitLabel`         | `string`            | Optional  | `Save`                    | Label for the submit button. |
| `addSubmitAndContinue`| `boolean`           | Optional  | `true`                    | Whether to show the submit-and-continue button. |
| `submitAndContinueLabel` | `string`         | Optional  | `Save and Continue`       | Label for the submit-and-continue button. |
| `submitAndContinueUrl`| `Url`               | Optional  |                           | URL for submit-and-continue operation. |
| `hideButtons`         | `boolean`           | Optional  | `false`                   | Whether to hide submission buttons. |
| `addCancel`           | `boolean`           | Optional  | `true`                    | Whether to show the cancel button. |
| `cancelLabel`         | `string`            | Optional  | `Back`                    | Label for the cancel button. |
| `cancelUrl`           | `Url`               | Optional  |                           | URL for navigation after canceling. |
| `addDelete`           | `boolean`           | Optional  | `true`                    | Whether to show a delete button (EDIT forms). |
| `deleteLabel`         | `string`            | Optional  | `Delete`                  | Label for the delete button. |
| `deleteMutation`      | `string`            | Optional  |                           | GraphQL mutation for the delete operation. |
| `deleteUrl`           | `Url`               | Optional  | Same as `submitUrl`       | URL to navigate after deletion. |
| `customStyle`         | `string`            | Optional  |                           | Custom CSS style for form styling. |
| `afterSubmitCallback` | `function`          | Optional  |                           | Callback function after form submission. |
| `fields`              | `FormField[]`       | Yes       |                           | Array of `FormField` objects defining each field. |
| `helpSections`        | `HelpSection[]`     | Optional  |                           | Instructional content sections. |

### FormType Enumeration
`FormType` includes two values: `CREATE` for creating new entries and `EDIT` for editing existing entries.

### HelpSection Interface
Provides instructional content sections:
- `header`: Optional section header.
- `content`: Mandatory content text.

### Fields Configuration
For details on field configuration, refer to the [Form Fields documentation](./form_fields.md).

## Internal Components
`GeneralForm` consists of several internal components, each handling specific form aspects:

- **FormCreate**: Manages the creation of new entries.
- **FormEdit**: Facilitates editing existing entries.
- **FormLayout**: Renders the form layout based on configuration and field types.
- **HelpSection**: Provides guidance and information related to the form.
- **SubmitButtons**: Handles the rendering and functionality of submission buttons, including submit, submit-and-continue, cancel, and delete buttons.

## Usage
The component is utilized in scenarios demanding a flexible and dynamic form. It's versatile to adapt to various data types and structures.

## Sample Configuration
```vue
const formConfig = {
  ...baseFormConfigConstructor(
    t,
    FormType.CREATE,
    createCompanyAddressMutation,
    'createAddress',
    companyId.value.toString()
  ),
  submitAndContinueUrl: { name: 'contacts.companies.address.edit', params: { companyId: companyId.value } }
};

<GeneralForm :config="formConfig  as FormConfig" />
```

Where the baseFormConfigConstructor are shared functions that look like this:

```vue
export const baseFormConfigConstructor = (
  t: Function,
  type: FormType,
  mutation: any,
  mutationKey: string,
  companyId: string,
  addressType: string | null = null
): FormConfig => ({
  cols: 1,
  type: type,
  mutation: mutation,
  mutationKey: mutationKey,
  submitUrl: { name: 'contacts.companies.show', params: {id: companyId }},
  fields: [
      {
        type: FieldType.Hidden,
        name: 'company',
        value: { "id": companyId}
      },
      {
        type: FieldType.Text,
        name: 'address1',
        label: t('contacts.companies.address.labels.addressOne'),
        placeholder: t('contacts.companies.address.placeholders.addressOne')
      },
      {
        type: FieldType.Text,
        name: 'address2',
        label: t('contacts.companies.address.labels.addressTwo'),
        placeholder: t('contacts.companies.address.placeholders.addressTwo'),
        optional: true
      },
      {
        type: FieldType.Text,
        name: 'address3',
        label: t('contacts.companies.address.labels.addressThree'),
        placeholder: t('contacts.companies.address.placeholders.addressThree'),
        optional: true
      },
      {
        type: FieldType.Text,
        name: 'city',
        label: t('contacts.companies.address.labels.city'),
        placeholder: t('contacts.companies.address.placeholders.city')
      },
      {
        type: FieldType.Text,
        name: 'postcode',
        label: t('contacts.companies.address.labels.postcode'),
        placeholder: t('contacts.companies.address.placeholders.postcode')
      },
      {
        type: FieldType.Query,
        name: 'country',
        label: t('contacts.companies.address.placeholders.country'),
        labelBy: 'name',
        valueBy: 'code',
        query: countriesQuery,
        dataKey: 'countries',
        isEdge: false,
        multiple: false,
        filterable: true,
      },
      getAddressTypeField(addressType, t),
      {
        type: FieldType.Query,
        name: 'contact',
        query: peopleQuery,
        queryVariables: {filter: {company: {id: {exact: companyId}}}},
        label: t('contacts.companies.address.labels.contact'),
        labelBy: 'firstName',
        valueBy: 'id',
        dataKey: 'people',
        isEdge: true,
        multiple: false,
        filterable: true,
        formMapIdentifier: 'id',
        createOnFlyConfig: personOnTheFlyConfig(t, companyId),
        optional: true
      }
    ],
});
```

## Enhancements and Features
- **Dynamic Field Configuration**: Enables on-the-fly updates to field properties based on user interaction.
- **Data Validation and Consistency**: Assures the integrity and standardization of form data.
- **Backend Integration**: Connects seamlessly with GraphQL for data operations.

To use `GeneralForm`, provide it with the `FormConfig` object. The component will automatically generate the form based on this configuration.

We will go more in deep about how to use it on the practical use for [form pages](./../../../../practical_use/form_page.md)