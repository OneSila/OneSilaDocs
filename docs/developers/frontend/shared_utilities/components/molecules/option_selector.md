
# OptionSelector

## Overview
`OptionSelector.vue` allows creating an option selector interface, transforming non-selectable elements like images into a "checkbox" style selection. It's useful for selecting one option from a set of visual choices.

## Properties
- `choices`: An array of choices, each being an object with a `name` property.
- `modelValue`: The currently selected option's name.

## Usage
```vue
<OptionSelector v-model="form.type" :choices="typeChoice">
  <template #VARIATION>
    <!-- Content for the VARIATION option -->
  </template>
  <template #BUNDLE>
    <!-- Content for the BUNDLE option -->
  </template>
  <template #UMBRELLA>
    <!-- Content for the UMBRELLA option -->
  </template>
</OptionSelector>
```

## Example
```vue
<OptionSelector v-model="selectedType" :choices="[{ name: 'Option1' }, { name: 'Option2' }]">
  <template #Option1>
    <div>Option 1 Content</div>
  </template>
  <template #Option2>
    <div>Option 2 Content</div>
  </template>
</OptionSelector>
```