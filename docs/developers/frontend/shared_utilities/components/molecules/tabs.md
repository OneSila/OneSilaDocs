
# Tabs Component

## Overview
The `Tabs.vue` component provides a tabbed interface for displaying content. It uses the Headless UI TabGroup for functionality.

## Properties
- `tabs`: Array of tab items with `name`, `label`, and optional `icon` and `danger` properties.
- `disabledTabs`: Array of tab names that should be disabled.
- `transparent`: Boolean to make the tab background transparent.

## Usage
```vue
<template>
  <Tabs :tabs="tabsList" :disabledTabs="disabledTabs" />
</template>
```

## Slots
- Each tab's content can be provided using named slots corresponding to the tab `name`.