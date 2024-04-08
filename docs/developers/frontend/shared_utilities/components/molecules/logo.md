
# Logo Component

## Overview
The `Logo.vue` component displays a logo image, typically used for branding. It's wrapped in a link component, which redirects to a specified route when clicked, commonly the homepage.

## Properties
- `alt`: Alternate text for the logo image.
- `to`: The route name to navigate to when the logo is clicked.

## Usage
```vue
<Logo alt="Logo Alt Text" to="{ name: 'dashboard' }" />
```