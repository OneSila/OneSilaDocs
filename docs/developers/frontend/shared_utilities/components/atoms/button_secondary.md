# SecondaryButton

The `SecondaryButton` component is used for secondary actions, complementing the primary button. It's often used to offer an alternative action.

### Props

- Inherits all props from `Button` component.

### Usage

```html
<SecondaryButton
  :loading="loadingState"
  :disabled="isDisabled"
  custom-class="additionalClasses"
  @click="handleSecondaryAction"
>
  More Info
</SecondaryButton>
```