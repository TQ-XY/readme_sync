---
api:
  file: loyalty_webhooks.json
  operationId: loyalty_programs_loyalty
hidden: false
---
## Purpose

This webhook is used by channels to retrieve a list of loyalty programs available to a specific customer.&#x20;

# Request Payload

| Field       | Type     | Required | Description                                                                                         |
| :---------- | :------- | :------- | :-------------------------------------------------------------------------------------------------- |
| `sessionId` | `string` | Yes      | A unique session identifier.                                                                        |
| `order`     | `object` | Yes      | See **Order schema**[ 🔗](https://developers.deliverect.com/update/reference/loyalty-order-schema/) |

<br />

# Expected Response Schema

| Field             | Type                | Required | Description                                                                                 |
| :---------------- | :------------------ | :------- | :------------------------------------------------------------------------------------------ |
| `programId`       | `string`            | Yes      | The unique identifier of the loyalty program.                                               |
| `title`           | `string`            | Yes      | The title or display name of the program.                                                   |
| `type`            | `string` (enum)     | Yes      | Type of the loyalty program.                                                                |
| `applicable`      | `boolean`           | No       | Indicates if the customer meets the basic requirements for this program. Default is `true`. |
| `description`     | `string`            | **Yes**  | A description of the loyalty program.                                                       |
| `cost`            | `number`            | No       | The cost of the program, e.g., the number of loyalty points to redeem.                      |
| `media`           | `object`            | No       | Media assets associated with the program, such as an image or icon.                         |
| `media.mediaType` | `string`            | Yes      | Values may be: `image` / `video`                                                            |
| `media.url`       | `string`            | Yes      | The url of the resource                                                                     |
| `expiresAt`       | `string` (ISO 8601) | No       | The expiration date and time of the program.                                                |
| `discount`        | `number`            | No       | The specific discount value.                                                                |
| `itemPLU`         | `string`            | No       | The PLU of the item to which the program applies.                                           |
| `quantity`        | `number`            | No       | The quantity of items affected by the program.                                              |
| `minOrderValue`   | `number`            | No       | The minimum order value required for this program to be applicable.                         |

# Loyalty program types

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Name
      </th>

      <th>
        Value
      </th>

      <th>
        Description
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Flat off order
      </td>

      <td>
        `discount_amount`
      </td>

      <td>
        Contains a predetermined monetary amount which is subtracted from the price of an order.
      </td>
    </tr>

    <tr>
      <td>
        Percent off order
      </td>

      <td>
        `discount_percentage`
      </td>

      <td>
        Contains a predetermined percentage amount which is then calculated based on the order, and subtracted from the price.
      </td>
    </tr>

    <tr>
      <td>
        Flat off item
      </td>

      <td>
        `item_discount_amount`
      </td>

      <td>
        Contains a predetermined monetary amount which is subtracted from the price of an item.
      </td>
    </tr>

    <tr>
      <td>
        Percent off item
      </td>

      <td>
        `item_discount_percentage`
      </td>

      <td>
        Contains a predetermined percentage amount which is then calculated based on the item and subtracted.
      </td>
    </tr>

    <tr>
      <td>
        Item fixed amount
      </td>

      <td>
        `item_fixed_price`
      </td>

      <td>
        The configured item will be available at a fixed base price. Modifiers might come at an additional price depending on the menu configuration.
      </td>
    </tr>

    <tr>
      <td>
        Buy one get one for free
      </td>

      <td>
        `buy_one_get_one_free`
      </td>

      <td>
        Free extra item that will be added to an order if the item already exists in the order. `itemPLU` field is required for this type of programs.
      </td>
    </tr>

    <tr>
      <td>
        Free Item
      </td>

      <td>
        `free_item`
      </td>

      <td>
        Free extra item that will be added to an order, `itemPLU` field is required for this type of programs.

        Note: available for Deliverect Kiosk, not on Deliverect Direct.
      </td>
    </tr>
  </tbody>
</Table>

The webhook supports two distinct use cases, differentiated by the level of detail included in the order payload.

## 1. Case: Listing All Available Programs

This use case is for when a channel wants to display all potential loyalty programs a customer can access, before they start building an order basket. The request payload will contain only customer and session details.

### Request Payload:

The request payload will include a sessionId and customer information.

```json Payload
{
   "accountId":"67acb06448864d7b4f0a51b6",
   "locationId":"6403c0baea6956b6f6970c5c",
   "channelLinkId":"6403c0b9ea6956b6f6970c5b",
   "loyaltyProfileId":"67acb4da622cc8743d8abd34",
   "order":{
      "accountId":"67acb06448864d7b4f0a51b6",
      "locationId":"6403c0baea6956b6f6970c5c",
      "channelLinkId":"6403c0b9ea6956b6f6970c5b",
      "orderType":3,
      "customer":{
         "email":"loyalty@customer.com",
         "phoneNumber":"+31201234567",
         "name":"John Doe"
      },
      "items":[
         {
            "plu":"CMB-02",
            "name":"Vegetarian Rames",
            "price":1700,
            "quantity":1,
            "subItems":[
               {
                  "plu":"VEG-01",
                  "name":"Vegetables Sayur Lodeh",
                  "price":0,
                  "quantity":1,
                  "subItems":[
                     
                  ]
               },
               {
                  "plu":"VEG-02",
                  "name":"Vegetables Mix Tumisan",
                  "price":0,
                  "quantity":1,
                  "subItems":[
                     
                  ]
               }
            ]
         }
      ],
      "discounts":[
         {
            "name":"Amount discount",
            "programId":"1234",
            "type":"discount_amount",
            "amount":100
         }
      ],
      "subTotal":1700,
      "discountTotal":-100,
      "paymentAmount":1600,
      "decimalDigits":2
   }
}
```

As a response Deliverect expects validated list of loyalty programs available for a given customer.

### Expected Response Payload:

The loyalty provider must respond with a list of all programs the customer has access to. Since no order items are provided in the request, many programs may be marked as not applicable.

The applicable field indicates whether a customer meets the basic requirements for the program to be applied, such as having enough points or the program not being expired. The loyalty partner may perform extra checks to determine which programs can be marked as applicable.

Example Response:

```json
[
    {
        "programId": "1",
        "title": "Discount",
        "description": "Discount amount for the order.",
        "cost": 100,
        "type": "discount_amount",
        "discount": 100,
        "applicable": true
    },
    {
        "programId": "4",
        "title": "50% Order percent off",
        "type": "discount_percentage",
        "applicable": true,
        "description": "Get 50% OFF the order",
        "cost": 200,
        "media": {
            "url": "",
            "mediaType": "image"
        },
        "expiresAt": null,
        "discount": 5000
    },
    {
        "programId": "2",
        "title": "Free item",
        "description": "Get an item for free.",
        "cost": 500,
        "type": "free_item",
        "itemPLU": "DRN-01",
        "media": {
            "url": "https://program.media/image",
            "mediaType": "image"
        },
        "applicable": false
    },
    {
        "programId": "3",
        "title": "Buy one get one for free",
        "description": "Get a cookie with the purchase of another cookie!",
        "cost": 100,
        "type": "buy_one_get_one_free",
        "itemPLU": "DRN-02",
        "media": {
            "url": "https://program.media/image",
            "mediaType": "image"
        },
        "applicable": true
    },
    {
        "programId": "5",
        "title": "Coke $10 off",
        "type": "item_discount_amount",
        "applicable": true,
        "description": "For our premium cokes!",
        "cost": 150,
        "media": {
            "url": "",
            "mediaType": "image"
        },
        "expiresAt": null,
        "discount": 1000
    },
    {
        "programId": "6",
        "title": "Coke 50% off",
        "type": "item_discount_percentage",
        "applicable": true,
        "description": "Great discount for a coke!",
        "cost": 150,
        "media": {
            "url": "",
            "mediaType": "image"
        },
        "expiresAt": null,
        "discount": 5000
    },
    {
        "programId": "7",
        "title": "Hamburger for $5",
        "type": "item_fixed_price",
        "applicable": true,
        "description": "Get a hamburger for only $5",
        "cost": 150,
        "media": {
            "url": "",
            "mediaType": "image"
        },
        "expiresAt": null,
        "discount": 500
    }
]
```

## 2. Case: Listing Programs Applicable to a Current Basket

This use case is for when a channel wants to see which programs are applicable to a customer's current order, including all items and existing discounts.

### Request Payload:

For this case, the loyalty provider will receive the full order payload.

Example Request:

```json
{
  "sessionId": "{{loyaltySessionId}}",
  "order": {
    "customer": {
      "name": "{{loyaltyCustomerFirstName}} {{loyaltyCustomerLastName}}",
      "email": "{{loyaltyCustomerEmail}}",
      "phoneNumber": "{{loyaltyCustomerPhone}}",
      "loyaltyProviderCustomerId": "{{loyaltyCustomerProviderId}}"
    },
    "orderType": 2,
    "items": [
      {
        "plu": "P-TE-zxb3-2",
        "name": "Burger",
        "price": 10000,
        "quantity": 1,
        "subItems": [],
        "productType": 1
      }
    ],
    "payment": {
      "amount": 10000
    },
    "discounts": []
  }
}
```

### Expected Response Payload:

The response must return a list of all programs, with the applicable field indicating whether they can be applied to the current basket. The applicable field's meaning remains the same as in Case 1.

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
    "media": {
      "url": "...",
      "mediaType": "image"
    },
    "expiresAt": null,
    "discount": 200,
    "itemPLU": null,
    "quantity": null,
    "minOrderValue": 1000
  }
]
```