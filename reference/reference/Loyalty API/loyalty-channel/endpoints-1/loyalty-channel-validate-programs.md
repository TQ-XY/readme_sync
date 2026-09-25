---
api:
  file: loyalty-api.json
  operationId: post_new-endpoint
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
## Purpose

To validate a customer's selected loyalty program against their current order and return the final, machine-readable discount details for the channel to apply to the basket. The loyalty provider validates the selected program using its internal business rules, and it's important to note that a single loyalty program may result in multiple discounts being applied to the order.

When to Use:

- When a customer selects a loyalty program to add to their basket.
- Before the customer proceeds to payment, to ensure all discounts are correctly applied.

### Internal Logic for Program Application:

**Program Availability Verification:** The system contacts the loyalty provider to confirm if the selected programs are applicable to the provided basket. The provider is responsible for validating the program's availability and business rules.

**Handling Already Applied Programs:** If a program has already been applied (and is present in the order's discounts payload), the system will revalidate it without adding any new discounts. This prevents application errors but also confirms the program is still valid for the current order state.

**Important Note:** The endpoint does not validate the correctness of the discounts that are already present in the order payload.

## Endpoint Details

**Request Payload:**<br />The request includes the list of programIds to be validated and the complete order payload.

This schema defines the complete request body sent to the wallet validation webhook.

| Field        | Type               | Required | Description                                                                                              |
| :----------- | :----------------- | :------- | :------------------------------------------------------------------------------------------------------- |
| `sessionId`  | `string`           | No       | A unique **session token** linking all related loyalty actions (e.g., retrieve, validate, create order). |
| `order`      | `object`           | Yes      | See **Order schema**[ 🔗](https://developers.deliverect.com/page/channel-orders)                         |
| `programIds` | `array of strings` | Yes      | A list of program Ids that the customer has selected to apply to their basket.                           |

Example Request:

```json
{
  "sessionId": "TEST1741193909",
  "programIds": [
    "1"
  ],
  "order": {
    "items": [
      {
        "plu": "1324882025",
        "name": "Coke",
        "price": 500,
        "quantity": 2
      }
    ],
    "customer": {
      "email": "john.doe@test.com",
      "phoneNumber": "+32121212121",
      "loyaltyProviderCustomerId": "abc123"
    },
    "decimalDigits": 0,
    "deliveryCost": 0,
    "serviceCharge": 0,
    "orderType": 1,
    "tip": 0
  }
}
```

<br />

### Response Schema and Structure

The programs/validate endpoint is transitioning to a new response schema designed for improved flexibility and scalability. This new structure cleanly separates validation results from discount details and standardises how different discount types are represented.

**Field Deprecation**

We are actively deprecating a number of fields from our previous schema. During a transition period, the API will return a Transitional Response that includes both the deprecated and new fields to ensure backwards compatibility. In a future update, all deprecated fields will be entirely removed.

#### Response Schema Details

| Field              | Type                | Nullable | Default Value      | Deprecated | Description                                                                                                                                                                                                                             |
| :----------------- | :------------------ | :------- | :----------------- | :--------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `programId`        | `string`            | No       | Required           | No         | The unique identifier of the loyalty program that was validated.                                                                                                                                                                        |
| `validationError`  | `object`            | Yes      | `null`             | **Yes**    | The legacy object for validation errors. Replaced by the `validationErrors` array.                                                                                                                                                      |
| `validationErrors` | `array of objects`  | No       | `[]` (empty array) | No         | A list of errors. Each object in the array contains a `message` string explaining the failure. This array is empty on successful validation.                                                                                            |
| `discounts`        | `array of objects`  | No       | `[]` (empty array) | No         | A list of validated discount objects to be applied to the order. Empty if validation fails or if the program has already been applied. See **Discount Schema page**[ 🔗](https://developers.deliverect.com/reference/loyalty-discounts) |
| `title`            | `string`            | No       | Required           | **Yes**    | The display name of the program. This information should be retrieved from the program discovery endpoint (`/programs/retrieve`).                                                                                                       |
| `type`             | `string`            | No       | Required           | **Yes**    | The legacy type of the discount. This has been replaced by the `offer` and `scope` fields within the new `discounts` objects.                                                                                                           |
| `applicable`       | `boolean`           | No       | `true`             | **Yes**    | Indicates if the customer meets the basic requirements for the program to be applied. The new schema indicates validity by the presence of a response object in the validation endpoint.                                                |
| `description`      | `string`            | Yes      | `null`             | **Yes**    | A description of the program. This information should be retrieved from the program discovery endpoint.                                                                                                                                 |
| `cost`             | `number`            | Yes      | `null`             | **Yes**    | The loyalty cost of the program. This is a program-level detail and is no longer included in the validation response.                                                                                                                   |
| `media`            | `object`            | Yes      | `null`             | **Yes**    | Display-related media assets. This information should be retrieved from the program discovery endpoint.                                                                                                                                 |
| `expiresAt`        | `string` (ISO 8601) | Yes      | `null`             | **Yes**    | Program expiration details. This information should be retrieved from the program discovery endpoint.                                                                                                                                   |
| `discount`         | `number`            | Yes      | `null`             | **Yes**    | The specific amount of the discount. This has been replaced by the `value` field within the new `discounts.offer` object.                                                                                                               |
| `itemPLU`          | `string`            | Yes      | `null`             | **Yes**    | The PLU of the discounted item. This has been replaced by the `plu` field within the new `discounts.scope` object.                                                                                                                      |
| `quantity`         | `number`            | Yes      | `null`             | **Yes**    | The quantity of items affected. This is now a field within the new `discounts.offer` or `discounts.scope` objects, depending on the discount type.                                                                                      |
| `minOrderValue`    | `number`            | Yes      | `null`             | **Yes**    | A business rule condition. This is now handled by the loyalty provider's internal logic and will be removed from the validation response.                                                                                               |

<br />

#### Discount Type Translation Table (Legacy to New):

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Loyalty (Legacy)
      </th>

      <th>
        Loyalty (New)
      </th>

      <th>
        Commerce / Order API Types
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        `discount_amount`
      </td>

      <td>
        - Scope: `order`
        - Offer: `flat_off`
      </td>

      <td>
        `order_flat_off`
      </td>
    </tr>

    <tr>
      <td>
        `discount_percentage`
      </td>

      <td>
        - Scope: `order`
        - Offer: `percent_off`
      </td>

      <td>
        `order_percent_off`
      </td>
    </tr>

    <tr>
      <td>
        `free_item`
      </td>

      <td>
        - Scope: `product`
        - Offer: `free`
      </td>

      <td>
        `item_free`
      </td>
    </tr>

    <tr>
      <td>
        `buy_one_get_one_free`
      </td>

      <td>
        - Scope: `item`
        - Offer: `free`
      </td>

      <td>
        `item_bogof`
      </td>
    </tr>

    <tr>
      <td>
        item_discount_amount
      </td>

      <td>
        - Scope: `item`
        - Offer: `flat_off`
      </td>

      <td>
        `item_flat_off`
      </td>
    </tr>

    <tr>
      <td>
        item_discount_percentage
      </td>

      <td>
        - Scope: `item`
        - Offer: `percent_off`
      </td>

      <td>
        `item_percent_off`
      </td>
    </tr>

    <tr>
      <td>
        `item_fixed_price`
      </td>

      <td>
        - Scope: `item`
        - Offer: `fixed_amount`
      </td>

      <td>
        N/A
      </td>
    </tr>
  </tbody>
</Table>

<br />

### Example Responses

#### Current Response (Deprecated)

This is the legacy response schema. It is still returned for backwards compatibility but should be considered deprecated.

Example Response:

```json
[
  {
    "programId": "1",
    "title": "$2 OFF",
    "type": "discount_amount",
    "applicable": true,
    "description": "",
    "cost": 10,
    "media": { ... },
    "expiresAt": null,
    "discount": 200,
    "itemPLU": null,
    "quantity": null,
    "minOrderValue": 1000,
    "validationError": {
      "message": "test"
    }
  }
]
```

<br />

#### Transition Response

This response is provided during the transition period to ensure a seamless migration for clients. It includes both the deprecated fields from the legacy schema and the new, definitive discounts array. This allows clients to update their integrations to the new schema without breaking existing functionality.

Example Response:

```json
[
    {
        "programId": "1",
        "title": "$2 OFF",
        "type": "discount_amount",
        "applicable": true,
        "description": "",
        "cost": 10,
        "media": {},
        "expiresAt": null,
        "discount": 200,
        "itemPLU": null,
        "quantity": null,
        "minOrderValue": 1000,
        "validationErrors": [
            {
                "message": "test"
            }
        ],
        "validationError": {
            "message": "test"
        },
        "discounts": [
            {
                "provider": "loyalty",
                "externalId": "program_123",
                "offer": {
                    "type": "flat_off",
                    "value": 200
                },
                "scope": {
                    "type": "order"
                }
            }
        ]
    }
]
```

<br />

#### Future Response (New)

This is the new, recommended response schema. It provides a clear and consistent structure for all discount types. It contains only the essential, machine-readable information required to apply a discount to an order.

Example Response:

```json
[
  {
    "programId": "1",
    "validationErrors": [],
    "discounts": [
      {
        "provider": "loyalty",
        "externalId": "program_123",
        "offer": {
          "type": "flat_off",
          "value": 200
        },
        "scope": {
          "type": "order"
        }
      }
    ]
  }
]
```

<br />

### Program Revalidation

The validation endpoint supports revalidation, where the initial call will return a new discount, but subsequent calls will not. This is crucial for managing the order lifecycle.

Scenario: A channel first validates two programs (order_flat_off_123 and free_item_123) when the basket is empty.

Request Payload (First Call):

```json
{
  "programIds": [
    "order_flat_off_123",
    "free_item_123"
  ],
  "order": {
    "items": [
      {
        "plu": "P-CO-7TbZ-2",
        "name": "Cola",
        "quantity": 3,
        "price": 500,
        "discountReferenceIds": []
      }
    ],
    "discounts": []
  }
}
```

API Response:

```json
[
  {
    "programId": "order_discount_123",
    "validationErrors": [],
    "discounts": [
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
    ]
  },
  {
    "programId": "free_item_123",
    "validationErrors": [],
    "discounts": [
      {
        "provider": "loyalty",
        "externalId": "1",
        "offer": {
          "type": "free"
        },
        "scope": {
          "type": "product"
        }
      }
    ]
  }
]
```

Scenario: The channel applies the first two discounts to the basket and then adds a new program (new_program_item_discount). The new validation request includes all three program IDs.

Request Payload (Revalidation Call):

```json
{
  "programIds": [
    "order_flat_off_123",
    "free_item_123",
    "new_program_item_discount"
  ],
  "order": {
    "items": [
      {
        "plu": "P-CO-7TbZ-2",
        "name": "Cola",
        "quantity": 3,
        "price": 500,
        "discountReferenceIds": [2]
      },
      {
        "plu": "P-CO-7TbZ-2",
        "name": "Cola",
        "quantity": 1,
        "price": 500,
        "discountReferenceIds": [1]
      }
    ],
    "discounts": [
      {
        "type": "item_free",
        "provider": "loyalty",
        "name": "Free",
        "referenceId": 1,
        "value": 500,
        "amount": 500,
        "programId": "free_item_123"
      },
      {
        "type": "order_flat_off",
        "provider": "loyalty",
        "name": "5$ off",
        "referenceId": 2,
        "value": 500,
        "amount": 500,
        "programId": "order_discount_123"
      }
    ]
  }
}
```

API Response:

```json
[
  {
    "programId": "order_discount_123",
    "validationErrors": [],
    "discounts": []
  },
  {
    "programId": "free_item_123",
    "validationErrors": [],
    "discounts": []
  },
  {
    "programId": "new_program_item_discount",
    "validationErrors": [],
    "discounts": [
      {
        "provider": "loyalty",
        "externalId": "1",
        "offer": {
          "type": "flat_off",
          "value": 500
        },
        "scope": {
          "type": "item",
          "lineIndex": 1
        }
      }
    ]
  }
]
```

<br />

### Program Removal

Some loyalty providers may place a temporary lock on a program once it is validated, as a measure for fraud prevention. If a customer selects a program and then decides to remove it from their basket, the channel must call the validation endpoint to signal this removal and release the lock.

To remove a program, the channel should:

1. **Remove the program's ID** from the `programIds` array in the request payload.
2. **Include the program's discount details** in the `order.discounts` payload to explicitly signal its removal from the validation context.

This process informs the loyalty provider that the program is no longer in use, allowing it to be made available to the customer again.

**Example: Removing a Program from the Basket**

In this example, the customer is removing the program with the ID `free_item_123`. The `order_flat_off_123` program remains selected.

```json
{
  "programIds": [
    "order_flat_off_123",
  ],
  "order": {
    "items": [
      {
        "plu": "P-CO-7TbZ-2",
        "name": "Cola",
        "quantity": 3,
        "price": 500,
        "discountReferenceIds": [2]
      },
      {
        "plu": "P-CO-7TbZ-2",
        "name": "Cola",
        "quantity": 1,
        "price": 500,
        "discountReferenceIds": [1]
      }
    ],
    "discounts": [
      {
        "type": "item_free",
        "provider": "loyalty",
        "name": "Free",
        "referenceId": 1,
        "value": 500,
        "amount": 500,
        "programId": "free_item_123"
      },
      {
        "type": "order_flat_off",
        "provider": "loyalty",
        "name": "5$ off",
        "referenceId": 2,
        "value": 500,
        "amount": 500,
        "programId": "order_discount_123"
      }
    ]
  }
}
```

**Expected Response:**
The response will only include a validation object for the programs that remain selected (order_flat_off_123). The response for the removed program (free_item_123) will not be returned.

```json
[
  {
    "programId": "order_discount_123",
    "validationErrors": [],
    "discounts": []
  }
]
```

<br />