# GeneralSearch Overview

## Description
`GeneralSearch` is a versatile Vue component designed to facilitate complex searching and filtering functionalities in web applications. It integrates elements like a search bar, filter modal, ordering dropdown, and a reset filter button, offering a comprehensive and dynamic user experience.

## Configuration
`GeneralSearch` is configured using the `SearchConfig` object, which includes settings for search functionality, filters, order criteria, and pagination.

### Configuration Elements

| Key             | Type             | Description |
|-----------------|------------------|-------------|
| `search`        | `boolean`        | Enables a search input for keyword searches. |
| `cols`          | `number`         | Specifies the number of columns in the filter layout. |
| `orderKey`      | `string`         | Defines the query parameter key for ordering results. |
| `filters`       | `SearchFilter[]` | Array of filter objects for advanced filtering options. |
| `orders`        | `OrderCriteria[]`| Criteria for sorting and ordering search results. |
| `limitPerPage`  | `number`         | Maximum number of results to display per page. |

### OrderCriteria
Defines the sorting order of search results:

| Key     | Type       | Description |
|---------|------------|-------------|
| `name`  | `string`   | The name of the ordering field as expected by the backend. |
| `label` | `string`   | User-friendly label for the ordering option. |
| `type`  | `OrderType`| Sort order type: `ASC` for ascending or `DESC` for descending. |

### Internal Components
`GeneralSearch` combines several internal components:

- **SearchInput**: Offers a user interface for keyword searches.
- **GeneralFilter**: Hosts various filtering options as defined in the `SearchConfig`.
- **GeneralOrdering**: Allows users to select the order in which search results are presented.
- **FilterModal**: A modal interface for users to apply different filters to the search results.

## Features
- **All-in-One**: Consolidates search and filtering functionalities in a single, cohesive component.
- **Customizable Filters**: Easily configurable filters to suit different data types and search requirements.
- **Dynamic Sorting**: Allows users to dynamically sort search results based on different criteria.
- **Quick Integration**: Designed for seamless integration into existing Vue applications.

## Usage
The `GeneralSearch` component can be integrated into web applications where advanced search capabilities are required. It's particularly useful in data-driven applications where users need to filter and sort through large datasets.

## Sample Configuration
```typescript
const searchConfig = searchConfigConstructor(t);

<GeneralSearch :searchConfig="searchConfig" />
```

Where searchConfigConstructor is a function that returns a SearchConfig object:

```typescript
export const searchConfigConstructor = (t: Function): SearchConfig => ({
  search: false,
  orderKey: "sort",
  filters: [
    {
      type: FieldType.Choice,
      name: 'status',
      label: t('sales.orders.labels.status.title'),
      labelBy: 'name',
      valueBy: 'code',
      options: getStatusOptions(t),
      addExactLookup: true
    },
    {
      type: FieldType.Choice,
      name: 'reasonForSale',
      label: t('sales.orders.labels.reasonForSale.title'),
      labelBy: 'name',
      valueBy: 'code',
      options: getReasonForSaleOptions(t),
      addExactLookup: true
    },
    {
      type: FieldType.Query,
      name: 'customer',
      label: t('contacts.people.labels.customer'),
      labelBy: 'name',
      valueBy: 'id',
      query: customersQuery,
      dataKey: 'customers',
      filterable: true,
      isEdge: true,
      addExactLookup: true,
      exactLookupKeys: ['id']
    },
  ],
  orders: [
    {
      name: 'status',
      label: t('sales.orders.labels.status.title'),
      type: OrderType.ASC
    },
    {
      name: 'status',
      label: t('sales.orders.labels.status.title'),
      type: OrderType.DESC
    },
    {
      name: 'reference',
      label: t('sales.orders.labels.reference'),
      type: OrderType.ASC
    },
    {
      name: 'reference',
      label: t('sales.orders.labels.reference'),
      type: OrderType.DESC
    }
  ]
});
```

For details on configuring individual filters within GeneralSearch, please refer to the [Search Filters documentation](./filter_fields.md).

We will go more in deep about how to use it on the practical use for [listing pages](./../../../../practical_use/list_page.md)