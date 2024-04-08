# CancelButton

The `CancelButton` component is a specific button with predefined styles. It is designed to be used as a cancel action in forms or dialogs.

### Props

- Inherits all props from `Button` component.

### Usage

```html
<CancelButton
  :loading="loadingState"
  :disabled="isDisabled"
  custom-class="additionalClasses"
  @click="handleCancel"
>
  Cancel
</CancelButton>
```