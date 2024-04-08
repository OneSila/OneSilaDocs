
# Text Input

A general-purpose `TextInput` component for various types of text input including standard, secret (password), and number input types.

## Props

- `placeholder`: Placeholder text for the input.
- `modelValue`: The binding value of the input.
- `error`: Displays the input in an error state if true.
- `transparent`: Makes the input background transparent.
- `disabled`: Disables the input.
- `secret`: If true, treats the input as a password field.
- `number`: Allows only numerical input.
- `float`: Allows floating-point numerical input.
- `minNumber`: Minimum value for numerical input.
- `maxNumber`: Maximum value for numerical input.
- `focused`: Automatically focus the input when the component is mounted.
- `allowAutocomplete`: Enables the browser's autocomplete feature.

## Usage

```vue
<TextInput placeholder="Enter text" v-model="textInputValue" />
```