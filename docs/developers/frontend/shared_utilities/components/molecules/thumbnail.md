
# Thumbnail Component

## Overview
The `Thumbnail.vue` component displays an image thumbnail. It can also show an icon when no image link is provided.

## Properties
- `link`: URL of the image to display.
- `width`: Width of the thumbnail. If not provided, it defaults to full width.
- `compact`: Boolean indicating whether to use the compact styling.

## Usage
```vue
<template>
  <Thumbnail :link="imageUrl" :width="64" :compact="true" />
</template>
```
