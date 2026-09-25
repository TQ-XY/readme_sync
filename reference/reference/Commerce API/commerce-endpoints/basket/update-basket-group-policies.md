---
api:
  file: commerce.json
  operationId: patch_commerce-accountid-baskets-basketid-group-policies
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
### Purpose

Update the group order basket policies.

## Policies

Pre-defined policies configuration that can be attached to the group basket.

| Policy                                                             | Behaviour                                                                                   | Scope    |
| :----------------------------------------------------------------- | :------------------------------------------------------------------------------------------ | :------- |
| New Joiners Deadline (**newJoinersDeadline**)                      | Defines the cutoff time after which no new customers can be added to the group.             | Basket   |
| Items Modification Deadline (**groupItemsModificationDeadline**)   | Defines the cutoff time after which customers can no longer modify their items.             | Basket   |
| Items Modification Deadline (**customerItemsModificationDeadline** | Defines the cutoff time after which a particular customer can no longer modify their items. | Customer |