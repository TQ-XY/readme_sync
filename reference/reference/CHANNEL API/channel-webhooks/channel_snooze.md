---
api:
  file: channel_webhooks.json
  operationId: channel_snooze
hidden: false
---
## Overview

When customers want to make one or more products or modifiers temporarily unavailable online, they will action a **'Snooze'** request to prevent the item being ordered for a certain period of time. This would typically be a response to items going out of stock.&#x20;

## Format

Both **Snooze** and **Unsnooze** events will be communicated to all channels hosting a menu containing the snoozed items.&#x20;

### Unsnoozing

When the snooze timeframe lapses, or if the snoozed status is removed manually, items will be **'Unsnoozed'&#x20;**&#x61;utomaticall&#x79;**. Channels should therefore&#x20;**&#x61;nticipate that items can become unsnoozed at any time before the originally specified snooze period ends.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Snoozed Items on Active Menus Only</strong><br>
    Only when a menu is published successfully to a channel, will snooze events be triggered for items contained in the menu.
  </p>
</div>
`}</HTMLBlock>

## Response

The intended purpose of snoozing a product is that it will no longer be available for a specified time period. As such, there is a need for this snoozed state to be clear on the customer facing menu. Two UI details that are commonly applied as follows;

- **Items in view but clearly marked unavailable** - a snoozed item can be visible but not available to select e.g. by greying out the product image.
- **Showing estimated unsnooze time** - as snooze requests contain the intended length of time for an item to be unavailable, it is therefore possible to show an estimate of when the product will become available again.

If your channel does not support the above suggested UI for displaying snoozed products, removing them from view altogether will achieve the same intended outcome.

## Request format

When one or more products are snoozed or unsnoozed, you can expect the request format shown below to be delivered to your specified webhook.

```json Snooze Products
{
    "accountId": "5b****71c6489f0029****d4",
    "locationId": "5c****ecc6489f0001****b8",
    "channelLinkId": "5e****abc11dec0001****9b",
    "operations": [
        {
            "action": "snooze",
            "data": {
                "items": [
                    {
                        "plu": "PIE1",
                        "snoozeStart": "2020-03-24T16:21:54.955000Z",
                        "snoozeEnd": "2020-03-24T22:21:54.955000Z"
                    }
                ]
            },
            "allSnoozedItems": [
                {
                    "plu": "PIE1",
                    "snoozeStart": "2020-03-24T16:21:54.955000Z",
                    "snoozeEnd": "2020-03-24T22:21:54.955000Z"
                },
                {
                    "plu": "MSB1",
                    "snoozeStart": "2020-03-24T16:21:54.955000Z",
                    "snoozeEnd": "2020-03-24T22:21:54.955000Z"
                }
            ]
        }
    ]
}
```
```json Unsnooze Products
{
    "accountId": "5b****71c6489f0029****d4",
    "locationId": "5c****ecc6489f0001****b8",
    "channelLinkId": "5e****abc11dec0001****9b",
    "operations": [
        {
            "action": "unsnooze",
            "data": {
                "items": [
                    {
                        "plu": "PIE1",
                        "snoozeStart": "2020-03-24T16:21:54.955000Z",
                        "snoozeEnd": "2020-03-24T22:21:54.955000Z"
                    },
                    {
                        "plu": "MSB1",
                        "snoozeStart": "2020-03-24T16:21:54.955000Z",
                        "snoozeEnd": "2020-03-24T22:21:54.955000Z"
                    }
                ],
                "allSnoozedItems": []
            }
        }
    ]
}
```

|                   |                                                                                                                                                                                                                                                                                                                                              |     |
| :---------------- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :-- |
| `accountId`       | The ID of the customer account                                                                                                                                                                                                                                                                                                               | str |
| `locationId`      | The ID of a specific location in the customer account                                                                                                                                                                                                                                                                                        | str |
| `channelLinkId`   | The unique id of the store on the channel platform                                                                                                                                                                                                                                                                                           | str |
| `action`          | `"snooze"` or `"unsnooze"`                                                                                                                                                                                                                                                                                                                   | str |
| `data.items`      | a list of items showing the period during which they each should be snoozed                                                                                                                                                                                                                                                                  |     |
| `plu`             | The items should be snoozed based on the PLU.                                                                                                                                                                                                                                                                                                | str |
| `snoozeStart`     | When snooze status should begin, timestamp is in UTC `yyyy-MM-ddTHH:mm:ssZ`                                                                                                                                                                                                                                                                  | str |
| `snoozeEnd`       | When snooze status should end, timestamp is in UTC `yyyy-MM-ddTHH:mm:ssZ`                                                                                                                                                                                                                                                                    | str |
| `allSnoozedItems` | Each time you receive a snooze request for your channel, you will also receive the complete list of all items (`allSnoozedItems`) that should currently be in a snoozed state i.e. all previously snoozed items included will be included with each request. This additional list of items can be disabled if required via Channel settings. |     |