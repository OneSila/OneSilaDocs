
# FilterManager Component

## Overview
The `FilterManager.vue` component is designed to manage filtering, ordering, and pagination for Apollo GraphQL queries. It is highly configurable and integrates seamlessly with Vue Router to maintain filter state across page navigation.

## Properties
- `searchConfig`: An object specifying the configuration for search, filters, order, and pagination.

## Usage
The `FilterManager` component is used as a slot container to pass down filter, order, and pagination variables to its slot contents, typically an `ApolloQuery` component.

### Example:
```vue
<FilterManager :searchConfig="searchConfig">
  <template v-slot:variables="{ filterVariables, orderVariables, pagination }">
    <ApolloQuery :query="query"
                 :variables="{filter: fixedFilterVariables !== null ? { ...filterVariables, ...fixedFilterVariables } : filterVariables,
                              order: fixedOrderVariables !== null ? { ...orderVariables, ...fixedOrderVariables } : orderVariables,
                              first: pagination.first,
                              last: pagination.last,
                              before: pagination.before,
                              after: pagination.after }">
      <!-- Your content here -->
    </ApolloQuery>
  </template>
</FilterManager>
```

In this setup, the `FilterManager` component is responsible for parsing query parameters and providing filter, order, and pagination variables to the ApolloQuery component.

## Integration with Apollo GraphQL
The component is tailored for use with Apollo GraphQL, enabling powerful data fetching capabilities combined with dynamic filtering and pagination. This makes it an ideal choice for building data-driven Vue applications.

We will show more of how to use it in the [general listing organism component](./../organisms/general_listing.md) and it the [listing page practical examples](./../../../practical_use/list_page.md).