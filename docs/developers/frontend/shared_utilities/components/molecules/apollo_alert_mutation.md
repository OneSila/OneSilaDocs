
# ApolloAlertMutation Component

## Overview
`ApolloAlertMutation` is a component that combines Apollo Mutation with SweetAlert2, providing a user-friendly confirmation dialog before proceeding with a GraphQL mutation. This is particularly useful for actions requiring user confirmation like deletions.

## Properties
- `mutation`: GraphQL mutation object or string.
- `mutationVariables`: Variables for the GraphQL mutation.
- `refetchQueries`: Queries to refetch post-mutation.
- `swalOptions`: Customizable options for the SweetAlert2 dialog ([SweetAlert2 Documentation](https://sweetalert2.github.io/)).
- `swalClasses`: Custom classes for different SweetAlert2 dialog elements.

## Usage
```vue
<ApolloAlertMutation
  :mutation="yourMutation"
  :mutationVariables="yourVariables"
  :refetchQueries="yourRefetchQueries"
  :swalOptions="yourSwalOptions"
  :swalClasses="yourSwalClasses"
>
  <template v-slot="{ mutate, loading }">
    <YourComponent :loading="loading" :confirmAndMutate="() => confirmAndMutate(mutate)" />
  </template>
</ApolloAlertMutation>
```

### Real-life Example
```vue
<ApolloAlertMutation
  v-if="config.addDelete && config.deleteMutation"
  :mutation="config.deleteMutation"
  :mutation-variables="config.identifierKey !== undefined ? { id: item.node[config.identifierKey] } : undefined"
  :refetch-queries="() => [{
    query: props.query,
    variables: {
      filter: fixedFilterVariables !== null ? { ...filterVariables, ...fixedFilterVariables } : filterVariables,
      order: fixedOrderVariables !== null ? { ...orderVariables, ...fixedOrderVariables } : orderVariables,
      first: pagination.first,
      last: pagination.last,
      before: pagination.before,
      after: pagination.after
    }
  }]"
>
  <!-- Custom slot content here -->
</ApolloAlertMutation>
```