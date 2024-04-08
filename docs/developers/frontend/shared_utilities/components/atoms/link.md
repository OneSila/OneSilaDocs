
# Link

The `Link` component is used for creating anchor tags in the application, supporting both internal navigation and external links.

### Props

- `path`: The URL or path for the link. Can be a string or a Vue Router location object.
- `inlineBlock`: If set, the link is displayed as an inline-block element.
- `block`: If set, the link is displayed as a block element.
- `disabled`: Disables the link.
- `external`: If set, the link is treated as an external link and will open in a new tab.
- `gutter`: Sets both vertical and horizontal padding.
- `verticalGutter`: Sets vertical padding.
- `horizontalGutter`: Sets horizontal padding.
- `selectable`: If set, the link text can be selected.

## Usage

### Internal Link
```vue
<Link path="/your-internal-path">
  Internal Link
</Link>
```

### External Link
```vue
<Link path="https://www.externalwebsite.com" external>
  External Link
</Link>
```