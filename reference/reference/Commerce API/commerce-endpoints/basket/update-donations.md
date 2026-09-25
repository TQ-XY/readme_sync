---
api:
  file: commerce.json
  operationId: patch_commerce-accountid-baskets-basketid-donations
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
## Donations

When applying a donation a unique `externalId` can be used , which can be a specific PLU in the POS related to donations.

```json Donation Example
{
  [
    {
      "externalId": "1234",
      "amount": 200
    }
  ]
}
```

<br />

<br />