---
title: specifications
deprecated: false
hidden: true
icon: fad fa-book-open-lines
metadata:
  robots: index
---
Use these specifications to identify the Deliverect Dine-In Payment API contact details, URI scheme, tags, and payment path.

## Contact information

**Contact email:** [frederik.cornil@deliverect.com](mailto:frederik.cornil@deliverect.com)

## License information

**Terms of service:** [Deliverect developer terms](http://developers.deliverect.com/)

## URI scheme

| Field | Value |
| --- | --- |
| Host | `developers.deliverect.com` |
| Base path | `/` |
| Scheme | HTTPS |

## Tags

| Tag | Description |
| --- | --- |
| `orders` | Operations related to orders |
| `receipts` | Operations related to receipts |
| `tables` | Operations related to tables |

## Paths

Send a payment for a Deliverect order.

```http
POST /channellinks/{clId}/orders/{channelOrderId}/payments
```