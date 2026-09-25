---
api:
  file: commerce.json
  operationId: commerce-checkout
hidden: false
---
## Purpose

Create a checkout session for an open basket to process it for POS order injection.

## Format

A checkout request finalizes an open basket into a live order by capturing order details such as the unique `channelOrderId`  along with general information such as cutlery preferences. It's also allowing payment method(s) to be specified as one of three types; <Glossary>Dpay</Glossary>, `third_party`, or `gift_card` with an additional option to itemise multiple payment methods i.e. 'Split Payment'&#x20;

### Body Parameters

For the expected checkout format see the model glossary below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/page/commerce-checkout-glossary" target="_blank" class="doc-button">▶ Checkout Model</a>
`}</HTMLBlock>

### Example

The `order` object includes different payment as shown in the examples below;

```json Dpay
{
  "basket": {
    "id": "62********************3x"
  },
  "order": {
    "channelOrderId": "TEST****629",
    "channelOrderDisplayId": "T**629",
    "by": "Mobile App",
    "includeCutlery": false
  },
  "note": "ORDER LEVEL NOTE",
  "payments": [
    {
      "type": "dpay",
      "externalId": "68****************44",
      "isPrepaid": true,
      "amount": 900,
      "metadata": {}
    }
  ]
}
```
```json Third Party
{
  "basket": {
    "id": "62********************3x"
  },
  "order": {
    "channelOrderId": "TEST****629",
    "channelOrderDisplayId": "T**629",
    "by": "Web App",
    "includeCutlery": false
  },
  "note": "ORDER LEVEL NOTE",
  "payments": [
    {
      "type": "third_party",
      "externalId": "62********************8e",
      "instrumentType": "card",
      "isPrepaid": true,
      "amount": 900,
      "metadata": {}
    }
  ]
}
```
```json Gift Card
{
  "basket": {
    "id": "62********************3x"
  },
  "order": {
    "channelOrderId": "TEST****629",
    "channelOrderDisplayId": "T**629",
    "by": "Web App",
    "includeCutlery": false
  },
  "note": "ORDER LEVEL NOTE",
  "payments": [
    {
      "type": "gift_card",
      "externalId": "63********************f4",
      "isPrepaid": true,
      "amount": 900,
      "metadata": {
        "giftCardProviderProfileLinkId": "67********************t8",
        "giftCardNumber": "62*************44",
        "giftCardVerificationCode": "64**32"
      }
    }
  ]
}
```
```json Multiple Payments
{
  "basket": {
    "id": "62********************3x"
  },
  "order": {
    "channelOrderId": "TEST****629",
    "channelOrderDisplayId": "T**629",
    "by": "Mobile App",
    "courier": "restaurant",
    "includeCutlery": true
  },
  "note": "ORDER LEVEL NOTE",
  "payments": [
    {
      "type": "dpay",
      "externalId": "68********************4e",
      "isPrepaid": false,
      "amount": 300,
      "metadata": {}
    },
    {
      "type": "gift_card",
      "externalId": "63********************f4",
      "isPrepaid": true,
      "amount": 300,
      "metadata": {
        "giftCardProviderProfileLinkId": "67********************t8",
        "giftCardNumber": "62*************44",
        "giftCardVerificationCode": "64**32"
      }
    },
    {
      "type": "third_party",
      "externalId": "66********************h3",
      "isPrepaid": true,
      "instrumentType": "card",
      "amount": 300,
      "metadata": {}
    }
  ]
}
```

# Payment types

There are different types of checkouts depending on the payment method used; a combination of the methods below is also possible (see Multiple payments (split payments) below;

| TYPE                         | DESCRIPTION                                                                                                      | PRE-REQUISITES                                     | ENUM          |
| :--------------------------- | :--------------------------------------------------------------------------------------------------------------- | :------------------------------------------------- | :------------ |
| **Deliverect Pay API**       | For processing payment via our own payment API suite                                                             | <Glossary>Dpay</Glossary> integrated in Deliverect | `dpay`        |
| **Commerce Channel Managed** | If the payment process is fully managed by the commerce platform, e.g. via a direct payment gateway integration. | None                                               | `third_party` |
| **Gift Card**                | For redeeming a gift card balance against the order, in full or in part.                                         | A gift card provider profile linked in Deliverect  | `gift_card`   |

<Accordion title="Deliverect Pay" icon="fa-duotone fa-solid fa-credit-card">
  The `dpay` payment type can be used only after; the payment has been initiated through the Deliverect Pay API, a `paymentId` has been issued, and authorisation has been successfully confirmed.

  During dpay checkout, use the `"paymentId"` from the payment request as the `externalId` as shown in the examples to the right.

  For further details on requesting payments via Deliverect Pay, see the guide below;

    

  <HTMLBlock>{`
  <a href="https://developers.deliverect.com/v3.0-ordering-experience/docs/how-to-request-a-payment" target="_blank" class="doc-button">▶ Payment API Guide</a>
  `}</HTMLBlock>
</Accordion>

<Accordion title="Third party" icon="fa-duotone fa-solid fa-building-columns">
  Use the `third_party` type for payments handled externally e.g. via your own payment provider rather than via Deliverect Pay. Provide the corresponding transaction ID or equivalent as the `externalId` as a reference.

  #### Unpaid orders

  In order to send unpaid orders, set the order type to `"third_party"` and `"isPrepaid": false`.

  #### Instrument Type

  Payment type to be associated with the third-party payment in the order in `"instrumentType"` field.

  - CASH = `"cash"`
  - CARD = `"card"`
  - CASH ON DELIVERY = `"cash_on_delivery"`
  - CARD ON DELIVERY = `"card_on_delivery"`
  - ONLINE = `"online"`
  - INVOICE = `"invoice"`
  - OTHER = `"other"`
</Accordion>

<Accordion title="Gift Card" icon="fa-duotone fa-solid fa-gift">
  Using the [Gift Card API](doc:overview-1) to retrieve a Gift Card balance and validate if it can be applied, the type  `gift_card` can be specified to complete the redemption of a gift card balance. Gift card payments are always `"isPrepaid": true`, since the value is drawn from the card at redemption.

  A `gift_card` payment requires a `metadata` object with the following fields:

  - `giftCardProviderProfileLinkId` — the ID of the gift card provider profile link configured in Deliverect, identifying which provider integration should process the redemption.
  - `giftCardNumber` — the gift card number entered or scanned by the customer.
  - `giftCardVerificationCode` — the card's verification code (PIN/CVC), used by the provider to authorise the redemption.

  The example below shows an order paid entirely with a gift card:

  ```json Gift Card Checkout
  {
    "basket": {
      "id": "62********************3x"
    },
    "order": {
      "channelOrderId": "TEST****629",
      "channelOrderDisplayId": "T**629",
      "by": "Web App"
    },
    "note": "ORDER LEVEL NOTE",
    "payments": [
      {
        "type": "gift_card",
        "externalId": "63********************f4",
        "isPrepaid": true,
        "amount": 900,
        "metadata": {
          "giftCardProviderProfileLinkId": "67********************t8",
          "giftCardNumber": "62*************44",
          "giftCardVerificationCode": "64**32"
        }
      }
    ]
  }
  ```

  <HTMLBlock>{`
  <div class="callout-banner callout-banner--neutral">
    <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
    <p>
      <strong>Partial Gift Card Payment</strong><br>
      Where a gift card balance doesn't cover the full order total, combine it with another payment type — see <a href="#multiple-payments-split-payments">Multiple payments</a>.
    </p>
  </div>
  `}</HTMLBlock>
</Accordion>

<Accordion title="Multiple payments (split payments)" icon="fa-duotone fa-solid fa-layer-group">
  An order can be settled with a combination of payment types by adding multiple entries to the `payments` array. Each entry follows the same rules as it would on its own (e.g. a `dpay` entry still requires a confirmed `paymentId`, a `gift_card` entry still requires its `metadata`), and the sum of all `amount` values must equal the basket total.

  The example below splits a `900` total across three methods: `300` charged via Deliverect Pay but not yet collected (`"isPrepaid": false`), `300` redeemed from a gift card, and `300` already captured by an external provider via card:

  ```json Multiple Payments Checkout
  {
    "basket": {
      "id": "62********************3x"
    },
    "order": {
      "channelOrderId": "TEST****629",
      "channelOrderDisplayId": "T**629",
      "by": "Mobile App",
      "courier": "restaurant"
    },
    "note": "ORDER LEVEL NOTE",
    "payments": [
      {
        "type": "dpay",
        "externalId": "68********************4e",
        "isPrepaid": false,
        "amount": 300,
        "metadata": {}
      },
      {
        "type": "gift_card",
        "externalId": "63********************f4",
        "isPrepaid": true,
        "amount": 300,
        "metadata": {
          "giftCardProviderProfileLinkId": "67********************t8",
          "giftCardNumber": "62*************44",
          "giftCardVerificationCode": "64**32"
        }
      },
      {
        "type": "third_party",
        "externalId": "66********************h3",
        "isPrepaid": true,
        "instrumentType": "card",
        "amount": 300,
        "metadata": {}
      }
    ]
  }
  ```
</Accordion>

## Dispatch Orders

For any delivery order, it is optional to leverage integrated Dispatch services by first pre-validating courier availability.

Once a courier is confirmed as available, a `validationId` is returned, which can be passed within the checkout stage as below and will secure the delivery job and initiate the dispatch flow;

```json Dispatch Order
"order": {
  "validationId": "{{uuid}}",
},
```

See documentation below on the 'Dispatch Availability' endpoint;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/post_fulfillment-validate" target="_blank" class="doc-button">▶ Dispatch Availability</a>
`}</HTMLBlock>

## Non-Dispatch Orders

In the case where a Deliverect integrated dispatch service is not needed, no address needs provided, but a key `"courier"` needs specified, with any string value like below which isn't '`restaurant`'.

```json Courier Example
"order": {
  "courier": "thirdparty"
},
```

# Checkout Confirmation

Regardless of the payment type, after sending a basket checkout request, Deliverect returns a 200 OK response if the request is valid.

Order creation is handled asynchronously, and a webhook event confirming successful order creation is sent to the configured [checkout update webhook URL](https://developers.deliverect.com/v3.0/reference/post_checkout-update).

<HTMLBlock>{`
<div class="callout-banner callout-banner--important">
  <span class="callout-icon"><i class="fa-duotone fa-solid fa-triangle-exclamation"></i></span>
  <p>
    <strong>Checkout Success</strong><br>
    Only consider a checkout successful after the basket checkout webhook URL receives <code>"status": "completed"</code>.
  </p>
</div>
`}</HTMLBlock>

## Cancel Orders

See below endpoint to process order cancellations;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/create-channel-order#channel-cancelations" target="_blank" class="doc-button">▶ Order Cancelations</a>
`}</HTMLBlock>