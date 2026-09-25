---
title: How to create a Group Order
deprecated: false
hidden: false
icon: fad fa-book-open-lines
metadata:
  robots: index
---
## User Role

Group baskets require a single 'Host' identified with `"role": "host"` and all other participants marked as `"role":"guest.`

### Group Policies

Pre-defined configuration policies can be attached to the group basket as detailed in the table below;

| Policy                                                              | Behaviour                                                                                   | Scope    |
| :------------------------------------------------------------------ | :------------------------------------------------------------------------------------------ | :------- |
| New Joiners Deadline (**newJoinersDeadline**)                       | Defines the cutoff time after which no new customers can be added to the group.             | Basket   |
| Items Modification Deadline (**groupItemsModificationDeadline**)    | Defines the cutoff time after which customers can no longer modify their items.             | Basket   |
| Items Modification Deadline (**customerItemsModificationDeadline**) | Defines the cutoff time after which a particular customer can no longer modify their items. | Customer |

<br />

<br />
