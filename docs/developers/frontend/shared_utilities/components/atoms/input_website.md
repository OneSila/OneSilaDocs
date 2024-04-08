
# Website Input

The `WebsiteInput` component is designed for URL or website address inputs, featuring validation and optional icons.

## Props

- `placeholder`: Placeholder text for the input.
- `label`: Label for the input field.
- `icon`: Icon to be displayed inside the input.
- `modelValue`: The binding value of the input.
- `disabled`: Boolean to disable the input.
- `focused`: Automatically focus the input when the component is mounted.
- `required`: Mark the input as required.

## Usage

```vue
<WebsiteInput placeholder="Enter website URL" label="Website" icon="globe" v-model="websiteUrl" />
```