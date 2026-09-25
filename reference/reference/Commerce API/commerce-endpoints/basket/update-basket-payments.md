---
api:
  file: commerce.json
  operationId: patch_commerce-accountid-baskets-basketid-payment
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
## Tip types:

| Type       | String Value |
| :--------- | :----------- |
| Restaurant | restaurant   |
| Driver     | driver       |

```json Tips - Restaurant
{
  "tips": [
    {
      "amount": 100,
      "type": "restaurant"
    }
  ]
}
```
```json Tips - Driver
{
  "tips": [
    {
      "amount": 100,
      "type": "driver"
    }
  ]
}
```

<br />

<br />