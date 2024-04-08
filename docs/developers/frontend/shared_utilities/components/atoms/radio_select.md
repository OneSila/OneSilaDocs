
# Radio Input

## Overview
The `RadioInput.vue` component represents a radio button that allows users to select a single value from a predefined list of options.

## Properties
- `name`: The name attribute for the radio input.
- `modelValue`: The v-model binding for the component, representing the selected value.

## Usage
```vue
<template>
  <RadioInput name="option" v-model="selectedOption">
    Option 1
  </RadioInput>
</template>
```