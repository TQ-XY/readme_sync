---
api:
  file: channel.json
  operationId: post_channelname-updatestorestatus-channellinkid
hidden: false
---
## Purpose

A channel platform may close a customer's stores for a range of reasons e.g. after too many failed orders. This endpoint allows an updated store status to sync from the channel into Deliverect.

## Request

For the payload, we always expect a JSON that contains:

- `status`: expeсted values would be `open` or `closed`.
- `reason`: reason for the status changes.

<br />