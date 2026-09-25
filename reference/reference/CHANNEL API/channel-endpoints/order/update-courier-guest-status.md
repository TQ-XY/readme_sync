---
api:
  file: channel.json
  operationId: post_channelname-courierupdate-channellinkid
hidden: false
---
## Purpose

Update courier or a guest's delivery status.

## Courier Update Status:

See the available statuses to set via the link below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/page/order-status#courier-statuses" target="_blank" class="doc-button">▶ See Courier Statuse</a>
`}</HTMLBlock>

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Courier Updates</strong><br>
    In order to help venues optimise their order workflow, it is vital that key stages of <strong>Pickup</strong>, <strong>Dropoff</strong> and <strong>Order Completion</strong> are communicated as and when they apply.
  </p>
</div>
`}</HTMLBlock>

### Customer Arrival Updates

A channel can also use this endpoint to process updates relating to a customers arrival status for either **<Glossary>pickup</Glossary>** or **<Glossary>curbside</Glossary>** orders.

Only with the statuses below can `"pickupNotes"` be applied to pass on details of the customer's current location and other details like their vehicle registration.

| Status Name        | Integer Value |
| :----------------- | :------------ |
| EN_ROUTE_TO_PICKUP | `83`          |
| ALMOST_AT_PICKUP   | `84`          |
| GUEST_ARRIVED      | `85`          |