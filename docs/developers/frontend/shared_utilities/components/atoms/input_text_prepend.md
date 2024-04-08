
# Text Input Prepend

The `TextInputPrepend` component is a text input with an option to prepend an icon or text.

## Props

- `id`: The ID for the input.
- `label`: Label for the input field.
- `type`: Type of the input, e.g., 'text', 'password'.
- `placeholder`: Placeholder text for the input.
- `modelValue`: The binding value of the input.

## Usage

```vue
<TextInputPrepend id="username" label="Username" type="text" placeholder="Enter your username">
  <!-- Slot for prepended content -->
  <Icon name="user" />
</TextInputPrepend>
```