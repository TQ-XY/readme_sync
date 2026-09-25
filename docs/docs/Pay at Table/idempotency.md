---
title: Idempotency
deprecated: false
hidden: true
icon: fad fa-book-open-lines
metadata:
  robots: index
---
Use an idempotency key when you post a payment to a bill so duplicate requests are not processed successfully more than once.

The [Post Payment to Bill](https://developers.deliverect.com/reference/post-payment-to-bill) endpoint requires the `Idempotency-Key` header.

```text Headers
Idempotency-Key: UUIDv4
accept: application/json
authorization: Bearer
```

Set `Idempotency-Key` to a string value. We recommend using a [UUIDv4](https://en.wikipedia.org/wiki/Universally_unique_identifier#Version_4_\(random\)).

When Deliverect receives a request with a specific idempotency key, we process the requested operation successfully only once.

If you send another request with the same idempotency key, Deliverect returns an error message that the idempotency key is already used. You will also receive the corresponding payment feedback event in your webhook

<br />