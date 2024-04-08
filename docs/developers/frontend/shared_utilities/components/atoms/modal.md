
# Modal

The `Modal` component is a versatile dialog box/popup mechanism for displaying content on top of the existing content.

### Props

- `modelValue`: A boolean that controls the visibility of the modal.

### Events

- `closed`: Emitted when the modal is closed.
- `update:modelValue`: Emitted with the updated visibility state.

### Usage

```vue
<Modal v-model="showInviteModal" @closed="showInviteModal = false">
    <CompanyInviteMember :language="language" @invite-submitted="onInviteSubmitted" @cancel-clicked="showInviteModal = false" />
</Modal>
```