# PrimaryButton

The `PrimaryButton` component represents the primary action in a set of buttons. It's typically used to draw attention to the main action on a form or dialog.

### Props

- Inherits all props from `Button` component.

### Usage

```html
<PrimaryButton
  :loading="loadingState"
  :disabled="isDisabled"
  custom-class="additionalClasses"
  @click="handlePrimaryAction"
>
  Submit
</PrimaryButton>
```