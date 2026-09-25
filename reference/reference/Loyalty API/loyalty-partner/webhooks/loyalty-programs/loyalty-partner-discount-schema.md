---
title: Loyalty Discounts Schema
excerpt: Loyalty Discount Schemas And Examples
deprecated: false
hidden: false
metadata:
  robots: index
---
To provide flexibility and accommodate varying types of discounts, we have modelled different types of variances in the discount by explicitly declaring what the scope and the offer of the discount is.

**Offer:** the type of the offer. Currently, we have a percentage and a flat amount.
**Scope:** the scope to which the offer applies. Currently, we have an order and an item. But it could be easily extended to products, categories, or event charges, such as a delivery fee, which is a common discount.

#### Discount Schema Fields

| Field      | Type   | Description                                                                   |
| :--------- | :----- | :---------------------------------------------------------------------------- |
| provider   | string | The source of the discount. For this API, the value will always be "loyalty". |
| externalId | string | The unique ID of the discount in the loyalty provider system.                 |
| offer      | object | An object that describes the type and value of the discount.                  |
| scope      | object | An object that defines where the discount applies.                            |

## Discount Offer Types

The offer field describes the specific type of discount and its value. Its structure changes based on the value of the type field. This flexible design allows the system to support a wide range of promotions, from simple flat amounts to fixed prices and free items.

<br />

### 1. Flat Off Offer

**Type:** `"flat_off"`

This offer provides a fixed amount discount.

| Field   | Type     | Description                                                                              |
| :------ | :------- | :--------------------------------------------------------------------------------------- |
| `type`  | `string` | The fixed value `"flat_off"`.                                                            |
| `value` | `number` | The discount amount in the smallest currency unit (e.g., $2.00 is represented as `200`). |

<br />

### 2. Percent Off Offer

**Type:** `"percent_off"`

This offer provides a percentage-based discount.

| Field   | Type     | Description                                                                        |
| :------ | :------- | :--------------------------------------------------------------------------------- |
| `type`  | `string` | The fixed value `"percent_off"`.                                                   |
| `value` | `number` | The discount percentage multiplied by 100 (e.g., 20.50% is represented as `2050`). |

<br />

### 3. Fixed Amount Offer

**Type:** `"fixed_amount"`

This offer sets the price of a specific item to a fixed value, regardless of its original price.

| Field   | Type     | Description                                                    |
| :------ | :------- | :------------------------------------------------------------- |
| `type`  | `string` | The fixed value `"fixed_amount"`.                              |
| `value` | `number` | The new fixed price of the item in the smallest currency unit. |

<br />

### 4. Free Offer

**Type:** `"free"`

This offer indicates that the target item is free. This is used for "Buy One, Get One Free" or "Free Item" discounts.

| Field  | Type     | Description               |
| :----- | :------- | :------------------------ |
| `type` | `string` | The fixed value `"free"`. |

***

## Discount Scope Types

The scope field defines where the discount applies within an order. Its structure changes based on the value of the type field. This allows a single discount object to be targeted to the entire order, a specific item, or a particular product.

<br />

### 1. Order Scope

**Type:** `"order"`

This scope indicates that the discount applies to the entire order.

| Field  | Type     | Description                |
| :----- | :------- | :------------------------- |
| `type` | `string` | The fixed value `"order"`. |

<br />

### 2. Item Scope

**Type:** `"item"`

This scope indicates that the discount applies to a specific line item in the order's basket.

| Field       | Type     | Description                                                    |
| :---------- | :------- | :------------------------------------------------------------- |
| `type`      | `string` | The fixed value `"item"`.                                      |
| `lineIndex` | `number` | The zero-based index of the item in the order's `items` array. |

<br />

### 3. Product Scope

**Type:** `"product"`

This scope indicates that the discount applies to products not in the basket.

| Field      | Type               | Description                                                                                                                                                                                          |
| :--------- | :----------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `type`     | `string`           | The fixed value `"product"`.                                                                                                                                                                         |
| `plu`      | `string`           | The PLU (Product Look-Up) of the item to which the discount applies.                                                                                                                                 |
| `quantity` | `number` or `null` | The number of products the discount affects. If `null`, the discount applies to all units of the product in the order. This field is required to be present, either with a number or a `null` value. |

<br />

## Examples

The following examples illustrate how the combination of a scope and offer can be used to create common discounts.

### Order flat off

```json
{
    "provider": "loyalty",
    "externalId": "1",
    "offer": {
        "type": "flat_off",
        "value": 500
    },
    "scope": {
        "type": "order"
    }
}
```

### Order percent

```json
{
    "provider": "loyalty",
    "externalId": "1",
    "offer": {
        "type": "percent_off",
        "value": 5050 // 50.50%
    },
    "scope": {
        "type": "order"
    }
}
```

### Item flat off

```json
{
    "provider": "loyalty",
    "externalId": "program_123",
    "offer": {
        "type": "flat_off",
        "value": 200
    },
    "scope": {
        "type": "item",
        "lineIndex": 1
    }
}
```

### Item percent off

```json
{
    "provider": "loyalty",
    "externalId": "program_123",
    "offer": {
        "type": "percent_off",
        "value": 3033 // 30.33%
    },
    "scope": {
        "type": "item",
        "lineIndex": 1
    }
}
```

### Item fixed price

```json
{
    "provider": "loyalty",
    "externalId": "program_123",
    "offer": {
        "type": "fixed_amount",
        "value": 200
    },
    "scope": {
        "type": "item",
        "lineIndex": 1
    }
}
```

### Free items

```json
{
    "provider": "loyalty",
    "externalId": "program_123",
    "offer": {
        "type": "free",
        "quantity": 1
    },
    "scope": {
        "type": "product",
        "plu": "abc123"
    }
}
```
