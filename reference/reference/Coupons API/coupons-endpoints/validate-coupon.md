---
api:
  file: coupon.json
  operationId: post_coupons-accountid-channel-channellinkid-coupons-couponcode-validate-1
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
:warning: This endpoint is deprecated. Please use [validate coupons.](https://developers.deliverect.com/v3.0-ordering-experience/update/reference/validate-coupons)

## Purpose

After performing the validation, if the response was successful (status code 200), the channel needs to call the `PATCH Update Basket - Discounts` endpoint, using the following pattern:

<br />

```json
[
  {
      "externalId": "coupon code",
      "provider": "coupon",
      "type": "order_flat_off",
      "value": 1234,
      "name": "coupon description"
  }
]
```

Response

```json
{
  "discounts": [
    {
      "offer": {
        "type": "flat_off",
        "value": 1000,
        "currency": "EUR",
        "display": "10.00"
      },
      "scope": {
        "type": "order"
      },
      "provider": "coupon",
      "externalId": "SUMMER",
      "name": ""
    }
  ],
  "description": "",
  "code": "SUMMER"
}
```