
# Badge

The `Badge` component is a versatile and customizable element used to display a small piece of information, like a label or a status indicator. It is designed to be compact and visually distinct, making it ideal for drawing attention to specific items within a UI.

## Usage

The `Badge` component can be used in a variety of contexts. Here's an example of how to use it in your Vue templates:

```vue
<Badge text="Completed" color="green" />
```

In this example, a `Badge` is created with the text "Completed" and a green background. The `color` prop allows you to specify the color theme of the badge, with options including `primary`, `gray`, `red`, `yellow`, `green`, `blue`, `indigo`, `purple`, and `pink`. If no color is specified, it defaults to `gray`.

## Props

The `Badge` component accepts the following props:

- `text`: The text to be displayed inside the badge.
- `color`: The color theme for the badge. Available options include `primary`, `gray`, `red`, `yellow`, `green`, `blue`, `indigo`, `purple`, and `pink`. 

## Styles

The style of the badge changes based on the `color` prop provided. Each color option applies a combination of background color, text color, and ring style specific to that theme, creating a visually appealing badge.

Feel free to use this component to highlight statuses, tags, or any small piece of information that needs to stand out in the application.