---
api:
  file: channel_webhooks.json
  operationId: channel_order_status
hidden: false
---
## Purpose

Whenever a POS updates the status of an order, we will deliver a webhook event to your specified endpoint.

Each integrated POS will provide statuses in accordance with their own workflows, meaning the specific statuses received can vary, yet any order with status between `20` (Accepted) and `95` (Auto-finalized) confirms a successfully accepted order.

Statuses higher than `95`, indicate that something went wrong with the order.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>

  If you receive a status that is not documented below, it can safely be ignored, an unknown status should not impact normal order processing workflow
  </p>
</div>
`}</HTMLBlock>

<HTMLBlock>{`
<a href="https://developers.deliverect.com/page/order-status" target="_blank" class="doc-button">▶ See All Order Statuses</a>
`}</HTMLBlock>

## Canceled Orders

An ordering platform can process cancellations via the `/order` endpoint (see [Create / Cancel Order](ref:create-channel-order)) cancellations can also be initiated from the POS.

When a POS cancels an order, a status `110` is sent as per example below. This information should be related to the end-consumer in whichever manner possible i.e. email notification of an unsuccessful order.

When a merchant choses not to accept an order via our Delivery Manager App (DMA) they can choose to 'Reject' the order, in which case, the status 'Denied' is sent `35`

```json Order Accepted
{
    "orderId": "61********************b4",
    "status": 20,
    "timeStamp": "YYYY-MM-DDTHH:mm:ss.SSSSSSZ",
    "receiptId": "",
    "reason": "",
    "channelOrderId": "TEST******4206",
    "location": "61********************b4",
    "channelLink": "61********************c3"
}
```
```json Order Denied
{
    "orderId": "61********************b4",
    "status": 35,
    "timeStamp": "YYYY-MM-DDTHH:mm:ss.SSSSSSZ",
    "receiptId": "",
    "reason": "Device ID: 24b35c00-c66d-4176-9032-27f28033d3a0",
    "channelOrderId": "TEST******4206",
    "location": "61********************b4",
    "channelLink": "61********************c3"
}
```
```json Order Cancelled
{
    "orderId": "61********************b4",
    "status": 110,
    "timeStamp": "YYYY-MM-DDTHH:mm:ss.SSSSSSZ",
    "receiptId": "",
    "reason": "Item out of stock",
    "channelOrderId": "TEST******4206",
    "location": "61********************b4",
    "channelLink": "61********************c3"
}
```
```json Order Failed
{
    "orderId": "61********************b4",
    "status": 120,
    "timeStamp": "YYYY-MM-DDTHH:mm:ss.SSSSSSZ",
    "receiptId": "",
    "reason": "",
    "channelOrderId": "TEST******4206",
    "location": "61********************b4",
    "channelLink": "61********************c3"
}
```

Each incoming status update should be confirmed with an HTTP status 200.

```json Example Response 200 OK
{
  "result": "OK"
}
```