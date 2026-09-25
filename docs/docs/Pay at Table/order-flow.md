---
title: Order Flow
deprecated: false
hidden: true
icon: fad fa-book-open-lines
metadata:
  robots: index
---
Use the Pay at Table API to retrieve an open table bill, wait for the latest bill update, and post a payment to the POS.

This flow applies to unpaid eat-in orders that have been opened on a specific table in the POS.

## Payment flow

1. [Get the tables from the POS](https://developers.deliverect.com/reference/get-pos-tables-from-location) for the location.
2. [Get the bill](https://developers.deliverect.com/reference/bills-by-table) for an open order on a specific table ID.
3. Wait for the bill update event on your [Bill Update webhook URL](https://developers.deliverect.com/reference/channel-bill-update).
4. [Post the payment](https://developers.deliverect.com/reference/post-payment-to-bill) for the specific bill.
5. Wait for the payment result on your [Payment Feedback webhook](https://developers.deliverect.com/reference/channel-payment-feedback).

After you retrieve the bill, Deliverect continues polling the POS for the latest version of the bill. Deliverect sends the most recent bill information to your Bill Update webhook URL.

Use the `freshness` parameter to see how old the bill data is. The value is in seconds.

To confirm that no items were added to the bill after your last request, wait for the bill update event before posting the payment.

When you post the payment, Deliverect sends a synchronous response confirming that your request was received. This response does not confirm that the payment was processed in the POS. Deliverect sends the final processing result to your Payment Feedback webhook.

## Flow diagram

The diagram below shows the full Pay at Table payment flow.

1. Get the bill by table ID and receive a synchronous response with the latest bill information in Deliverect.
2. Deliverect polls the POS for the latest version of the bill.
3. Deliverect sends the most recent version of the bill to your webhook.
4. Post a payment for the specific bill and receive a synchronous response confirming that Deliverect acknowledged your request and is communicating with the POS.
5. Deliverect polls the POS for the latest payment processing status.
6. Deliverect sends the payment processing result to your Payment Feedback webhook.

![Pay at Table API order flow](https://files.readme.io/677a010-21EA358C-B3FB-4BCC-9443-02F68873A334.jpeg)