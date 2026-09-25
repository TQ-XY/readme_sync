---
api:
  file: commerce.json
  operationId: commerce-channel-api-baskets-update-basket-fulfillment
hidden: false
---
## Purpose

Modify the fulfilment type and its associated parameters and/or update the requested fulfilment time.

## Fulfillment Types:

| Type       | Definition                                                         |
| :--------- | :----------------------------------------------------------------- |
| `delivery` | Commerce platform will be arranging delivery                       |
| `pickup`   | Will be collected i.e. for takeaway (can apply for Kiosk orders)   |
| `curbside` | Will be as per pickup, but specific handoff to customer in vehicle |
| `eat-in`   | Customer will be ordering on-premise e.g. QR Code ordering         |

## Parameters:

Aside from the `"type"` being updated, below shows specific parameters expected when updating each fulfillment type. All required attributes are marked with *

### Delivery

| Parameter             | Meaning                                | Type             |
| :-------------------- | :------------------------------------- | :--------------- |
| `time`                | The intended pickup time for the order | string           |
| address.`line`        | Full address in single line            | string           |
| address.`coordinates` | Geo-location, expressed as [lat, lon]  | array [lat, lon] |

#### Example Request

```json delivery example
{
    "type": "delivery",
    "time": "2024-01-15T10:00",
    "address": {
        "line": "5030 W Lovers Ln, Dallas, TX 75209, US",
        "coordinates": [
            32.850713,
            -96.828014
        ],
        "note": "first floor, left door, happy dog"
    }
}
```

### **Pickup**

| Parameter     | Meaning                                                                                       | Type   |
| :------------ | :-------------------------------------------------------------------------------------------- | :----- |
| `time`        | The intended pickup time for the order                                                        | string |
| `pickupNotes` | Special instructions from the customer on their Pickup order e.g. pager numbers/table numbers | string |

#### Example Request

```json pickup example
  {
      "type": "pickup",
      "time": "2024-01-15T10:00",
      "pickupNotes":"Table number 7"
  }
```

### **Curbside**

| Parameter     | Meaning                                                                                            | Type   |
| :------------ | :------------------------------------------------------------------------------------------------- | :----- |
| `pickupNotes` | Special instructions from the customer on their Curbside order e.g. Car moderl/colour/registration | string |

#### Example Request

```json curbside example
  {
      "type": "curbside",,
      "pickupNotes":"Yellow Honda"
  }
```

**Eat-In**

| Parameter | Meaning                                                                       | Type   |
| :-------- | :---------------------------------------------------------------------------- | :----- |
| `spot`    | Specific location in the venue e.g. the table number or position at a counter | string |

```json eatIn example
  {
      "type": "eatIn",
      "spot": "table 2"
  }
```