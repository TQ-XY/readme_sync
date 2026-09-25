---
title: Eat-in Orders
deprecated: false
hidden: false
icon: fad fa-qrcode-read
metadata:
  robots: index
---
## Introduction

Use `orderType` and `table` to create an eat-in order that includes the table number for restaurant staff.

**Eat in** means a customer consumes the order at the location. Add a table number so staff know where to serve the order.

Set these fields in the order payload:

- To set the order type, use `"orderType": 3`. The value `3` identifies an eat-in order.
- &#x20;To include the table number, use `"table": "Table 5"`.

```json Order Type: Eat In
"orderType": 3,
"table": "1"
```

Deliverect shows the table number and sends it to the POS (point-of-sale system) in the order notes.


<Image src="https://files.readme.io/d8e7d55-guide_eatin_1.jpg" align="center" border={true} />


## Automatically open an order on a POS table

Adding a table number won't open the order on that table in the POS. A direct table integration requires the table ID. Use the [GET POS Tables from Location endpoint](https://developers.deliverect.com/reference/get-pos-tables-from-location) to get the table ID for a location.

<HTMLBlock>{`
<div class="callout-banner callout-banner--important">
  <span class="callout-icon"><i class="fa-regular fa-triangle-exclamation"></i></span>
  <p><strong>Limited Support</strong><br>
 Not all POS systems currently return the table IDs
</div>
`}</HTMLBlock>