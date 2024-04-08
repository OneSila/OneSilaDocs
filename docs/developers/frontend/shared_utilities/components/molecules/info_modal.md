
# InfoModal

## Overview
The `InfoModal.vue` component displays an information button that, when clicked, shows a modal. The modal's content can be customized through slots.

## Properties
- `disabled`: If true, the button is disabled.
- `buttonClass`: Custom CSS class for the button.

## Usage
```vue
<InfoModal :disabled="false" buttonClass="custom-class">
  <template #content>
    <!-- Modal content goes here -->
  </template>
</InfoModal>
```