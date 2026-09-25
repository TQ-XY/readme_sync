---
api:
  file: loyalty_webhooks.json
  operationId: loyalty_validateprogram
hidden: false
---
## Purpose

This webhook is called by our system to confirm a customer's loyalty program selection and retrieve the final discount details to apply to the basket. The loyalty provider is responsible for validating the selected program against the order using its internal business rules, and must respond with the final discount details for the channel to apply. Note that a single program can result in multiple discounts being applied to the order.

### Format

This webhook is triggered in two scenarios;

- When a customer selects a loyalty program to add to their basket.
- Before the customer proceeds to payment, to ensure all discounts are correctly applied.

## Internal Logic for Program Application

**Program Availability Verification:** Your system will receive a payload containing the selected programs and the current order. You are responsible for verifying the program's availability and business rules.

**Handling Already Applied Programs:** If a program has already been applied (and is present in the order's discounts payload), our system will revalidate it. Your response should reconfirm the program's validity without adding any new discounts.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>

    The webhook request does not intend to validate the correctness of the discounts that are already present in the order payload.
  </p>
</div>
`}</HTMLBlock>

## Request Payload

Your webhook will receive a POST request with a JSON body. The request will include the list of programIds to be validated and the complete order payload.

This schema defines the complete request body sent to the wallet validation webhook.

| Field              | Type               | Required | Description                                                                                              |
| :----------------- | :----------------- | :------- | :------------------------------------------------------------------------------------------------------- |
| `accountId`        | `string`           | Yes      | The unique identifier for the **merchant account**.                                                      |
| `loyaltyProfileId` | `string`           | Yes      | The unique identifier for the customer's **loyalty profile** within the system.                          |
| `sessionId`        | `string`           | No       | A unique **session token** linking all related loyalty actions (e.g., retrieve, validate, create order). |
| `locationId`       | `string`           | Yes      | The ID of the specific store/location where the order is being placed.                                   |
| `channelLinkId`    | `string`           | Yes      | The unique identifier linking the channel to the account/location.                                       |
| `order`            | `object`           | Yes      | See **Order schema**[ 🔗](https://developers.deliverect.com/update/reference/loyalty-order-schema/)      |
| `programIds`       | `array of strings` | Yes      | A list of program Ids that the customer has selected to apply to their basket.                           |

Example Request:

```json
{
  "sessionId": "test",
  "accountId": "6798b2b2a030bcf7dd6c1ee0",
  "loyaltyProfileId": "68fa15d0ab58f558a01a77de",
  "locationId": "684940131579e410c7792348",
  "channelLinkId": "684940251579e410c7792352",
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

## Expected Response Schema and Structure

Your webhook must respond with a JSON payload that follows our defined schema. The response is an array of objects, with one object for each program that was included in the request. The new schema provides a flexible structure for discounts.

### Field Deprecation:

We are actively deprecating a number of fields from our previous schema. During a transition period, our system will send a Transitional Response that includes both deprecated and new fields. In a future update, all deprecated fields will be entirely removed.

### Response Schema Details:

| Field            | Type             | Nullable | Description                                                                                                                                                                                                                             |
| :--------------- | :--------------- | :------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| programId        | string           | No       | The unique identifier of the loyalty program that was validated.                                                                                                                                                                        |
| validationErrors | array of objects | No       | A list of errors. Each object contains a message string explaining the failure. This array is empty on successful validation.                                                                                                           |
| discounts        | array of objects | No       | A list of validated discount objects to be applied to the order. Empty if validation fails or if the program has already been applied. See **Discount Schema page**[ 🔗](https://developers.deliverect.com/reference/loyalty-discounts) |

<br />

### Response Examples

It contains only the essential, machine-readable information required to apply a discount.

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

### Program Removal

Some loyalty providers may place a temporary lock on a program for fraud prevention after validation. To remove a program from the basket, our system will call your webhook by:

- Excluding the program's ID from the `programIds` array.
- Including the program's discount details in the order.discounts payload to signal its removal.

This process informs your system to release the lock on the program, making it available for the user again.

**Expected Response:** Your response should only include a validation object for the programs that remain selected in the programIds array. The removed program should not be included in the response.

<br />