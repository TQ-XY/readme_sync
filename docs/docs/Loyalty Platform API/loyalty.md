---
title: How to test Loyalty Programs
deprecated: false
hidden: false
metadata:
  robots: index
---
## Introduction

A Loyalty platform should integrate the [Get Loyalty Programs](ref:loyalty-channel-get-programs) webhook to ensure channels integrated with Loyalty are able to retrieve a list of loyalty programs available to a specific customer&#x20;

## Testing

In order to test whether the applied programs are correct, these will be displayed in test accounts provisioned for two Deliverect product 'Deliverect Direct' and 'Kiosk' as folllows.

<br />

### Deliverect Direct

Clicking on the points returned within `points.balance` will return the list of available programs


<Image src="https://files.readme.io/9dd4e18d959de1ef7f3650856b30cfe22b54465a33092197f5837912cdec9bda-Screenshot_2026-02-10_at_14.23.43.png" align="center" width="400px" border={true} />



<Image src="https://files.readme.io/9a347212c1121b8a9924a23b57f4ef5751dff9ec619a2fbef6b7b17d3c65c0ec-Screenshot_2026-02-10_at_14.44.24.png" align="center" width="400px" border={true} />


<br />

### Deliverect Kiosk

Clicking on 'My Loyalty' will display the rewards as in below screenshot;


<Image src="https://files.readme.io/aaa028abff030c26214fae34896ee65b489bccc7265a484ac21f8a7d0f3c01df-Screenshot_2026-04-15_at_09.14.30.png" align="center" border={true} />
