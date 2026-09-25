---
title: How to apply a Gift card to an order
deprecated: false
hidden: false
metadata:
  robots: index
---
Select the option add Gift Card on the basket checkout from the online ordering store.


<Image src="https://files.readme.io/63fc38c02882c056516299e6e6f218bb87b5801645c3c6b18179188fc1a3dc37-Basket_checkout.png" align="center" width="350px" border={true} />


Enter the Gift Card details and click on "apply gift card"; a call will be triggered to the configured [GET Balance webhook URL]().


<Image src="https://files.readme.io/cac923f1adf8113b0d32ca541af021c863642c553693552b3ab5a7968d19db19-Add_gift_card.png" align="center" width="500px" border={true} />


The body of the request will contain  the following information matching the data introduced

* Gift Card code = `giftCardNumber `
* PIN= `giftCardVerificationCode `

```json Get Balance
{giftCardNumber: "61234567",
 giftCardVerificationCode: "123"}
```

The expected response should contain the `giftCardNumber` and the `amount.` The balance amount paid should be sent as an integer with 2 decimal digits, for example, 1 euro would be sent as 100.

```json Gift Card provider response
{
  "giftCardNumber": "61234567",
  "amount": 1000
}
```

<Callout icon="⚠️" theme="warn">
  The amount entered manually during online ordering must not exceed the available balance returned in the response
</Callout>

### Redeem the gift card value

After the order is checked out, the configured [Redeem value webhook URL](https://developers.deliverect.com/v3.0-ordering-experience/reference/giftcards_redeem) will be called.

The payload includes the gift card details entered by the user when they applied the gift card.


<Image src="https://files.readme.io/d30e16ff09eeb934d06c7fec7f8207017c302fe6513035d4a54fbd983d46a17c-checkoutbasket.png" align="center" width="400px" border={true} />


```json Redeem value
{
    "giftCardNumber": "12547634**06",
    "giftCardVerificationCode": "12**",
    "amount": 100
}
```

### Reverse the gift card redemption

The [Reverse redeem webhook URL](https://developers.deliverect.com/v3.0-ordering-experience/reference/giftcards_reverse) will be triggered  to reverse a gift card redemption when an order that includes a gift card payment is cancelled.
