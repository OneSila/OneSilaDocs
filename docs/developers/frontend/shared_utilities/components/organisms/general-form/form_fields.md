# GeneralForm Field Configurations

## Overview
`GeneralForm` supports various field types, each with specific configurations. Below are detailed explanations and tables for each field type.

### BaseFormField (Common for All Fields)
| Key            | Type      | Mandatory | Default | Description |
|----------------|-----------|-----------|---------|-------------|
| `type`         | `FieldType`| Yes      |         | The type of field. |
| `name`         | `string`  | Yes       |         | The attribute name in the GraphQL schema; crucial for accurate data transmission to the server. |
| `optional`     | `boolean` | Optional  | `false` | Whether the field is optional. |
| `label`        | `string`  | Optional  |         | The field's label. |
| `disabled`     | `boolean` | Optional  | `false` | If the field is disabled. |
| `default`      | `any`     | Optional  |         | Default value of the field. |
| `help`         | `string`  | Optional  |         | Help text for the field. |
| `customCss`    | `string`  | Optional  |         | Custom CSS for the field. |
| `customCssClass`| `string` | Optional  |         | Custom CSS class for the field. |

### BooleanFormField
Inherits `BaseFormField`

| Key                | Type      | Mandatory | Default | Description |
|--------------------|-----------|-----------|---------|-------------|
| `strict`           | `boolean` | Yes       |         | Whether to enforce strict Boolean values. |
| `dropdownPosition` | `string`  | Optional  | `top`   | Position of the dropdown. |
| `placeholder`      | `string`  | Optional  |         | Placeholder text. |

### ValueFormField
Inherits `BaseFormField`

| Key                 | Type      | Mandatory | Default | Description |
|---------------------|-----------|-----------|---------|-------------|
| `placeholder`       | `string`  | Optional  |         | Placeholder text. |
| `error`             | `boolean` | Optional  | `false` | Indicates if there is an error. |
| `transparent`       | `boolean` | Optional  | `false` | If the field is transparent. |
| `secret`            | `boolean` | Optional  | `false` | For password fields. |
| `number`            | `boolean` | Optional  | `false` | If the field is numeric. |
| `maxNumber`         | `number`  | Optional  |         | Maximum number value. |
| `minNumber`         | `number`  | Optional  |         | Minimum number value. |
| `allowAutocomplete` | `boolean` | Optional  | `false` | If autocomplete is allowed. |

### EmailFormField
Inherits `BaseFormField`

| Key             | Type      | Mandatory | Default | Description |
|-----------------|-----------|-----------|---------|-------------|
| `placeholder`   | `string`  | Optional  |         | Placeholder text. |
| `icon`          | `string`  | Optional  |         | Icon for the field. |
| `modelValue`    | `any`     | Optional  |         | The model value. |
| `focused`       | `boolean` | Optional  | `false` | If the field is initially focused. |
| `required`      | `boolean` | Optional  | `false` | If the field is required. |

### WebsiteFormField
Inherits `BaseFormField`

| Key             | Type      | Mandatory | Default | Description |
|-----------------|-----------|-----------|---------|-------------|
| `placeholder`   | `string`  | Optional  |         | Placeholder text. |
| `icon`          | `string`  | Optional  |         | Icon for the field. |
| `modelValue`    | `any`     | Optional  |         | The model value. |
| `focused`       | `boolean` | Optional  | `false` | If the field is initially focused. |
| `required`      | `boolean` | Optional  | `false` | If the field is required. |

### TextareaFormField
Inherits `BaseFormField`

| Key                    | Type      | Mandatory | Default | Description |
|------------------------|-----------|-----------|---------|-------------|
| `placeholder`          | `string`  | Optional  |         | Placeholder text. |
| `transparent`          | `boolean` | Optional  | `false` | If the field is transparent. |
| `autogrow`             | `boolean` | Optional  | `false` | If the textarea should automatically grow. |
| `error`                | `boolean` | Optional  | `false` | Indicates if there is an error. |
| `gutterX`              | `string`  | Optional  |         | Horizontal gutter. |
| `gutterY`              | `string`  | Optional  |         | Vertical gutter. |
| `gutterless`           | `boolean` | Optional  | `false` | If the field is gutterless. |
| `blurOnEnterKeypress`  | `boolean` | Optional  | `false` | If should blur on enter keypress. |
| `scroll`               | `boolean` | Optional  | `false` | If the field should scroll. |

### ChoiceFormField
Inherits `BaseFormField`

| Key                   | Type      | Mandatory | Default | Description |
|-----------------------|-----------|-----------|---------|-------------|
| `options`             | `array`   | Yes       |         | Array of options for selection. |
| `labelBy`             | `string`  | Yes       |         | Field name for the label. |
| `valueBy`             | `string`  | Yes       |         | Field name for the value. |
| `placeholder`         | `string`  | Optional  |         | Placeholder text. |
| `dropdownPosition`    | `string`  | Optional  | `top`   | Position of the dropdown. |
| `mandatory`           | `boolean` | Optional  | `false` | If the selection is mandatory. |
| `multiple`            | `boolean` | Optional  | `false` | If multiple selections are allowed. |
| `filterable`          | `boolean` | Optional  | `false` | If the options are filterable. |
| `removable`           | `boolean` | Optional  | `true`  | If the options are removable. |
| `limit`               | `number`  | Optional  |         | Limit for the number of options. |

### ProxyChoiceFormField
Inherits `BaseFormField`

| Key                   | Type      | Mandatory | Default | Description |
|-----------------------|-----------|-----------|---------|-------------|
| `options`             | `array`   | Yes       |         | Array of options for selection. |
| `labelBy`             | `string`  | Yes       |         | Field name for the label. |
| `valueBy`             | `string`  | Yes       |         | Field name for the value. |
| `placeholder`         | `string`  | Optional  |         | Placeholder text. |
| `dropdownPosition`    | `string`  | Optional  | `top`   | Position of the dropdown. |
| `mandatory`           | `boolean` | Optional  | `false` | If the selection is mandatory. |
| `multiple`            | `boolean` | Optional  | `false` | If multiple selections are allowed. |
| `filterable`          | `boolean` | Optional  | `false` | If the options are filterable. |
| `removable`           | `boolean` | Optional  | `true`  | If the options are removable. |
| `limit`               | `number`  | Optional  |         | Limit for the number of options. |

_ProxyChoiceFormField Explanation:_
This field allows a selection that maps directly to specific model attributes, especially useful in cases like Django proxy models. For instance, given options like `{name: 'Supplier', value: 'isSupplier'}` and selecting 'Supplier', the field would set `isSupplier: true`.

### QueryFormField
Inherits `BaseFormField`

| Key                   | Type      | Mandatory | Default | Description                                          |
|-----------------------|-----------|-----------|---------|------------------------------------------------------|
| `labelBy`             | `string`  | Yes       |         | Field name for the label.                            |
| `valueBy`             | `string`  | Yes       |         | Field name for the value.                            |
| `query`               | `string`  | Yes       |         | GraphQL query for fetching data.                     |
| `queryVariables`      | `object`  | Optional  |         | Variables for the query.                             |
| `dataKey`             | `string`  | Yes       |         | Key to extract data from the query response.         |
| `isEdge`              | `boolean` | Optional  | `false` | If the response has edges in a GraphQL query result. |
| `formMapIdentifier`   | `string`  | Optional  |         | Identifier for mapping query response to the form.   |
| `placeholder`         | `string`  | Optional  |         | Placeholder text.                                    |
| `dropdownPosition`    | `string`  | Optional  | `top`   | Position of the dropdown.                            |
| `mandatory`           | `boolean` | Optional  | `false` | If the selection is mandatory.                       |
| `multiple`            | `boolean` | Optional  | `false` | If multiple selections are allowed.                  |
| `filterable`          | `boolean` | Optional  | `false` | If the options are filterable.                       |
| `removable`           | `boolean` | Optional  | `true`  | If the options are removable.                        |
| `limit`               | `number`  | Optional  |         | Limit for the number of options.                     |
| `createOnFlyConfig`   | `CreateOnTheFly` | Optional  |  | Configuration for creating entries on the fly.       |

_CreateOnTheFly Explanation:_
This feature allows users to create new entries for a particular model directly within the form. The `config` key in `CreateOnTheFly` is a `FormConfig` object, enabling users to create a new entity in a modal, with the new entry automatically selected in the form.

### DateFormField
_Still in development_

### SliderFormField
_Still in development_

### PhoneFormField
Inherits `BaseFormField`

### CheckboxFormField
Inherits `BaseFormField`

| Key              | Type         | Mandatory | Default | Description |
|------------------|--------------|-----------|---------|-------------|
| `uncheckedValue` | `'null'` or `'false'` | Optional | `false` | Value when unchecked. |

### HiddenFormField
Inherits `BaseFormField`

| Key             | Type      | Mandatory | Default | Description |
|-----------------|-----------|-----------|---------|-------------|
| `value`         | `any`     | Yes       |         | The value of the hidden field. |

Each field type extends from `BaseFormField` and adds its own unique properties. Default values are provided for optional parameters if not specified in the form configuration.


### Example of "options"

The array for all the options property should be an array with objects thtat contain the label by and value by keys. Here is an example:

```js
[
  { name: t('products.products.labels.type.choices.umbrella'), code: ProductType.Umbrella },
  { name: t('products.products.labels.type.choices.bundle'), code: ProductType.Bundle },
  { name: t('products.products.labels.type.choices.variation'), code: ProductType.Variation },
]
```

Where the name will be the label and the code will be the value that will be passed to the "name" in the form.