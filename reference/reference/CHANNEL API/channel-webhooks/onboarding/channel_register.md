---
api:
  file: channel_webhooks.json
  operationId: channel_register
hidden: false
---
## Purpose

To support customer onboardings, the webhook events below will communicate a stores `status` which instructs the channel to update the corresponding status on their side.&#x20;

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>The Register Webhook URL needs to be standardised, i.e.<strong>the same URL should be used for every customer installation</strong>.
  </p>
</div>
`}</HTMLBlock>

## Request

| Parameter           | Meaning                                                                                                                                                                                                                                                                                                                                          | Type   |
| :------------------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :----- |
| `status`            | `register` A new store/location needs to establish a connection between Deliverect and a channel platform<br /><br />`active` A new store/location is ready to start receiving orders into Deliverect from the channel platform<br /><br />`inactive` A customer wants to stop receiving orders to this store/location from the channel platform | string |
| `channelLocationId` | An identifier which can be set in Deliverect, which is know to the Merchant and allows mapping to the corresponding Deliverect channel link                                                                                                                                                                                                      | string |
| `channelLinkId`     | The<Glossary>channelLinkId</Glossary> is the unique store identifier in Deliverect for a specific channel in a location                                                                                                                                                                                                                          | string |
| `locationId`        | <Glossary>Location</Glossary>Id is the unique identifier of the location in Deliverect.                                                                                                                                                                                                                                                          | string |
| `channelLinkName`   | The channel name displayed in Deliverect.                                                                                                                                                                                                                                                                                                        | string |

### **Examples**

```json register
{
    "status": "register",
    "channelLocationId": "{{externalChannelLocationId}}",
    "channelLinkId": "{{channelLinkId}}",
    "locationId": "{{locationId}}",
    "channelLinkName": "Order Boss"
}
```
```json active
{
    "status": "active",
    "channelLocationId": "{{externalChannelLocationId}}",
    "channelLinkId": "{{channelLinkId}}",
    "locationId": "{{locationId}}",
    "channelLinkName": "Order Boss"
}
```
```json inactive
{
    "status": "inactive",
    "channelLocationId": "{{externalChannelLocationId}}",
    "channelLinkId": "{{channelLinkId}}",
    "locationId": "{{locationId}}",
    "channelLinkName": "Order Boss"
}
```

### Response Body

With the `"status": "register"` we always expect a JSON result which contains all the supported endpoints detailed in the table below;

| Attribute           | Purpose                                                                | Type   | Required |
| :------------------ | :--------------------------------------------------------------------- | :----- | :------- |
| `statusUpdateURL`   | Receive [Order Status Update](ref:channel_order_status) events         | string | YES      |
| `menuUpdateURL`     | Receive [Menu Update](ref:channel_menu_update) requests                | string | YES      |
| `snoozeUnsnoozeURL` | Receive both [Snooze / Unsnooze Products](ref:channel_snooze) requests | string | YES      |
| `busyModeURL`       | Receive [Busy mode](ref:busy-mode) requests (paused/online)            | string | YES      |
| `updatePrepTimeURL` | Receive [Preparation Time Update](ref:channel_prep_time) requests      | string | NO       |
| `courierUpdateURL`  | Receive [Courier Update](ref:courier-update-webhook) events            | string | NO       |
| `paymentUpdateURL`  | Received [Payment Update](ref:payment-update-webhook) events           | string | NO       |
| `authorizationURL`  | Receive [SSO Authorization](ref:channel_authorize) requests            | string | NO       |
| `menuUrl`           | Merchant Store URL / site URL                                          | string | NO       |

### **Response Example**

```json 200 OK
{
  "statusUpdateURL": "https://integrator.com/statusUpdate",
  "menuUpdateURL": "https://integrator.com/menuUpdate",
  "snoozeUnsnoozeURL": "https://integrator.com/snoozeUnsnooze",
  "busyModeURL": "https://integrator.com/busyMode",
  "updatePrepTimeURL": "https://integrator.com/updatePrepTimeURL",
  "paymentUpdateURL": "https://yourwebhook.com/payment_update",
  "courierUpdateURL": "https://yourwebhook.com/courier_update",
  "authorizationURL": "https://yourwebhook.com/authorization",
  "menuUrl": "https://integrator.com/store"
}
```

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>

    Please note, the expected response is
    <strong>case-sensitive</strong> ensure the response matches the required format exactly.
  </p>
</div>
`}</HTMLBlock>