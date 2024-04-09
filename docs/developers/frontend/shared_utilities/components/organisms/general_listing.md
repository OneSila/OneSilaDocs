# GeneralListing Overview

## Description
`GeneralListing` is a Vue component designed for displaying lists of items with features like filtering, sorting, pagination, and CRUD (Create, Read, Update, Delete) actions. It's highly configurable and works seamlessly with GraphQL backends.

## Configuration
`GeneralListing` uses two main configurations: `SearchConfig` for search and filtering, and `ListingConfig` for defining how the list and its items are displayed.

### SearchConfig
Refer to [GeneralSearch Configuration](./general-search/index.md) for details on setting up search and filters in `GeneralListing`.

### ListingConfig
Defines the layout and functionality of the listing page.

| Key                   | Type                | Description |
|-----------------------|---------------------|-------------|
| `headers`             | `string[]`          | Column headers for the listing table. |
| `fields`              | `ShowField[]`       | Fields to be displayed for each item, using the configuration from `GeneralShow`. Refer to [Show Fields](./general-show/show_fields.md). |
| `identifierVariables` | `Record<string, string>` | Additional variables for constructing dynamic routes or actions. |
| `urlQueryParams`      | `Record<string, string>` | Query parameters to include in URLs for actions like edit or show. |
| `identifierKey`       | `string`            | Key to identify individual items, usually 'id'. |
| `paramIdentifier`     | `string`            | Parameter identifier for routing, typically 'id'. |
| `addEdit`             | `boolean`           | Adds an edit button for each item. |
| `editUrlName`         | `string`            | Route name for the edit operation. |
| `addShow`             | `boolean`           | Adds a show button for each item. |
| `showUrlName`         | `string`            | Route name for the show operation. |
| `addDelete`           | `boolean`           | Adds a delete button for each item. |
| `deleteMutation`      | `string`            | GraphQL mutation string for the delete operation. |
| `deleteMutationRefetchQueries` | `string[]`  | Queries to refetch after a delete operation. |
| `addPagination`       | `boolean`           | Enables pagination for the listing. |
| `paginationConfig`    | `PaginationConfig`  | Configuration for pagination appearance and behavior. |
| `addActions`          | `boolean`           | Whether to show action buttons (edit, show, delete) for each item. |

### PaginationConfig
Configures pagination appearance and behavior.

| Key           | Type      | Description |
|---------------|-----------|-------------|
| `alignment`   | `string`  | Alignment of the pagination ('start', 'center', 'end'). |
| `buttonClass` | `string`  | Class for pagination buttons ('default', 'solid', 'rounded'). |
| `useIcons`    | `boolean` | Whether to use icons in pagination buttons. |

### ShowFields

You can read more about ShowFields [here](./general-show/show_fields.md).

## Features
- **Integration with GraphQL**: Directly works with GraphQL queries for fetching, updating, and deleting data.
- **Dynamic Fields**: Leverages `ShowField` configurations from `GeneralShow` for flexible display options.
- **Search and Filters**: Incorporates `SearchConfig` from `GeneralSearch` for powerful search and filtering capabilities.
- **CRUD Actions**: Supports actions like editing, viewing, and deleting items directly from the list.
- **Customizable Layout**: Offers extensive customization for headers, fields, and actions.

## Usage
Use `GeneralListing` in scenarios where you need to display lists of data with options for search, filter, sort, and perform actions on individual items. It's ideal for admin panels, data dashboards, and any application requiring a dynamic listing of items.

## Sample Configuration
```vue
const searchConfig = searchConfigConstructor(t);
const listingConfig = {
  headers: ['Name', 'Status', 'Actions'],
  fields: [
    { type: FieldType.Text, name: 'name' },
    { type: FieldType.Boolean, name: 'isActive' }
  ],
  addEdit: true,
  editUrlName: 'itemEdit',
  addShow: true,
  showUrlName: 'itemDetails',
  addDelete: true,
  deleteMutation: deleteItemMutation,
  addPagination: true,
  paginationConfig: {
    alignment: 'end',
    buttonClass: 'rounded',
    useIcons: true
  },
  addActions: true
};

<GeneralListing
  :searchConfig="searchConfig"
  :config="listingConfig"
  query="itemsQuery"
  queryKey="items"
/>
```

For more detailed implementations and practical uses with real life scenarios, refer to the [listing pages documentation](./../../../practical_use/list_page.md).