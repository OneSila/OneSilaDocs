
# Button

The `Button` component is a customizable button element used throughout the application. It supports various styles, states like loading and disabled, and custom classes for further customization.

### Props

- `loading`: Boolean - If true, shows a loading icon.
- `disabled`: Boolean - If true, disables the button interaction.
- `customClass`: String - Custom CSS class for styling the button.

### Role

The role of this component is to keep all the buttons with a very likely styling. Even if we have the custom-class we need to use at minimum.

### Usage

```html
<Button
  :loading="loadingState"
  :disabled="isDisabled"
  custom-class="additionalClasses"
  @click="handleClick"
>
  <!-- Button content goes here -->
</Button>
```