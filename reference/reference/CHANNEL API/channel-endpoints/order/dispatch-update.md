---
api:
  file: channel.json
  operationId: order-delivery-update-1
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
## Purpose

When a dispatch partner is assigned a delivery job, the details of the job can be queried via this endpoint.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Dispatch Integration Required</strong><br>
      Delivery details are only available where a Dispatch partner is integrated with Deliverect. It does not return results from ordering platforms partners who handle delivery.
  </p>
</div>
`}</HTMLBlock>

### Path Parameters

| Attribute | Definition                                                                                                                                                                                      |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `orderId` | Unique identifier of the Deliverect order, will be returned asynchronously via [Create / Cancel Order](ref:create-channel-order) or retrievable with [Get Checkout](ref:commerce-get-checkout)  |

<br />

### Response parameters

The response includes the following delivery details;

| Attribute               | Definition                                                                 | Type           |
| ----------------------- | -------------------------------------------------------------------------- | -------------- |
| `account`               | Unique identifier of the Deliverect account associated with the delivery.  | string         |
| `location`              | Unique identifier of the Deliverect location associated with the delivery. | string         |
| `pickupTime`            | Scheduled time for the courier to collect the order.                       | string         |
| `pickupTimeETA`         | Estimated time for the courier to collect the order.                       | string         |
| `transportType`         | Transport method used for the delivery.                                    | string         |
| `price`                 | Delivery price.                                                            | number         |
| `trackingURL`           | URL for tracking the delivery with the dispatch provider, when available   | string         |
| `deliverectTrackingURL` | Deliverect tracking URL, when available                                    | string or null |
| `deliveryTimeETA`       | Estimated time when the order will be delivered.                           | string         |

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Tracking URL Availability</strong><br>
     A tracking URL is returned only when supported by the Dispatch provider.
  </p>
</div>
`}</HTMLBlock>

## Courier Statuses

For a full list of all courier `status` values, see the link below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/page/order-status#courier-statuses" target="_blank" class="doc-button">▶ Courier Statuses</a>
`}</HTMLBlock>