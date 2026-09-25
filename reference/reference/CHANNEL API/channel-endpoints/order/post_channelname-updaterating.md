---
api:
  file: channel.json
  operationId: post_channelname-updaterating
hidden: false
---
A generic channel integration can use this endpoint to update the rating for a previously placed order.

When sending a rating update, Deliverect will check if the party sending the order has the correct scope to be able to. If not, they are considered unauthorized. The scope for generic channels is communicated to integrating parties and is checked in the request target URL only. Therefore, make sure this URL correctly contains the scope.

For a payload, we always expect a JSON that contains:

* Channel order ID (`channelOrderId`)
* Date (in UTC) when order was placed in ISO 8601 format (`orderDate`)
* ID of the channel link (`channelLinkId`)
* Array of rating objects (`rating`)
  * Subject of the rating. See allowed values in **Rating Subjects** table below (`subject`)
  * Rating value from 0 to 10 (`rating`)
  * [Optional] Comment for the rating (`comment`)  
    *[Optional] Reason for negative rating. See allowed values in **Rating Reasons** table below (`reason`)

## Rating Subjects

| Subject               | Integer Value |
| :-------------------- | :------------ |
| Unknown               | 0             |
| Restaurant            | 1             |
| Delivery              | 2             |
| Order                 | 3             |
| Menu_Item             | 4             |
| Restaurant_By_Courier | 5             |

## Rating Reasons

| Reason           | Integer Value |
| :--------------- | :------------ |
| Item missing     | 1             |
| Order issue      | 2             |
| Order is wrong   | 3             |
| Food isn't fresh | 4             |
| Food is cold     | 5             |
| Box was opened   | 6             |
| Delivery late    | 7             |
| Delivery issue   | 8             |
| Rude staff       | 9             |
| No issues        | 10000         |