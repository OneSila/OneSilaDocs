
# SelectAllCheckbox

## Overview
The `SelectAllCheckbox.vue` component is used to create a checkbox that allows selecting or deselecting all items in a list.

## Properties
- `checked`: Boolean to indicate whether the checkbox is checked or not.

## Usage
```vue
<template>
  <SelectAllCheckbox :checked="areAllSelected" @changed="selectAllOrNone" />
</template>
```

## Events
- `changed`: Emitted when the checkbox state changes.