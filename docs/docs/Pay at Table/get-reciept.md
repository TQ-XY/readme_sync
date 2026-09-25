---
title: GET Reciept
deprecated: false
hidden: true
icon: fad fa-book-open-lines
metadata:
  robots: index
---
## Get Receipt

Use this guide to collect the identifiers you need to test the GET Receipt endpoint in your staging environment.

**Prerequisites**

1. Contact the API support team and ask them to enable GET Receipt testing for your staging environment.
2. Confirm that the support team has linked a test location to a Lightspeed POS (point of sale) integration.
3. Confirm that the Lightspeed Test Menu is available in your staging environment.
4. Use your staging API credentials when you call the GET Receipt endpoint.

<br />

Go to Location and find the location with the Lightspeed logo.

![location with lightspeed logo](https://files.readme.io/1dac4df-985922F5-F3E3-4705-B38D-E6A658A94FBB_4_5005_c.jpeg "985922F5-F3E3-4705-B38D-E6A658A94FBB_4_5005_c.jpeg")

Go to Menu and find the Lightspeed Test Menu already created for you.

![Receipt ID is displayed](https://files.readme.io/1a61710-5A802B8F-5BB0-4069-9D78-0539DBC7B335_4_5005_c.jpeg "5A802B8F-5BB0-4069-9D78-0539DBC7B335_4_5005_c.jpeg")

Once you have placed a test order, go to the Orders tab and look for the receiptId.

![1568](https://files.readme.io/59f76b8-EAE41795-D5F5-4690-8039-4C51C9C352BC_4_5005_c.jpeg "EAE41795-D5F5-4690-8039-4C51C9C352BC_4_5005_c.jpeg")

You need the `receiptId` or the `tableId`, and the `locationId` in order to perform this call.

In order to get the `tableId`, you need to call the [Get POS Tables from Location](https://developers.deliverect.com/reference/get-pos-tables-from-location) endpoint.

You can then place a test "eat in" order using one of the eat-in table IDs and use that `tableId` to `GET Receipt`.