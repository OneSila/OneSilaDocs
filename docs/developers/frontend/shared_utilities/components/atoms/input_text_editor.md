
# Text Editor

`TextEditor` is a simple text area component that supports autogrowing and custom styling.

## Props

- `placeholder`: Placeholder text for the editor.
- `modelValue`: The binding value of the editor.
- `transparent`: Makes the editor's background transparent.
- `disabled`: Disables the editor.
- `autogrow`: If true, the editor expands as the user types.
- `error`: Displays the editor in an error state if true.
- `gutterX`: Horizontal padding for the editor.
- `gutterY`: Vertical padding for the editor.
- `gutterless`: Removes all padding if true.
- `blurOnEnterKeypress`: Blurs the editor when Enter is pressed.
- `scroll`: Allows scrolling in the editor.

## Usage

```vue
<TextEditor placeholder="Type here..." v-model="editorContent" autogrow />
```