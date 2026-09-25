---
title: 'How to connect a Gift Card provider to Deliverect Direct  '
deprecated: false
hidden: false
metadata:
  robots: index
---
## Register a new Gift Card provider

Deliverect will call the register Gift Card Profile URL when a merchant starts configuring gift card services in Deliverect.  Go to the "Gift Cards" tab > "Configuration" to register a new profile.

<Image align="center" border={true} width="700px" src="https://files.readme.io/c4c4503978fbf6b0b599bfa962dd8289e1b4df3475047c9fe9af7f47e7b20beb-GiftCard-Configuration.png" className="border" />

Click on "Add" at the top to register a new provider.

<Image align="center" border={false} src="https://files.readme.io/732983b3bac1f88207521b2bedc03b96d18eff9f04a78be2756ab8ed7e20885c-Generic_Gift_Card_copy.png" />

<Image border={false} />

Add a registration URL and the API Key and click on "install". The API response must contain the Redeem, Reverse and Balance URLs needed for the integration as explained on the [Register Gift Card API documentation.](https://developers.deliverect.com/reference/giftcards_webhooks_register)

<br />

<Image align="center" border={true} width="500px" src="https://files.readme.io/3e37c019acbe80d86abe44faf354c9880b3df0e9731fac7a017100da83679725-Screenshot_2026-01-15_at_12.28.19.png" className="border" />

<br />

### Linking the Provider to a specific Channel

After registering the profile, select a location & link it to the Deliverect Online Ordering Channel on the account by clicking on the  "Link" button.

<Image align="center" border={true} width="500px" src="https://files.readme.io/bb0fad279c8ac8c40ee1ba6d2ac3769525defc4e0051638496939838469c4367-Screenshot_2026-01-15_at_12.46.43.png" className="border" />

<br />

<br />