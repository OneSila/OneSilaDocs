
# Auth Module

## Overview
The `Auth` module in Vue applications handles user authentication and session management. It provides a structured way to manage user data and authentication states across the application.

## Features
- User Authentication: Manages user login states and user-specific data.
- Session Handling: Keeps track of the user's session for a seamless experience.
- User Data Management: Maintains and updates user-related information such as language, company association, and active status.

## Implementation Details
- The module utilizes Vue's reactive system to update and manage user state.
- It interfaces with GraphQL for backend communication.
- User data is stored in the local storage for persistent sessions.

## Key Functions
- `createAuth`: Initializes the auth state.
- `refreshUser`: Updates the user data and authentication state.
- `setCompanyToUser`: Associates a company with the user.
- `setLanguageToUser`: Sets the user's preferred language.
- `replaceAuth`: Replaces the current auth state with a new user.
- `removeAuth`: Handles user logout and cleans up the session.
- `isAuthenticated`: Checks if the user is authenticated.
- `hasCompany`: Checks if the user is associated with a company.
- `isCompanyOwner`: Checks if the user is the owner of the company.
- `isActive`: Checks if the user's account is active.
- `injectAuth`: Provides access to the auth state throughout the application.

The `Auth` module plays a crucial role in managing user-related functionalities, making it an essential part of any Vue application that requires user authentication.