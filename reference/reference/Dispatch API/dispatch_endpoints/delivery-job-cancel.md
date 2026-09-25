---
api:
  file: dispatch.json
  operationId: post_fulfillment-cancel
hidden: false
---
## Purpose

This endpoint allows a way of receiving notification from our partners that a job they have previously accepted is no longer possible to be dispatched by their system.

## Reason Tags

Cancelations shoud be tagged accordingly using one of the below;

| reasonTag                     | Meaning                                                                                                  |
| :---------------------------- | :------------------------------------------------------------------------------------------------------- |
| `COURIER_NO_LONGER_AVAILABLE` | There is no longer an available courier for the delivery                                                 |
| `COURIER_TRANSPORT_FAILURE`   | Courier attempted to deliver but could not because of a transport failure (e.g., a flat tire)            |
| `FOOD_ITEMS_ARE_NOT_READY`    | The order was not ready within the agreed time after pick up (between the dispatch partner and merchant) |
| `DROP_OFF_LOCATION_NOT_FOUND` | The courier could not find the delivery location                                                         |
| `CUSTOMER_UNRESPONSIVE`       | The customer did not pick up the phone nor open the door.                                                |
| `PACKAGE_SIZE_TOO_LARGE`      | The package size is too large to be delivered                                                            |

<br />

<HTMLBlock>{`
<div style="
  background-color: #f0f9f0;
  border: 1px solid #c8e6c9;
  border-radius: 12px;
  padding: 20px 24px;
  margin: 16px 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
">
  <p style="
    margin: 0 0 8px 0;
    color: #1b5e20;
    font-weight: 700;
    font-size: 16px;
    display: flex;
    align-items: center;
    gap: 8px;
  ">
    <span style="font-size: 18px;">ℹ️</span>
    Cancellation Cut-off Time
  </p>
  <p style="
    margin: 0;
    color: #2e5934;
    font-size: 15px;
    line-height: 1.6;
  ">
    You can cancel a delivery job with a valid <code>reasonTag</code> at any point before its status changes to <code>Delivered</code>.
  </p>
</div>
`}</HTMLBlock>

<br />