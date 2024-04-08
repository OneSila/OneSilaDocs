
# Utilities Overview

The `utils` directory in the OneSila Frontend project consists of two primary files: `constants.ts` and `index.ts`. These files contain essential constants and utility functions used across the application, promoting code reusability and maintaining standard practices.

## constants.ts

This file stores a collection of constant values and enums, providing a centralized definition for various aspects of the application. Notable constants include:

- **`PUBLIC_ROUTES`**: Array of public route names.
- **`DEFAULT_LANGUAGE`**: Default language setting.
- **`Url` Interface**: Structure for URL objects.
- **`FieldType` Enum**: Defines types of form fields.
- **`OrderStatus` & `ReasonForSale` Enums**: Enums for order statuses and sale reasons.
- **`ProductType` Enum**: Enum for product types (Variation, Bundle, Umbrella).

## index.ts

This file offers a suite of utility functions that support various functionalities in the application:

- **`isIframe`**: Checks if running in an iframe.
- **`useStringifyActiveStatus`**: Vue composition function for active status representation.
- **`slugify`**: Generates URL-friendly strings.
- **`flipBoolean` & `booleanify`**: Manages and interprets boolean values.
- **`getLength`**: Safely determines the length of an array.
- **`booleanifyIfNeeded` & `booleanSelectify`**: Handles boolean values in form inputs.
- **`truncate`**: Shortens a string with an ellipsis.
- **`getSelectedOrderIndex`**: Determines index of a selected order based on route query.
- **`dataImageToBlob`**: Converts base64 encoded images to Blob objects.
- **`getFlagImageSrc` & `getSrcImage`**: Retrieves image sources for flags and assets.
- **`matchComplexError` & `processGraphQLErrors`**: Handles and parses GraphQL error responses.