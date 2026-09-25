---
api:
  file: dispatch.json
  operationId: put_fulfillment-hetaupdate-dspname-locationid
hidden: true
link:
  new_tab: false
metadata:
  robots: index
---
## Purpose

This endpoint allows providing an estimated arrival time of a driver on a given location.

It should be updated each time there is a relevant change from the last provided hypothetical estimated time of arrival.

```json Hypothetical Estimated Time of Arrival
[
    {
        "heta": 900
    }
]
```

<HTMLBlock>{`
<div style="
  background-color: #fff8e1;
  border: 1px solid #ffcc80;
  border-radius: 12px;
  padding: 20px 24px;
  margin: 16px 0;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
">
  <p style="
    margin: 0;
    color: #8d4e00;
    font-weight: 700;
    font-size: 16px;
    display: flex;
    align-items: center;
    gap: 8px;
  ">
    <span style="font-size: 18px;">⚠️</span>
    The hypothetical estimated time of arrival should be provided in seconds.
  </p>
</div>

<br />
`}</HTMLBlock>

<br />
