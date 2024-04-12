
# Tabs

## Overview
The `Tabs.vue` component provides a tabbed interface for displaying content. It uses the Headless UI TabGroup for functionality.

## Properties
- `tabs`: Array of tab items with `name`, `label`, and optional `icon` and `danger` properties.
- `disabledTabs`: Array of tab names that should be disabled.
- `transparent`: Boolean to make the tab background transparent.

The tab also have a property named `alwaysRender` this will let us render a rab without actually showing it. If we don't use it each tab has its business logic independent of other even if they are defined in the same place.

So if in one tab we have a subscription that fetch the data we can't use it on the second tab if we didn't opened first the first tab. For this we came with `alwaysRender` that will render the first tab (and get the subscription data for example) without actually showing in the frontend. So if the second tab also need some data from other tab it can used it.

## Usage
```vue
<template>
  <Tabs :tabs="tabsList" :disabledTabs="disabledTabs" />
</template>
```

## Slots
- Each tab's content can be provided using named slots corresponding to the tab `name`.