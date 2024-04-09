
# ApolloSubscription

## Overview
`ApolloSubscription` is a component designed to manage GraphQL subscriptions in Vue.js applications. It helps in setting up subscriptions and handling real-time data updates.

## Properties
- `subscription`: The GraphQL subscription query.
- `variables`: Optional variables for the subscription query.

## Usage
```vue
<ApolloSubscription :subscription="yourSubscription" :variables="yourVariables">
  <template v-slot:default="{ loading, error, result }">
    <!-- Your content here -->
  </template>
</ApolloSubscription>
```

### Real-life Example
```vue
<ApolloSubscription :subscription="meSubscription">
  <template v-slot:default="{ loading, error, result }">
    <template v-if="!loading && result">
      <!-- Your content here -->
    </template>
  </template>
</ApolloSubscription>
```