---
title: Testing
deprecated: false
hidden: true
icon: fad fa-book-open-lines
metadata:
  robots: index
---
Test a Pay at Table order by retrieving the location tables, placing an Eat In order, retrieving the bill, and posting a payment.

## Prerequisites

- Get the `locationId` for the location from the [channel registration webhook](https://developers.deliverect.com/reference/post-channel-status) request.
- Get your channel name and `channelLinkId`.
- Sync or retrieve the table IDs for the location.

Example channel registration webhook request:

```json
{
  "status": "active",
  "channelLocationId": "{{externalChannelLocationId}}",
  "channelLinkId": "{{channelLinkId}}",
  "locationId": "{{locationId}}",
  "channelName": "Space Channel"
}
```

## 1. Retrieve the tables for the location

Call the tables endpoint with the `locationId` for the location:

[`https://api.staging.deliverect.com/tables/{locationId}`](https://api.staging.deliverect.com/tables/{locationId})

You can also sync tables from the Deliverect account:

1. Go to **Locations**.
2. Click **More**.
3. Click **Manage Tables**.

![Manage Tables option in the Deliverect location menu](https://files.readme.io/0238d16-484221C4-7E43-4CAC-9243-93EB7D274089_4_5005_c.jpeg)

## 2. Place a test order

After you have the table IDs from the POS, place a test order:

1. Go to **Menu**.
2. Click **Preview menu**.
3. Add items to the basket.
4. Before you submit the order, click **Add Info**.
5. Select **Eat In** as the order type.
6. Disable **Order is Already Paid**.
7. Add the table number.
8. Save and submit the order.

![Add Info panel for setting the order type and table number](https://files.readme.io/9feb679-38AECB80-0FC6-4FC6-9616-D008B5976954.jpeg)

## 3. Accept the order in the POS

After you place the order, go to the POS and accept it.

## 4. Request the bill ID

Request the bill ID by calling the bills endpoint with your channel name, `channelLinkId`, and `tableId`:

[`https://api.staging.deliverect.com/{channel}/channelLinks/{channelLinkId}/tables/{tableId}/bills`](https://api.staging.deliverect.com/{channel}/channelLinks/{channelLinkId}/tables/{tableId}/bills)

See the expected response in the [Get Bills by Table](https://developers.deliverect.com/reference/bills-by-table) documentation. The response includes the `billId`, payment information, and order items.

## 5. Pay the bill

To pay the bill, call the payments endpoint with your channel name, `channelLinkId`, and `billId`:

[`https://api.staging.deliverect.com/{channel}/channelLinks/{channelLinkId}/bills/{billId}/payments`](https://api.staging.deliverect.com/{channel}/channelLinks/{channelLinkId}/bills/{billId}/payments)

<Callout icon="far fa-bell" theme="info">
  ###

  After every request to get the bill and post a payment, Deliverect sends one event to your bill update webhook URL and payment feedback webhook URL respectively.
</Callout>

See the expected events in the [Bill Update](https://developers.deliverect.com/reference/channel-bill-update) and [Payment Feedback](https://developers.deliverect.com/reference/channel-payment-feedback) documentation.