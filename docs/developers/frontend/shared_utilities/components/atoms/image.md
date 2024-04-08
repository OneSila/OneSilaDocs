
# Image

The `Image` component is used for displaying images with optional cover styles and custom alt text.

## Props

- `source`: The source URL of the image.
- `cover`: A boolean to specify if the image should cover its container.
- `alt`: Alternative text for the image.

## Usage

```vue
import loginImage from '../../../assets/images/auth/login.svg';

<Image :source="loginImage" alt="Cover Image" class="w-full mx-auto" />
```