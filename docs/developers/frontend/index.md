# Getting Started with OneSila Frontend

Welcome to the OneSila Frontend documentation! This guide is designed to help you set up and understand the OneSila Frontend, which works in tandem with the OneSila Headless ERP system. 

In addition to basic setup instructions, this guide will provide an overview of the project structure, making it easier for you to navigate and utilize the various components and features of the application. Whether you are looking to contribute to the project or simply want to get it up and running, the following sections will assist you in getting started.

## Prerequisites

Before you start, ensure you have the following prerequisites installed on your system:

- [Node.js and npm](https://nodejs.org/en/download/) (Node.js 14.x or later)
- [Git](https://git-scm.com/downloads) for cloning the repository
- OneSila Headless Backend (follow the setup instructions in its [repository](https://github.com/OneSila/OneSilaHeadless))

## Technology Stack Overview

The OneSila Frontend is built using a modern technology stack to ensure efficiency, scalability, and ease of use. Key technologies include:

- **Vue 3**: A progressive JavaScript framework used for building user interfaces.
- **Tailwind CSS 3.3.3**: A utility-first CSS framework for rapidly building custom designs.
- **Apollo Client**: A comprehensive state management library for JavaScript that enables you to manage both local and remote data with GraphQL.
- **TypeScript**: A typed superset of JavaScript that compiles to plain JavaScript, used for adding type safety to the code.

These technologies have been chosen for their robustness and the rich ecosystem they provide, allowing for the creation of a flexible and maintainable frontend architecture.

## Setup

1. Open a terminal.
2. Clone the OneSila Frontend repository using Git:

    ```bash
    git clone https://github.com/OneSila/OneSilaFrontend.git
    ```

3. Navigate to the cloned directory:

    ```bash
    cd OneSilaFrontend
    ```

4. Install the necessary dependencies:

```bash
npm install
```

## Running the Application

To run the application locally, you need to start both the frontend and the backend services.

### Starting the Backend

1. Ensure you have set up the OneSila Headless Backend. Refer to its [repository](https://github.com/OneSila/OneSilaHeadless) for instructions.
2. Run the backend service:

```bash
./manage.py runserver localhost:8080
```

### Starting the Frontend

1. In a new terminal window, navigate to the OneSila Frontend director
2. Run the following command to start the frontend service:

```bash
VITE_APP_API_GRAPHQL_URL="http://localhost:8080/graphql/" VITE_APP_API_GRAPHQL_WEBSOCKET_URL="ws://localhost:8080/graphql/" npm run dev
```


## Understanding the Project Structure

The OneSila Frontend project has a structured directory layout for easy navigation and development:

- `assets`: Contains image assets used across the application.
- `core`: Core functionalities and business logic of the application.
- `locale`: Localization files for supporting multiple languages.
- [`shared`](./shared_utilities/index.md): Shared utilities, API integration, and common components.
- [`utils`](./utils.md): Utility functions and constants.

Refer to the project's directory for a more detailed view of the structure.


## Shared Directory Overview

The `shared` directory is a crucial part of the OneSila Frontend project, organizing common functionalities, components, and utilities used across the application. Here's a brief overview of its structure and purpose:

### [API](./api.md)
This subdirectory contains GraphQL queries, mutations, and subscriptions, organized by their use cases such as authentication, contacts, currencies, etc.

#### Mutations
Contains `.js` files for GraphQL mutations, allowing modifications to data.

#### Queries
Holds `.js` files for GraphQL queries to fetch data.

#### Subscriptions
Contains `.js` files for GraphQL subscriptions, enabling real-time data updates.

### [Components](./shared_utilities/components/index.md)
A collection of Vue components categorized into atoms, molecules, layouts, and organisms, providing a wide range of UI elements for the application.

#### [Atoms](./shared_utilities/components/atoms/index.md)
Basic building blocks of the UI such as buttons, checkboxes, icons, etc., each with their own directory and `.vue` files.

#### [Molecules](./shared_utilities/components/molecules/index.md)
More complex UI components that combine atoms, such as `ApolloAlertMutation.vue` for GraphQL mutations with alert feedback, `Breadcrumbs.vue` for navigation, and more.

#### [Layouts](./shared_utilities/components/layouts/index.md)
Contains layout components for organizing content, such as `Flex.vue` and `Grid.vue`.

#### [Organisms](./shared_utilities/components/organisms/index.md)
Complex components composed of molecules and atoms, acting as complete sections or functionality blocks within the application. Examples include `GeneralForm.vue` for generic form.

### [Modules](./shared_utilities/modules/index.md)
JavaScript modules providing various functionalities like authentication handling (`auth`), device information (`device`), network status (`network`), etc.

### [Plugins](./shared_utilities/plugins/index.md)
Vue plugins to extend the functionality of the application, like `font-awesome.ts` for icons, `i18n.ts` for internationalization, and `router.ts` for routing.

### Templates
Contains general Vue templates like `GeneralTemplate.vue` used across different parts of the application.

### Theme
Holds CSS and styling-related files for the application's theme, categorized under the `default` theme directory. Files include general CSS (`app.css`), component-specific styles like `datatable.css`, and utility styles like `animate.css`.

### [Utils](./utils.md)
Utility functions and constants used throughout the application, such as `constants.ts` for application-wide constants.