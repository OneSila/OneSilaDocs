# Inventory

## Inventory Movement Query

Due to the nature of generic relations, and how we implement them. You must use inline fragments.  

Query sample:

```graphql
query inventoryMovements{
  inventoryMovements{
    edges{
      node {
        __typename
        movementFrom {
          ... on InventoryType {
            id
          }
          ... on PurchaseOrderType {
            id
          }
        }
        movementTo {
          ... on InventoryType {
            id
          }
          ... on PackageType {
            id
          }
        }
      }
    }
  }
}
```

Reponse sample:

```
{
  "data": {
    "inventoryMovements": {
      "edges": [
        {
          "node": {
            "__typename": "InventoryMovementType",
            "movementFrom": {
              "id": "SW52ZW50b3J5VHlwZToxMDA="
            },
            "movementTo": {
              "id": "SW52ZW50b3J5VHlwZToxMDA="
            }
          }
        }
      ]
    }
  }
}
```

## Inventory Movement Create

Mutation example

```graphql
    mutation createInventoryMovement($data: InventoryMovementInput!){
      createInventoryMovement(data: $data){
        quantity
        notes
        product {
          id
        }
        movementFrom {
            ... on InventoryType {
                id
            }
            ... on PurchaseOrderType {
                id
            }
        }
        movementTo {
            ... on InventoryType {
                id
            }
            ... on PackageType {
                id
          }
        }
      }
    }
```

Where `InventoryMovementInput` looks like:

```python
{
  'data': {
    'product': {'id': supplier_prod_id},  # GlobalID
    'quantity': 5,
    'movementToId': inv_id,
    'movementFromId': inv_bis_id
  }
}
```