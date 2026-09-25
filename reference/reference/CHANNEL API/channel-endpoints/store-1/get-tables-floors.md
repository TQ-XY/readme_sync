---
api:
  file: channel.json
  operationId: get_tables-locationid
hidden: false
---
## Purpose

Retrieve the tables and floors configured in the customers POS for a specific location

### Example Response

```json Example Response
{
  "tables": [
    {
      "id": "89302",
      "name": "T5",
      "floorId": "10",
      "seats": 4,
      "type": "unknown"
    },
    {
      "id": "89204",
      "name": "B2",
      "seats": 2,
      "floorId": "11",
      "type": "unknown"
    }
  ],
  "floors": [
    {
      "id": "10",
      "name": "Top Floor"
    },
    {
      "id": "11",
      "name": "Bottom Floor"
    }
  ]
}
```