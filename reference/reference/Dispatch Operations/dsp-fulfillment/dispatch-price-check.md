---
api:
  file: fulfilment.json
  operationId: pricecheck
hidden: true
---
## Purpose

This endpoint is used in conjunction with a setting on the Deliverect platform that will both confirm the validity of the dispatch validationID or if required provide a new validationID before proceeding to Delivery Creation in your basket while also informing you of the Delivery Fee to charge your user based on the aforementioned settings on the Deliverect platform. This enables platforms to bridge the gap between validating the customer delivery location when entering your platform and accepting payment for a delivery job while reducing the need for further logic on your platform to calculate the delivery fee. This is an optional endpoint