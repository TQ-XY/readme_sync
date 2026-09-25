---
title: Troubleshooting
deprecated: false
hidden: false
icon: fad fa-bullseye-arrow
metadata:
  robots: index
---
## Order Creation Issues

Below are common areas to check if having issues in order creation in the Channel APi

<Accordion title="Use the correct channelLinkId" icon="fa-duotone fa-solid fa-link">
  Each location is connected to your test channel link with its own unique `channelLinkId`. When you create an order, make sure you include the correct `channelLinkId` in the URL.

  `https://api.staging.deliverect.com/channelname/order/channelLinkId`

  You can find a channel's `channelLinkId` by navigating to the **Locations** page of the customer account.


  <Image src="https://files.readme.io/90a6268-guide_ordersnotshowing_1_annotated.png" align="center" border={true} />

</Accordion>

<Accordion title="Channel name/scope and authorization errors" icon="fa-duotone fa-solid fa-lock">
  Channels may include the wrong channel name in the URL when creating the order.

  `https://api.staging.deliverect.com/channelname/order/channelLinkId`

  The channel name or "scope" is provided with the welcome email together with the API credentials. As a rule of thumb, the channel name is one word and entirely lowercase. Include it in the request and match its case exactly.

  If the channel name or scope is incorrect, you'll receive the following error:

  ```json
    {"code":"Authorization error","description":"you're not allowed to send in orders"}
  ```
</Accordion>

<Accordion title="403 Forbidden" icon="fa-duotone fa-solid fa-server">
  If below error is retutned, check the correct environment base URL is used.

  - Staging environment: [api.staging.deliverect.com]()
  - Production environment: [api.deliverect.com]()

  ```json 403 - insufficient_permissions
  {
      "code": "insufficient_permissions",
      "description": "Not allowed to access this channelLink."
  }

  ```
</Accordion>

<Accordion title="Orders not appearing, although showing 201 Created" icon="fa-duotone fa-solid fa-magnifying-glass">
  Check your `pickUpTime`, which controls the date range selector format on the Orders page. When creating the order, ensure the `pickUpTime` value is either:

  - the current time if the order is ASAP.
  - a future time if the order is in the future.

  Orders are filtered by `pickUpTime`, so an order won't be visible on the Orders page if this value is in the past — you'd need to select that past date to find it. For example, if you use the sample date `"2020-03-09T17:17:38Z"`, select March 9th 2020 to see your order.

  Also use a unique order ID. Orders with duplicate IDs are hidden as duplicates and are not viewable in the system.
</Accordion>

<Accordion title="Orders are failing" icon="fa-duotone fa-solid fa-triangle-exclamation">
  Check the order failure message. View it by [going to the Orders page](https://help.deliverect.com/en/articles/7979013-view-orders) of your test customer account. If you see an invalid PLU (price look-up code) error, use the correct PLUs for your products.
</Accordion>
