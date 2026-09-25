---
api:
  file: channel_webhooks.json
  operationId: channel_busy_mode
hidden: false
---
## Purpose

When a store is busy it may choose to restrict the flow of incoming orders either by **temporarily pausing their store** or by **increasing the expected pickup time of orders**. These events are sent via the Busy Mode webhook and should initiate real time updates to a stores availability.

## Format

Busy mode events will specify the target store via it's unique <Glossary>channelLinkId</Glossary> together with one of three updated `status` detailed below.

| Status   | Meaning                                                                                                                                                                                   |
| :------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `PAUSED` | The store should be 'paused' and closed to online orders until further notification                                                                                                       |
| `BUSY`   | The store is currently busy and **ASAP orders should not be possible,&#x20;**&#x74;he specified `"delay"` in minutes should be clearly communicated to guests when processing new orders. |
| `ONLINE` | This is a request to disable busy mode. The store should be open as normal.                                                                                                               |

## Request

See below examples of busy mode events to expect;

```json PAUSED
{
    "accountId": "5b****71c6489f0029****d4",
    "locationId": "5c****ecc6489f0001****b8",
    "channelLinkId": "5e****abc11dec0001****9b",
    "status": "PAUSED"
}
```
```json ONLINE
{
    "accountId": "5b****71c6489f0029****d4",
    "locationId": "5c****ecc6489f0001****b8",
    "channelLinkId": "5e****abc11dec0001****9b",
    "status": "ONLINE"
}
```
```json BUSY
{
    "accountId": "61e14f0c888c8389fa5908bb",
    "locationId": "633d62de0f******f893bdf",
    "channelLinkId": "647618*******166c858de0b0",
    "status": "BUSY",
    "delay": 30
}
```

## Response

The response should indicate pausing or unpausing the store was successful with a `200 OK` status code. The body of the response should echo the current status of the store after having made the change ("PAUSED" , "ONLINE", "BUSY").&#x20;

```json Store Paused 200 OK
{
  "status": "PAUSED"
}
```
```json Store Online 200 OK
{
  "status": "ONLINE"
}
```
```json Store Busy 200 OK
{
  "status": "BUSY"
}
```

<br />