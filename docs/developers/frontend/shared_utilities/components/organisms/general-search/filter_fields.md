# GeneralSearch Filters Configuration

## Overview
`GeneralSearch` supports an array of different filter types for advanced search functionality. Each filter type comes with specific configurations, enabling a wide range of search criteria.

### BaseFilter (Common for All Filters)
| Key               | Type                   | Mandatory | Description |
|-------------------|------------------------|-----------|-------------|
| `type`            | `FieldType`            | Yes       | The type of filter. |
| `name`            | `string`               | Yes       | The attribute name in the GraphQL schema; crucial for accurate filtering on the server. |
| `label`           | `string`               | Yes       | User-friendly label for the filter. |
| `default`         | `any`                  | Optional  | Default value of the filter. |
| `disabled`        | `boolean or null`      | Optional  | Indicates if the filter is initially disabled. |
| `addExactLookup`  | `boolean`              | Optional  | If set, adds exact lookup for the filter value. |
| `exactLookupKeys` | `string[]`             | Optional  | Keys for exact lookup, if `addExactLookup` is true. |

### BooleanFilter
Inherits `BaseFilter`

| Key               | Type      | Mandatory | Description |
|-------------------|-----------|-----------|-------------|
| `strict`          | `boolean` | Yes       | Enforces strict Boolean values. |
| `dropdownPosition`| `string`  | Optional  | Position of the dropdown. |
| `placeholder`     | `string`  | Optional  | Placeholder text for the filter. |

### ValueFilter
Inherits `BaseFilter`

| Key           | Type      | Mandatory | Description |
|---------------|-----------|-----------|-------------|
| `placeholder` | `string`  | Optional  | Placeholder text for the filter. |
| `error`       | `boolean` | Optional  | Indicates if there is an error state. |
| `transparent` | `boolean` | Optional  | Makes the filter transparent if set to true. |
| `secret`      | `boolean` | Optional  | Hides the filter value (useful for sensitive data). |
| `number`      | `boolean` | Optional  | Indicates if the filter accepts only numeric values. |
| `maxNumber`   | `number`  | Optional  | Maximum numeric value allowed. |
| `minNumber`   | `number`  | Optional  | Minimum numeric value allowed. |

### ChoiceFilter
Inherits `BaseFilter`

| Key                | Type      | Mandatory | Description |
|--------------------|-----------|-----------|-------------|
| `options`          | `array`   | Yes       | Array of options for the filter. Each option should be an object containing `labelBy` and `valueBy` keys. |
| `labelBy`          | `string`  | Yes       | Field name for the option label. |
| `valueBy`          | `string`  | Yes       | Field name for the option value. |
| `placeholder`      | `string`  | Optional  | Placeholder text for the filter. |
| `dropdownPosition` | `string`  | Optional  | Position of the dropdown. |
| `mandatory`        | `boolean` | Optional  | Indicates if a selection is mandatory. |
| `multiple`         | `boolean` | Optional  | Allows multiple selections. |
| `filterable`       | `boolean` | Optional  | Allows filtering within the options. |
| `removable`        | `boolean` | Optional  | Allows removal of selected options. |
| `limit`            | `number`  | Optional  | Limit for the number of selectable options. |

### QueryFilter
Inherits `BaseFilter`

| Key                | Type      | Mandatory | Description                                                            |
|--------------------|-----------|-----------|------------------------------------------------------------------------|
| `labelBy`          | `string`  | Yes       | Field name for the option label.                                       |
| `valueBy`          | `string`  | Yes       | Field name for the option value.                                       |
| `query`            | `string`  | Yes       | GraphQL query for fetching data.                                       |
| `dataKey`          | `string`  | Yes       | Key to extract data from the query response.                           |
| `placeholder`      | `string`  | Optional  | Placeholder text for the filter.                                       |
| `dropdownPosition` | `string`  | Optional  | Position of the dropdown.                                              |
| `mandatory`        | `boolean` | Optional  | Indicates if a selection is mandatory.                                 |
| `isEdge`           | `boolean` | Optional  | If true, indicates the response has edges in the GraphQL query result. |
| `multiple`         | `boolean` | Optional  | Allows multiple selections.                                            |
| `filterable`       | `boolean` | Optional  | Allows filtering within the options.                                   |
| `removable`        | `boolean` | Optional  | Allows removal of selected options.                                    |
| `limit`            | `number`  | Optional  | Limit for the number of selectable options.                            |

### DateFilter (Still in Development)
Inherits `BaseFilter`

### SliderFilter (Still in Development)
Inherits `BaseFilter`

### CheckboxFilter
Inherits `BaseFilter`

| Key             | Type      | Mandatory | Description |
|-----------------|-----------|-----------|-------------|
| `uncheckedValue`| `string`  | Optional  | Specifies the value when unchecked. Can be either 'null' or 'false'. |

## Special Features
- **Lookup Types**: The plan is to expand the filter configuration to allow specifying the type of lookup (`exact`, `in`, `icontains`, etc.). This will provide greater flexibility in filtering based on various conditions.

## Usage
Integrate `GeneralSearch` into applications requiring advanced search and filtering functionalities. It is ideal for scenarios where users need to sift through large datasets based on multiple criteria.

