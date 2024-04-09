
# GeneralShow Field Configurations

## Overview
`GeneralShow` uses various field types, each tailored to display specific types of data. Here's a breakdown of the different field configurations available.

### ShowBaseField (Common for All Fields)
| Key             | Type        | Mandatory | Description |
|-----------------|-------------|-----------|-------------|
| `name`          | `string`    | Yes       | The attribute name in the GraphQL schema; crucial for accurate data display. |
| `icon`          | `string`    | Optional  | Icon for the field. |
| `label`         | `string`    | Optional  | User-friendly label for the field. |
| `clickable`     | `boolean`   | Optional  | If true, makes the field clickable. |
| `clickUrl`      | `Url`       | Optional  | URL to navigate to when clicked. |
| `showLabel`     | `boolean`   | Optional  | Determines whether to show the label. |
| `customCss`     | `string`    | Optional  | Custom CSS for the field. |
| `customCssClass`| `string`    | Optional  | Custom CSS class for the field. |

### TextField
Inherits `ShowBaseField`

### PhoneField
Inherits `ShowBaseField`

### EmailField
Inherits `ShowBaseField`

### WebsiteField
Inherits `ShowBaseField`

### DateField
Inherits `ShowBaseField`

### BooleanField
Inherits `ShowBaseField`

### ImageField
Inherits `ShowBaseField`

| Key       | Type      | Mandatory | Description |
|-----------|-----------|-----------|-------------|
| `basePath`| `string`  | Optional  | Base path for the image URL. |
| `suffix`  | `string`  | Optional  | Suffix to append to the image URL. |
| `alt`     | `string`  | Optional  | Alternate text for the image. |
| `width`   | `string`  | Optional  | Width of the image. |
| `height`  | `string`  | Optional  | Height of the image. |

### NestedTextField
Inherits `ShowBaseField`

| Key           | Type    | Mandatory | Description |
|---------------|---------|-----------|-------------|
| `keys`        | `string[]` | Yes   | Array of keys to access nested text values. |

### ArrayField
Inherits `ShowBaseField`

| Key               | Type              | Mandatory | Description |
|-------------------|-------------------|-----------|-------------|
| `keys`            | `string[]`        | Yes       | Array of keys to access values within an array. |
| `clickIdentifiers`| `ClickIdentifier[]` | Optional | Array of click identifier configurations for clickable elements within the array. |

#### How does the click indentifiers works?

The type is pretty straight forward like this:

`type ClickIdentifier = Record<string, string[]>;`

So it's an object with a key and as a value an array of strings. But what does it mean?

The key will represent the parameters (param) in the route objects. And the array is an array of keys to get the value from a newsted object. So if the value we want to click is more in deep of the object we can access it.

Example:

```typescript
const arrayFiled =  {
    type: FieldType.Array,
    name: 'product',
    label: t('products.title'),
    clickable: true,
    keys: ['sku'],
    showLabel: true,
    clickIdentifiers: [{id: ['id']}],
    clickUrl: {name: 'products.products.show'},
  }
```

***Good to know:*** If we have clickUrl but we don't have identifiers in the array it will try to use the clickUrl only (without params) for the URL link.

### BadgeField
Inherits `ShowBaseField`

| Key       | Type                | Mandatory | Description |
|-----------|---------------------|-----------|-------------|
| `badgeMap`| `Record<string, Badge>` | Yes   | Mapping of badge text to its visual representation. |

#### How does the click badgeMap works?

The type looks like this:

```typescript
export interface Badge {
  text: string;
  color: string;
}
```

As you can see in the [badge component](./../../atoms/badge.md) the badge need a text and a color. So when we build the badgeMap we will need the:

- key as the value come from the backend. ex: VARIATION
- text as a user-friendly translatable text
- colo one supported color for the badge

## Features
- **Diverse Field Types**: Supports various data representations, from basic text to complex nested structures.
- **Customization Options**: Each field type offers customization options like custom CSS, labels, and click actions.
- **Interactive Elements**: Certain fields can be made clickable, navigating to specific URLs.

## Usage
`GeneralShow` is used to create detailed, visually appealing displays of data, with each field type adding a unique aspect to the overall presentation. 