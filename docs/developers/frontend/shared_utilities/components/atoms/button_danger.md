# DangerButton

The `DangerButton` component is used to signify actions that have potentially destructive effects, like deleting or removing data.

### Props

- Inherits all props from `Button` component.

### Usage

```html
<DangerButton
  :loading="loadingState"
  :disabled="isDisabled"
  custom-class="additionalClasses"
  @click="handleDangerAction"
>
  Delete
</DangerButton>
```