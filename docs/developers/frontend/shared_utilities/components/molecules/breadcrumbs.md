
# Breadcrumbs Component

## Overview
`Breadcrumbs.vue` is a navigational component that helps users to keep track of their locations within programs, documents, or websites.

## Properties
- `links`: An array of objects representing each breadcrumb link. Each object should have a `path` and `name` property.

### Usage
```vue
<template>
  <Breadcrumbs :links="[{ path: { name: 'dashboard' }, name: 'Dashboard' }, { name: 'Profile' }]"/>
</template>
```
This will render a breadcrumb trail with links to 'Dashboard' and a non-clickable 'Profile'.