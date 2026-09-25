---
api:
  file: loyalty-api.json
  operationId: post_loyalty-channellinkid-compensationcards-validate
hidden: false
link:
  new_tab: false
metadata:
  robots: index
next:
  pages:
    - slug: endpoints-1
      title: Endpoints
      type: endpoint
---
## Purpose

This endpoint allows partners to validate one or more compensation cards against a specific order/basket. It determines if a card is applicable, calculates the associated discounts, or identifies specific validation errors (e.g., expired, invalid).

## **Request Schema**

| Field                 | Type          | Required | Description                                                                                                                                                                           |
| --------------------- | ------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `sessionId`           | String        | Yes      | A unique identifier for the session. Required for some integrations to track card validation and subsequent redemption.                                                               |
| `compensationCardIds` | List\[String] | Yes      | A list of compensation card codes to be validated.                                                                                                                                    |
| `order`               | Object        | Yes      | The complete order/basket object to validate the cards against. For more details, see the [Channel Order Model Documentation](https://developers.deliverect.com/page/channel-orders). |

###

## **Response Schema**

The response is a **list of objects**, where each object represents the validation result for a specific card.

| Field                | Type           | Description                                                                    |
| -------------------- | -------------- | ------------------------------------------------------------------------------ |
| `compensationCardId` | String         | The unique code of the card (matches the request).                             |
| `expiresAt`          | ISO8601 String | The expiration date/time of the card.                                          |
| `validationErrors`   | List\[Object]  | A list of errors if the card is not applicable. Contains `code` and `message`. |
| `discounts`          | List\[Object]  | A list of applicable discounts derived from the card.                          |

## **Functional Scenarios**

### **Case 1: Adding a New Compensation Card**

This occurs when a user enters a new card code. The `order` object does not yet contain discounts for this card.

**Success (Applicable):** The response contains the discount details to be applied to the basket.

```json
[
  {
    "compensationCardId": "CARD_ID_1",
    "discounts": [
      {
        "externalId": "CARD_ID_1",
        "offer": { "type": "flat_off", "value": 1000 },
        "provider": "loyalty",
        "scope": { "type": "order" }
      }
    ],
    "expiresAt": "2024-01-01T00:00:00Z",
    "validationErrors": []
  }
]
```

**Failure (Not Applicable):** The `validationErrors` list will explain why the card cannot be used.

```json
[
  {
    "compensationCardId": "CARD_ID_1",
    "discounts": [],
    "expiresAt": "2024-01-01T00:00:00Z",
    "validationErrors": [
      {
        "code": "invalid_code",
        "message": "Invalid compensation card code"
      }
    ]
  }
]
```

### **Case 2: Re-validating an Applied Card**

This occurs during checkout or basket updates when a card is already present in the order.discounts array.

**Still Valid:**: The response returns the current applicable discount. This ensures that the partner has the most up-to-date calculation (e.g., if the order total changed, the discount value may have been updated).

```json
[
  {
    "compensationCardId": "CARD_ID_1",
    "discounts": {
      "externalId": "CARD_ID_1",
      "offer": {
        "type": "flat_off",
        "value": 1000
      },
      "provider": "loyalty",
      "scope": {
        "type": "order"
      }
    },
    "expiresAt": "2024-01-01T00:00:00Z",
    "validationErrors": []
  }
]
```

**No Longer Valid:** The partner should remove the discount from the order based on the `validationErrors`.

```json
[
  {
    "compensationCardId": "CARD_ID_1",
    "discounts": [],
    "expiresAt": "2024-01-01T00:00:00Z",
    "validationErrors": [
      {
        "code": "inapplicable_code",
        "message": "The applied code is no longer valid"
      }
    ]
  }
]
```

### **Case 3: Removing an Applied Card**

This occurs when a partner removes a card ID from the compensationCardIds list, but the discount is still present in the order object.

The Response will only include a validation object for the gift card that remain selected. The response for the removed gift card (CARD_ID_1) will not be returned.

Request example

```json
{
  "compensationCardIds": [
    "CARD_ID_1"
],
  "order": {
    "discounts": [
      {
        "provider": "loyalty",
        "type": "compensation_card",
        "programId": "CARD_ID_1",
        "value": 1000
      },
      {
        "provider": "loyalty",
        "type": "compensation_card",
        "programId": "CARD_ID_2",
        "value": 1000
      }
    ]
  ...
  }
}
```

Response example

```json
[
  {
    "compensationCardId": "CARD_ID_1",
    "discounts": {
      "externalId": "CARD_ID_1",
      "offer": {
        "type": "flat_off",
        "value": 1000
      },
      "provider": "loyalty",
      "scope": {
        "type": "order"
      }
    },
    "expiresAt": "2024-01-01T00:00:00Z",
    "validationErrors": []
  }
]
```

<br />

<br />