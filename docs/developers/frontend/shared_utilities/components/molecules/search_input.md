
# SearchInput

## Overview
The `SearchInput` component is a search field with an integrated search icon, primarily used for filtering data or initiating search queries in an application. It offers a debounce feature for efficient query handling.

## Properties
- `modelValue`: The search query string.
- `placeholder`: Optional placeholder text for the search input.
- `disabled`: Boolean indicating whether the input is disabled.
- `updateRoute`: Boolean to update the route query parameters upon search.
- `routeKey`: The key used for the search parameter in the route query.
- `debounce`: Time in milliseconds for debouncing the search input.

## Usage
```vue
<template>
  <SearchInput
    v-model="searchQuery"
    :placeholder="searchPlaceholder"
    :updateRoute="true"
    :debounce="600"
  />
</template>
```

The component utilizes the Vue Router for optionally updating the route query parameters based on the search input. This makes it ideal for use in applications with route-based filtering or search functionality.

## Events
- `update:modelValue`: Emitted when the search query is updated.
- `focus`: Emitted when the input is focused.

## Styling
This component uses Tailwind CSS for styling. The search icon is positioned absolutely within the input field, creating a clean and integrated look.