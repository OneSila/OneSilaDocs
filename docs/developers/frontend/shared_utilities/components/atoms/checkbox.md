
# Checkbox

The Checkbox component is a custom UI element for toggling a boolean value. It's designed to provide a visually appealing and customizable alternative to the default HTML checkbox.

## Usage

Here’s how to implement the Checkbox component in a Vue template:

```vue
<script setup lang="ts">
import { Checkbox } from '../../../../../atoms/checkbox';
import { ref } from 'vue';

// State for the checkbox
const checkedValue = ref(false);
</script>

<template>
  <Checkbox v-model="checkedValue" />
</template>

```

Customize the appearance by changing the `bg-primary` and `bg-gray-200` classes to suit your application's color scheme.