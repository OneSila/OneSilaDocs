# BackgroundImage

## Overview
The `BackgroundImage` component is used for displaying a full-width background image. It's a simple component that takes an image source (`src`), alternative text (`alt`), and an optional class modifier (`classModifier`).

## Usage
To use the `BackgroundImage` component, you need to provide the `src` for the image and the `alt` text for accessibility. Optionally, you can pass a `classModifier` to customize the component's styling.

```vue
import bgGradient from '../../../assets/images/auth/bg-gradient.png';

<BackgroundImage :src="bgGradient" alt="Gradiant packground" />
```

If you want to override the default full-width styling, you can pass a `classModifier`.

```vue
import comingSoonObject1 from '../../../assets/images/auth/coming-soon-object1.png';

<BackgroundImage :src="comingSoonObject1" alt="Coming Soon 1" class-modifier="absolute left-0 top-1/2 h-full max-h-[893px] -translate-y-1/2" />
```

This will apply your custom class to the component, allowing you to define specific styles.