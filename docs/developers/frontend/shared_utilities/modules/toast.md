
# Toast Module Overview

## Description
The Toast module provides a convenient way to display brief, auto-dismissing messages or alerts in a Vue.js application.

## Key Features
- **Customizable Toasts**: Supports different types like info, success, warning, and error.
- **Auto-dismiss**: Toasts automatically disappear after a set duration.
- **Interactive**: Users can pause the timer by hovering over the toast.

## Usage
Use the Toast module to display notifications or alerts to the user, especially for asynchronous operations' status like API requests.

## Example
```typescript
import { Toast } from './toastModule';

// Display an information toast
Toast.info('Information message');

// Display a success toast
Toast.success('Success message');

// Display an error toast
Toast.error('Error message');

// Display a warning toast
Toast.warning('Warning message');
```