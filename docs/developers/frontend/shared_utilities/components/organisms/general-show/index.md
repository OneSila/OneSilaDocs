# GeneralShow Overview

## Description
`GeneralShow` is a Vue component designed to display detailed information in a structured and readable format. It is capable of presenting various data types, including text, images, nested text, arrays, badges, and more, with customization options for each.

## Configuration
The `ShowConfig` object is used to configure the `GeneralShow` component, specifying how data is presented and interacted with.

## Configuration Elements

| Key                     | Type                  | Mandatory | Description |
|-------------------------|-----------------------|-----------|-------------|
| `cols`                  | `1 or 2`              | Optional  | Number of columns for the layout. |
| `subscription`          | `string`              | Yes       | GraphQL subscription string for real-time data. |
| `subscriptionKey`       | `string`              | Yes       | Key in the GraphQL response for subscription data. |
| `subscriptionVariables` | `object`              | Optional  | Variables for the subscription. |
| `addBack`               | `boolean`             | Optional  | If true, adds a back button. |
| `backUrl`               | `Url`                 | Optional  | URL to navigate to when back button is clicked. |
| `addEdit`               | `boolean`             | Optional  | If true, adds an edit button. |
| `editUrl`               | `Url`                 | Optional  | URL for edit operation. |
| `addDelete`             | `boolean`             | Optional  | If true, adds a delete button. |
| `deleteMutation`        | `string`              | Optional  | GraphQL mutation for delete operation. |
| `deleteVariables`       | `object`              | Optional  | Variables for the delete mutation. |
| `deleteUrl`             | `Url`                 | Optional  | URL to navigate to after deletion. |
| `customStyle`           | `string`              | Optional  | Custom CSS style for the component. |
| `title`                 | `string`              | Optional  | Title of the display page. |
| `description`           | `string`              | Optional  | Description of the display page. |
| `fields`                | `ShowField[]`         | Yes       | Array of fields to display. |



### Custom Functions
- **updateField**: Updates configuration for a specific field.
- **getFieldComponent**: Maps a field type to its corresponding component.
- **accessNestedProperty**: Accesses nested properties in a data object.

## Features
- **Flexible Layout**: Supports single or dual-column layouts.
- **Real-Time Data**: Integrates with GraphQL subscriptions for live data updates.
- **Interactive Elements**: Optionally includes back, edit, and delete buttons.
- **Custom Styling**: Allows custom styles and CSS classes for personalization.
- **Variety of Field Types**: Supports a wide range of data presentations.

## Usage
`GeneralShow` is ideal for applications requiring detailed views of individual items, such as profiles, product details, or data summaries. It is highly customizable to fit various data presentation needs.

## Sample Configuration
```vue
const showConfig = showConfigConstructor(t, id.value);

<GeneralShow :config="showConfig" />
```

Where the showConfigConstructor looks like:

```typescript
export const showConfigConstructor = (t: Function, id): ShowConfig => ({
  cols: 1,
  subscription: salesPriceListSubscription,
  subscriptionKey: 'salesPriceList',
  subscriptionVariables: { pk: id },
  addBack: true,
  backUrl:  {name: 'sales.priceLists.list' },
  addEdit: true,
  editUrl: {name: 'sales.priceLists.edit', params: { id: id } },
  addDelete: true,
  deleteMutation: deleteSalesPriceListMutation,
  fields: [
    {
      name: 'name',
      type: FieldType.Text,
      label: t('shared.labels.name'),
      showLabel: true
    },
    {
      name: 'discount',
      type: FieldType.Text,
      label: t('sales.prices.labels.discountAmount'),
      showLabel: true
    },
    {
      name: 'currency',
      type: FieldType.NestedText,
      label: t('shared.labels.currency'),
      keys: ['isoCode'],
      showLabel: true
    },
    {
      name: 'notes',
      type: FieldType.Text,
      label: t('shared.labels.notes'),
      showLabel: true
    },
    {
      name: 'vatIncluded',
      type: FieldType.Boolean,
      label: t('sales.priceLists.labels.vatIncluded'),
      showLabel: true
    },
    {
      name: 'autoUpdate',
      type: FieldType.Boolean,
      label: t('sales.priceLists.labels.autoUpdate'),
      showLabel: true,
    },
    {
      type: FieldType.Array,
      name: 'customers',
      label: t('sales.customers.title'),
      clickable: true,
      clickUrl: {name: 'sales.customers.show'},
      clickIdentifiers: [{id: ['id']}],
      keys: ['name'],
      showLabel: true
    }
  ]
});
```

For details on configuring individual show fields within GeneralShow, please refer to the [Show fields documentation](./show_fields.md).

We will go more in deep about how to use it on the practical use for [form pages](./../../../../practical_use/list_page.md)