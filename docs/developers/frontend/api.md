
# API Folder

The `api` directory in the OneSila Frontend project is a centralized location for all GraphQL queries, mutations, and subscriptions. This structure provides a modular and organized approach to handling data operations.

## Overview
- **Mutations**: Used to modify data (e.g., creating, updating, deleting records).
- **Queries**: Fetch data from the server.
- **Subscriptions**: Real-time data updates through WebSocket connections.

### Mutations
Mutations in GraphQL are used to create, update, or delete data. Here's an example of a mutation used to create a new company:

```javascript
import { gql } from 'graphql-tag';

export const createCompanyMutation = gql`
mutation createCompany($data: CompanyInput!) {
  createCompany(data: $data){
    id
    name
    eoriNumber
    vatNumber
  }
}
`;
```

This mutation, `createCompanyMutation`, takes a `CompanyInput` object and creates a new company record. The response includes fields like `id`, `name`, `eoriNumber`, and `vatNumber`.

### Queries
Queries are used to fetch data. Here's an example of a query to fetch companies:

```javascript
import { gql } from 'graphql-tag';

export const companiesQuery = gql`
query Companies($first: Int, $last: Int, $after: String, $before: String, $order: CompanyOrder, $filter: CompanyFilter) {
  companies(first: $first, last: $last, after: $after, before: $before, order: $order, filters: $filter) {
    edges {
      node {
        id
        name
        eoriNumber
        vatNumber
      }
      cursor
    }
    totalCount
    pageInfo {
      endCursor
      startCursor
      hasNextPage
      hasPreviousPage
    }
  }
}
`;
```

The `companiesQuery` fetches a list of companies with pagination and filtering capabilities. The response is paginated (`edges`, `pageInfo`) and includes details for each company.

### Subscriptions
Subscriptions provide real-time updates via a WebSocket connection. Here's an example subscription for a company:

```javascript
import { gql } from 'graphql-tag';

export const getCompanySubscription = gql`
subscription getCompany ($id: String!) {
  company(pk: $id) {
    id
    name
    isSupplier
    vatNumber
    eoriNumber
    isSupplier
    isCustomer
    isInternalCompany
    isInfluencer
    relatedCompanies {
      id
      name
    }
  }
}`;
```

This subscription, `getCompanySubscription`, listens for real-time updates to a company specified by `id`. It provides the latest information about the company whenever any changes occur.

## Usage in Components
These API functions are integrated into Vue components, where they are used to fetch, display, and manipulate data dynamically. For example, a component might use `companiesQuery` to display a list of companies or `createCompanyMutation` to add a new company to the database.

---
This modular approach to handling API calls keeps the codebase clean, organized, and easy to maintain. Each API operation is defined in its dedicated file, making it straightforward to locate and update specific GraphQL operations.