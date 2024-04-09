
# Screen Module Overview

## Description
The Screen module provides information about the screen dimensions and assists in responsive design for Vue.js applications.

## Key Features
- **Screen Size Detection**: Determines the width and height of the screen.
- **Device Type Checks**: Functions to check if the device is mobile, tablet, or desktop based on screen width.

## Usage
Use the module to adapt the application's layout and behavior according to the user's screen size.

## Example
```typescript
import { detectScreen, isMobile, isTablet, isDesktop } from './screenModule';

const screen = detectScreen();

console.log('Is Mobile:', isMobile(screen));
console.log('Is Tablet:', isTablet(screen));
console.log('Is Desktop:', isDesktop(screen));
```