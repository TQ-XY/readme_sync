---
api:
  file: dispatch_webhooks.json
  operationId: dispatch_cancel_job
hidden: false
---
## Purpose

A merchant or ordering channel may cancel the order, which in turn will cancel the delivery job and it will be communicated as a webhook event to specifiied 'Cancel URL'

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>

    The Cancel Webhook URL needs to be standardised, i.e.
    <strong>the same URL should be used for every customer installation</strong>.
  </p>
</div>
`}</HTMLBlock>

## Request

Below is an example of a cancel event;&#x20;

```json Cancel Delivery Job
{
    "jobId": "5c8******************0d1",
    "account": "5be******************e57",
    "pickupLocation": {
        "location": "5ea******************4a9"
    },
    "deliveryLocations": [
        {
            "orderId": "5f4******************2af",
            "channelOrderDisplayId": "MT4YVTPL",
            "deliveryId": "ABC567"
        }
    ],
    "courier": {
        "courierId": "D1234"
    }
}
```

## Response

We expect the following response to confirm the cancellation is processed on your side.

```json Example Response
{
  "status": "confirmed",
  "reason": "",
  "price": 0
}
```