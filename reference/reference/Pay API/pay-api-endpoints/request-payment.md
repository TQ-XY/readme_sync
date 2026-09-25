---
api:
  file: payapi.json
  operationId: pay_endpoints-request-payment
hidden: false
---
## Purpose

Deliverect Pay's API <Glossary>Dpay</Glossary> allows channels to request a payment with two payment mode types of `redirect` or `token`&#x20;

## Overview

The formats for requesting a payment are outlined as below;

1. **Channel → Deliverect Pay** — the payment request specifies a mode of either `redirect` or `token`(card data is not transmitted in either case)
2. **Deliverect Pay → Payment Service Provider** — a redirect URL is returned or funds are acquired (captured or pre-authorized based on `captureMode`of `immediate` or `manual`.
3. **Payment Service Provider → Deliverect Pay → Channel** — the channel receives the payment identifier and status

## Request a payment using a token

Once a token has been verified by calling the [Create Token](ref:token-proxy) endpoint this can be used to acquire funds.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <div>
    <p><strong>Capture mode</strong></p>
    <p>Fund acquisition can be requested in two capture modes:</p>
    <table>
      <thead>
        <tr>
          <th>Mode</th>
          <th>Behavior</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><code>immediate</code></td>
          <td>Capture the funds instantly <em>(default)</em>.</td>
        </tr>
        <tr>
          <td><code>manual</code></td>
          <td>Pre-authorize the funds now; capture them later.</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>
`}</HTMLBlock>

### Path parameters

| Parameter       | Type   | Description                                                                                |
| --------------- | ------ | ------------------------------------------------------------------------------------------ |
| `channelLinkId` | string | The channel link the payment is requested under. Must match the link used at tokenization. |

#### Request body

| Field                | Description                                                                             | Type    |
| -------------------- | --------------------------------------------------------------------------------------- | ------- |
| `gatewayProfileId`\* | Gateway configuration to route the payment through.                                     | string  |
| `mode`\*             | How the payment is funded.                                                              | object  |
| `mode.type`\*        | Payment mode. Use `token` for token-based payments (other modes exist).                 | string  |
| `mode.tokenId`\*     | The `id` of a **verified** token from [Create Token](ref:token-proxy)                   | string  |
| `captureMode`        | `immediate` (default) or `manual`. See capture modes above.                             | string  |
| `amount`\*           | Amount in the currency's **minor units** (e.g. `1000` = 10.00 USD).                     | integer |
| `currency`\*         | ISO 4217 currency code (e.g. `USD`).                                                    | string  |
| `payer`\*            | Details of the paying customer.                                                         | object  |
| `payer.name`\*       | The payer's display name.                                                               | string  |
| `payer.reference`\*  | Channel-side customer reference — typically the same `customerId` used at tokenization. | string  |

#### Response body

| Field           | Type   | Description                                                                                                                                                           |
| --------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `paymentId`     | string | Identifier of the created payment. Use it to reference the payment in subsequent operations (e.g. capture, refund).                                                   |
| `paymentStatus` | string | Status of the payment, e.g. `authorized`. With `captureMode: "immediate"` funds are captured right away; with `manual` the payment remains authorized until captured. |

####

***

## Glossary of attributes

<HTMLBlock>{`
<a 
  href="https://developers.deliverect.com/page/glossary-payment-api"
  target="_blank"
  style="
    background-color: #058851;
    border-radius: 12px;
    padding: 12px 20px;
    color: #ffffff;
    text-decoration: none;
    display: inline-flex;
    align-items: center;
    gap: 8px;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    font-size: 14px;
    font-weight: 700;
    line-height: 1;
  "
>
  ▶ Payment Glossary
</a>
`}</HTMLBlock>