---
api:
  file: channel.json
  operationId: order-delivery-update
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
A status update for an order happens when a delivery partner performs an action on that order.<br />Each incoming status update should be confirmed with an HTTP status `200`.

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
    Delivery Updates from Dispatch Partners
  </p>
  <p style="
    margin: 0;
    color: #2e5934;
    font-size: 15px;
    line-height: 1.6;
  ">
    This endpoint will only return results when there is a registered Dispatch partner that has integrated with our Dispatch API and is connected to the customer (restaurant, food business) account.
    It does not return results from channel partners that may also deliver the orders.
  </p>
</div>
`}</HTMLBlock>

The table below lists statuses and their corresponding integer value.

| Deliverect status tag | Description            | Integer value |
| :-------------------- | :--------------------- | :------------ |
| READY FOR PICKUP      | ready for pickup       | 70            |
| IN DELIVERY           | en route to customer   | 80            |
| FINALIZED             | delivered              | 90            |
| CANCEL                | should be voided       | 100           |
| CANCELED              | has been voided on POS | 110           |
| FAILED                | failed                 | 120           |
| PARSE FAILED          | parsing failed         | 124           |

<Callout icon="🚧" theme="warn">
  ###

  `FINALIZED` means that the order is finalized in the POS. However, this doesn't necessarily mean that the food has been delivered to the end customer.
</Callout>

<br />