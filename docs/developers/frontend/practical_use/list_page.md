# Listing Pages

## Introduction

Listing pages play a vital role in Vue.js applications, particularly for displaying data in an organized, searchable, and sortable manner. This guide delves into creating and configuring listing pages, with a focus on the constructors used for configuration and their practical implementation.

## Search and Listing Configurations

### Creating Search Configurations

A `searchConfigConstructor` function creates configurations for the search functionality in listing pages. It defines the search capabilities, order criteria, and filters for the data.

You can find out more about the search component [here](./../shared_utilities/components/organisms/general-search/index.md). and the user used [here](./../shared_utilities/components/organisms/general-search/filter_fields.md) 

Example of `searchConfigConstructor`:

```typescript
export const searchConfigConstructor = (t: Function): SearchConfig => ({
  search: true,
  orderKey: "sort",
  filters: [
    {
      type: FieldType.Query,
      query: companiesQuery,
      label: t('contacts.people.labels.company'),
      name: 'company',
      labelBy: "name",
      valueBy: "id",
      dataKey: "companies",
      filterable: true,
      isEdge: true,
      addExactLookup: true,
      exactLookupKeys: ['id']
    },
  ],
  orders: []
});
```

This configuration allows users to search, filter, and order the listing data based on defined criteria.

Another more complex example will be:

```typescript
export const getStatusOptions = (t) => [
  { name: t('sales.orders.labels.status.choices.draft'), code: OrderStatus.DRAFT },
  { name: t('sales.orders.labels.status.choices.pending'), code: OrderStatus.PENDING },
  { name: t('sales.orders.labels.status.choices.pendingInventory'), code: OrderStatus.PENDING_INVENTORY },
  { name: t('sales.orders.labels.status.choices.toPick'), code: OrderStatus.TO_PICK },
  { name: t('sales.orders.labels.status.choices.toShip'), code: OrderStatus.TO_SHIP },
  { name: t('sales.orders.labels.status.choices.done'), code: OrderStatus.DONE },
  { name: t('sales.orders.labels.status.choices.cancelled'), code: OrderStatus.CANCELLED },
  { name: t('sales.orders.labels.status.choices.hold'), code: OrderStatus.HOLD },
  { name: t('sales.orders.labels.status.choices.exchanged'), code: OrderStatus.EXCHANGED },
  { name: t('sales.orders.labels.status.choices.refunded'), code: OrderStatus.REFUNDED },
  { name: t('sales.orders.labels.status.choices.lost'), code: OrderStatus.LOST },
  { name: t('sales.orders.labels.status.choices.merged'), code: OrderStatus.MERGED },
  { name: t('sales.orders.labels.status.choices.damaged'), code: OrderStatus.DAMAGED },
  { name: t('sales.orders.labels.status.choices.void'), code: OrderStatus.VOID }
];

export const getReasonForSaleOptions = (t) => [
  { name: t('sales.orders.labels.reasonForSale.choices.sale'), code: ReasonForSale.SALE },
  { name: t('sales.orders.labels.reasonForSale.choices.returnGoods'), code: ReasonForSale.RETURNGOODS },
  { name: t('sales.orders.labels.reasonForSale.choices.documents'), code: ReasonForSale.DOCUMENTS },
  { name: t('sales.orders.labels.reasonForSale.choices.sample'), code: ReasonForSale.SAMPLE },
  { name: t('sales.orders.labels.reasonForSale.choices.gift'), code: ReasonForSale.GIFT }
];

export const searchConfigConstructor = (t: Function): SearchConfig => ({
  search: true,
  orderKey: "sort",
  filters: [
    {
      type: FieldType.Choice,
      name: 'status',
      label: t('sales.orders.labels.status.title'),
      labelBy: 'name',
      valueBy: 'code',
      options: getStatusOptions(t),
      addExactLookup: true
    },
    {
      type: FieldType.Choice,
      name: 'reasonForSale',
      label: t('sales.orders.labels.reasonForSale.title'),
      labelBy: 'name',
      valueBy: 'code',
      options: getReasonForSaleOptions(t),
      addExactLookup: true
    },
    {
      type: FieldType.Query,
      name: 'customer',
      label: t('contacts.people.labels.customer'),
      labelBy: 'name',
      valueBy: 'id',
      query: customersQuery,
      dataKey: 'customers',
      filterable: true,
      isEdge: true,
      addExactLookup: true,
      exactLookupKeys: ['id']
    },
  ],
  orders: [
    {
      name: 'status',
      label: t('sales.orders.labels.status.title'),
      type: OrderType.ASC
    },
    {
      name: 'status',
      label: t('sales.orders.labels.status.title'),
      type: OrderType.DESC
    },
    {
      name: 'reference',
      label: t('sales.orders.labels.reference'),
      type: OrderType.ASC
    },
    {
      name: 'reference',
      label: t('sales.orders.labels.reference'),
      type: OrderType.DESC
    }
  ]
});
```

We can see here a larger way to configure the filters including choice fields and ordering.

## Configuring the Listing

The `listingConfigConstructor` function configures how the data is listed on the page. It specifies the headers, fields, and actions available for each data item.

Example of `listingConfigConstructor`:

```typescript
export const listingConfigConstructor = (t: Function): ListingConfig => ({
  headers: [t('shared.labels.firstName'), t('shared.labels.email'), t('shared.labels.phone'), t('contacts.people.labels.company'), t('shared.placeholders.language')],
  fields: [
    { name: 'firstName', type: FieldType.Text },
    { name: 'email', type: FieldType.Email, clickable: true },
    { name: 'phone', type: FieldType.Phone, clickable: true },
    { name: 'company', type: FieldType.NestedText, keys: ['name'] },
    { name: 'language', type: FieldType.Image, basePath: '/images/flags', suffix: '.svg' }
  ],
  identifierKey: 'id',
  addActions: true,
  addEdit: true,
  editUrlName: 'contacts.people.edit',
  addShow: false,
  addDelete: true,
  addPagination: true,
  deleteMutation: deletePersonMutation,
});
```

This configuration controls the data columns, edit/delete actions, pagination, and other functionalities on the listing page.

You can find out more about the listing component [here](./../shared_utilities/components/organisms/general_listing.md) and the used fields [here](./../shared_utilities/components/organisms/general-show/show_fields.md) 

Also, regarding to the listing we can add this so we can import from a single page:

```typescript
import { peopleQuery } from "../../../shared/api/queries/contacts.js"


export const listingQueryKey = 'people';
export const listingQuery = peopleQuery;
```

After this in the Vue controller where the route is defined is as easy as it goes.

```typescript
import { useI18n } from 'vue-i18n';
import { searchConfigConstructor, listingConfigConstructor, listingQueryKey, listingQuery } from '../configs';

const { t } = useI18n();
const searchConfig = searchConfigConstructor(t);
const listingConfig = listingConfigConstructor(t);
```

```vue
<GeneralListing
  :searchConfig="searchConfig"
  :config="listingConfig"
  :query="listingQuery"
  query-key="listingQueryKey"
/>
```

## Advanced Usage: Dynamic Listing Configurations

For more complex scenarios, listing pages can dynamically adjust their configurations based on context, such as when embedded within another page (e.g., a tab in a customer details page).

### Advanced Configuration Example

Here's an advanced listingConfigConstructor that adjusts headers and fields based on whether it's filtered by a customer ID.

```typescript
const getHeaders = (t, customerId) => {
  return customerId
    ? [t('sales.orders.labels.reference'), t('shared.labels.date'), t('sales.orders.labels.status.title')]
    : [t('sales.orders.labels.reference'), t('sales.orders.labels.customer'), t('shared.labels.date'), t('sales.orders.labels.status.title')];
}

const getFields = (customerId, t): ShowField[] => {
  const commonFields: ShowField[] = [
    { name: 'reference', type: FieldType.Text },
    { name: 'createdAt', type: FieldType.Date },
    { name: 'status', type: FieldType.Badge, badgeMap: getSalesOrderStatusBadgeMap(t)},
  ];

  if (!customerId) {
    commonFields.splice(1, 0, { name: 'customer', type: FieldType.NestedText, keys: ['name'] } as NestedTextField);
  }

  return commonFields;
}

const getUrlQueryParams = (customerId: string | null = null, productId: string | null = null): Record<string, string> | undefined => {
  const params: Record<string, string> = {};

  if (customerId) {
    params.customerId = customerId;
  }
  if (productId) {
    params.productId = productId;
    params.tab = 'items';
  }
  return Object.keys(params).length > 0 ? params : undefined;
}

export const listingConfigConstructor = (t: Function, customerId: string|null = null, productId: string|null = null): ListingConfig => ({
  headers: getHeaders(t, customerId),
  fields: getFields(customerId, t),
  identifierKey: 'id',
  addActions: true,
  addEdit: !productId,
  editUrlName: 'sales.orders.edit',
  showUrlName: 'sales.orders.show',
  urlQueryParams: getUrlQueryParams(customerId, productId),
  addShow: true,
  addDelete: false,
  addPagination: true,
});
```

In fact this is not that advanced but it's a nice way to show it. So this constructor can be used in the main page but also in different tabs that show this since we control the query params and the headers and the data to exclude something if we are on a tab.