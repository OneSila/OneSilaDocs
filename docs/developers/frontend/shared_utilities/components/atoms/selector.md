
# Selector

## Overview
The `Selector.vue` component is a versatile and customizable select dropdown. It's designed to provide an enhanced user experience for selecting options from a list. This component supports multiple features including search functionality, multiple selections, custom label and value mapping, and more.

## Properties
- `options`: Array of options for the dropdown.
- `modelValue`: The currently selected value or values in case of multiple selections.
- `labelBy`: Field name to display as the option label.
- `valueBy`: Field name to use as the underlying option value.
- `placeholder`: Placeholder text displayed in the selector.
- `dropdownPosition`: Specifies the dropdown opening position.
- `boolean`: A boolean value to determine some behavior (further detail needed).
- `mandatory`: Whether a selection is mandatory.
- `multiple`: Support for selecting multiple options.
- `filterable`: Allows filtering through the options.
- `removable`: If true, selected options can be removed.
- `limit`: Limits the number of options shown in the dropdown.
- `isLoading`: Displays a loading state when options are being fetched.
- Additional properties for further customization and control.

## Usage

### Basic Usage
```vue
<Selector
  v-model="selectedValue"
  :options="optionsList"
  labelBy="name"
  valueBy="id"
  placeholder="Select an option"
/>
```

### Advanced Usage with GraphQL and Internationalization
This example demonstrates integrating the selector with a GraphQL query and internationalization for dynamic options and placeholders.

```vue
<ApolloQuery :query="languagesQuery">
  <template v-slot="{ result: { data } }">
    <Selector
      v-if="data"
      v-model="form.language"
      :options="data.languages"
      labelBy="name"
      valueBy="code"
      :placeholder="t('auth.register.company.placeholders.selector.language')"
      filterable
    />
  </template>
</ApolloQuery>
```

### Using with Dynamic Filtering and Customization
This example shows the use of dynamic filtering, custom dropdown positions, and other properties for a tailored user experience.

```vue
<Selector
  v-model="selectedValue"
  :options="filter.options"
  :label-by="filter.labelBy"
  :value-by="filter.valueBy"
  :placeholder="placeholder"
  :dropdown-position="dropdownPosition"
  :mandatory="mandatory"
  :multiple="multiple"
  :filterable="filterable"
  :removable="removable"
  :limit="limit"
  :disabled="disabled"
/>
```

These examples demonstrate the flexibility of the `Selector` component, making it suitable for a wide range of applications requiring user input through dropdown selections.