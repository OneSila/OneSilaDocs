
# RecursiveAccordion

## Overview
The `RecursiveAccordion` component is a versatile component used to display hierarchical data structures. It leverages the `Accordion` component to present nested data in an expandable format, enhancing readability and user experience.

## Properties
- `data`: The data object that the component should display. The data can be a nested structure of objects and arrays.

## Usage
```vue
<template>
  <RecursiveAccordion :data="nestedData" />
</template>
```

This component recursively renders each level of the nested data using `Accordion` components, allowing for a deep dive into the hierarchical structure. It's particularly useful for visualizing JSON-like data structures or deeply nested arrays and objects.

## Events
- `clicked`: Emitted when a thumbnail within the accordion is clicked.

## Slots
- `content`: Slot to provide custom content for the accordion panels.

## Styling
The component uses Tailwind CSS for styling, providing a consistent and modern look. It can be customized with Tailwind's utility classes.