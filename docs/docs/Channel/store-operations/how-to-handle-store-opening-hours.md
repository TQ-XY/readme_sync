---
title: How to handle Store Availability
deprecated: false
hidden: false
metadata:
  robots: index
---
## Introduction

A store's normal business hours are communicated via the `"availabilities"` array in the menu payload.

## Format

Each object in the `"availabilities"` array will specify a period of store availability as in example below;

```json Availabilities Example
"availabilities": [
 {
    "dayOfWeek": 1,
    "startTime": "13:00",
    "endTime": "21:30"
 }
```

### Request Body

| Field       | Use                                                                                                            | Type    |
| :---------- | :------------------------------------------------------------------------------------------------------------- | :------ |
| `dayOfWeek` | An integer value that indicates the day of the week for this availability (starting at 1 for Monday).          | integer |
| `startTime` | A 24-hour HH:MM format notation of the start time of availability expressed in the local time of the location. | string  |
| `endTime`   | A 24-hour HH:MM format notation of the end time of availability expressed in the local time of the location.   | string  |

| Day of week | Integer value |
| :---------- | :------------ |
| Monday      | `1`           |
| Tuesday     | `2`           |
| Wednesday   | `3`           |
| Thursday    | `4`           |
| Friday      | `5`           |
| Saturday    | `6`           |
| Sunday      | `7`           |

<br />

### Example - multiple time slots per day

Multiple non-overlapping periods can be specified per day as shown in the example below e.g. Saturday's availability (`"dayOfWeek": 6`) has two periods in the day where the store will be open;

```json Availabilities
"availabilities": [
    {
        "dayOfWeek": 1,
        "endTime": "17:00",
        "startTime": "09:00"
    },
    {
        "dayOfWeek": 2,
        "endTime": "17:00",
        "startTime": "09:00"
    },
    {
        "dayOfWeek": 3,
        "endTime": "17:00",
        "startTime": "09:00"
    },
    {
        "dayOfWeek": 4,
        "endTime": "17:00",
        "startTime": "09:00"
    },
    {
        "dayOfWeek": 5,
        "endTime": "17:00",
        "startTime": "09:00"
    },
    {
        "dayOfWeek": 6,
        "endTime": "17:00",
        "startTime": "09:00"
    },
    {
        "dayOfWeek": 6,
        "endTime": "22:00",
        "startTime": "19:00"
    },
    {
        "dayOfWeek": 7,
        "endTime": "17:00",
        "startTime": "09:00"
    }
],
```

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Store Availabilty Messaging</strong><br>
Menu <code>"availabilities"</code> reflect normal operating hours per store. Outside of operating hours, stores can be closed temporarily via <a href="https://developers.deliverect.com/reference/post-busy-mode">Busy Mode</a>.

Customers should clearly see whether ordering is unavailable due to being outside opening hours or if a temporary closure applies.
  </p>
</div>
`}</HTMLBlock>
