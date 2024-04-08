
# Popover

## Overview
The `Popover.vue` component is used to create a floating box, like a tooltip or a dropdown, that pops up when a user interacts with an element. It can be activated on click or hover and supports ignoring outside clicks.

## Properties
- `position`: Specifies the position of the popover relative to the trigger element.
- `hover`: Determines if the popover should activate on hover.
- `ignoreOutside`: Class name to ignore outside clicks.

## Events
- `hidden`: Emitted when the popover is closed.

## Usage
```vue
<template>
  <Popover position="bottom" @hidden="handleHidden">
    <template v-slot:trigger>
      <Button>Open Popover</Button>
    </template>
    <div>Popover Content</div>
  </Popover>
</template>
```