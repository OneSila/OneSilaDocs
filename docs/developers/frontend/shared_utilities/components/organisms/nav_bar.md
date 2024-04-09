
# SideBar Overview

## Description
The `SideBar` component is a key part of the navigation in Vue.js applications. It provides a vertical navigation menu that includes links to different sections of the application. This component enhances the user experience by offering easy and organized access to various functionalities.

## Features and Functionality
- **Navigation Links**: The `SideBar` contains links to various sections of the application like contacts, products, inventory, sales, and more.
- **Collapsible Sub-menus**: Each main menu item can have a collapsible sub-menu, making it easier to organize and navigate through different subsections.
- **Settings Section**: A dedicated section for settings related to different functionalities of the application.
- **Dynamic Activation**: The active state of the navigation links updates dynamically based on the current route.

## Internal Components
- **Icon**: Used for displaying icons alongside menu items.
- **Link**: Navigation component to different sections of the application.
- **VueCollapsible**: A Vue component used to create collapsible sub-menus.

## Navigation Items Configuration (`navItems.ts`)
The navigation items and their structure are defined in the `navItems.ts` file. This file exports the navigation sections and items, making it easy to update and add new menu items.

### Example Configuration:
```typescript
export const navSections: NavSection[] = [
  {
    items: [
      {
        title: 'contacts.title',
        icon: 'envelope',
        subItemsKey: 'contacts',
        subItems: [
          {
            route: { name: 'contacts.companies.list' },
            title: 'contacts.companies.title'
          },
          // Other sub-items...
        ]
      },
      // Other main items...
    ]
  }
];

export const settingsSection: NavSection = {
  // Settings items configuration...
};
```

## Usage in Templates
In the Vue component templates, `SideBar` is used as part of the main layout, usually in combination with the header and content sections.

### Example Usage in Template:
```vue
<SideBar :sidebar="sidebar" @hide-sidebar="toggleSidebar()" />
```

This structure allows for a consistent and efficient navigation experience across different parts of the application.