---
api:
  file: dispatch.json
  operationId: post_fulfillment-generic-events
hidden: false
---
## Purpose

This endpoint allows persisting updates from third-party delivery systems to Deliverect.

## Format

Updates to the following are supported;

- Delivery Job Statuses
- Pickup Time & ETA
- Delivery Time & ETA
- Courier Information

## Delivery Job Statuses:

| Status Name           | Meaning                                          | Integer Value |
| :-------------------- | :----------------------------------------------- | :------------ |
| `COURIER_ASSIGNED`    | Courier has been assigned                        | `73`          |
| `EN_ROUTE_TO_PICKUP`  | Courier approaching the pickup location          | `83`          |
| `ARRIVED_AT_PICKUP`   | The courier has arrived at the pickup location   | `85`          |
| `EN_ROUTE_TO_DROPOFF` | Courier approaching the drop-off location        | `87`          |
| `ARRIVED_AT_DROPOFF`  | The courier has arrived at the drop-off location | `89`          |
| `DELIVERED`           | Courier has delivered the order                  | `90`          |

<TimestampsUTC />
