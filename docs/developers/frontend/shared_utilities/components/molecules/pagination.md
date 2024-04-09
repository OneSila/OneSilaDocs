
# Pagination

## Overview
`Pagination.vue` provides a navigational pagination component, allowing users to browse through pages of content. It supports first, last, next, and previous page navigation.

## Properties
- `pageInfo`: An object containing information about pagination state (`endCursor`, `startCursor`, `hasNextPage`, `hasPreviousPage`).
- `alignment`: Sets the alignment of the pagination buttons (`start`, `center`, `end`).
- `buttonClass`: Defines the style of the pagination buttons (`default`, `solid`, `rounded`).
- `useIcons`: If true, icons will be used for the navigation buttons.

## Usage
```vue
<Pagination :pageInfo="pageInfo" alignment="center" buttonClass="default" :useIcons="true" />
```

## Example
```vue
<template>
  <Pagination
    :pageInfo="{ 
      endCursor: 'cursor', 
      startCursor: 'cursor', 
      hasNextPage: true, 
      hasPreviousPage: false 
    }"
    alignment="center"
    buttonClass="default"
    useIcons
  />
</template>
```