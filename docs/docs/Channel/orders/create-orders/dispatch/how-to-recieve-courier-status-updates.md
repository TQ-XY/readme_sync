---
title: How to recieve courier status updates
deprecated: false
hidden: false
metadata:
  robots: index
---
## Introduction

Implement a courier status update webhook to receive real-time delivery updates from a dispatch partner and keep your customers informed.

### Format

This webhook returns updates from dispatch partners. It does not return updates for channel partners, which are ordering platforms that may also deliver orders.

The courier status update webhook sends an update when the dispatch partner reports a change in the courier journey (the delivery process from dispatch through completion). These updates help you show customers the current state of their delivery.

The webhook sends updates for:

- Estimated delivery time changes when `deliveryTimeETA` changes by more than 60 seconds. Deliverect uses this threshold to reduce minor ETA fluctuations while still sending meaningful delivery time changes. The value uses UTC format.
- Changes to the courier's name.
- Dispatch partner actions that change the order status.
- Updated courier coordinates from the dispatch partner.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Pre-requisites</strong><br>
   Ensure that there is a registered dispatch partner who is integrated with our Dispatch API and also connected to the customer (restaurant or food business) account. This webhook does not return results for channel partners who may also deliver orders.
  </p>
</div>
`}</HTMLBlock>

## Required request details

Use the [Courier Status Update API reference](https://developers.deliverect.com/v3.0-ordering-experience/reference/courier-update-webhook) as the source of truth for request fields, field types, and supported status values.

At minimum, your webhook handler should:

1. Read the fields that identify the order and courier update.
2. Process status changes from the dispatch partner.
3. Process `deliveryTimeETA` changes when present.
4. Process courier name and coordinate updates when present.
5. Store or forward the update to the systems that notify customers.

## Webhook configuration

Configure your webhook to respond with `200 OK` after it receives and processes an update successfully.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <Callout icon="👍" theme="okay">
  Courier status updates arrive in real time. Design your webhook handler to process updates promptly and avoid delaying the <code>200 OK</code> response.
</Callout>
  </p>
</div>
`}</HTMLBlock>

<br />

<br />

<br />
