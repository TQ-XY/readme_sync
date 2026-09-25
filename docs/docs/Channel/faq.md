---
title: FAQ
deprecated: false
hidden: false
icon: fad fa-comment-question
metadata:
  robots: index
---
###

<Accordion title="What is a channel?" icon="fad fa-question">
  Channels are online stores that allow customers to place orders. They are connected to Deliverect and allow for the transmission of orders.
</Accordion>

<Accordion title="What is the purpose of a channel link ID?" icon="fad fa-question">
  A channel link ID is unique to a channel. When building an integration to send orders to a customer location in Deliverect, we provide you with a test channel in our staging environment. Reference your test channel by that unique ID to form part of the dispatch delivery order endpoint.
</Accordion>

<Accordion title="How do I retrieve the channel link Id?" icon="fad fa-question">
  We send the channel link ID via the [Channel Registration](ref:channel_register) webhook which is called when the channel is registered

  The external location ID (`locationId`) is also provided. This is the unique ID of the customer on your platform.
</Accordion>

<Accordion title="What is the purpose of a Scope?" icon="fad fa-question">
  A Channel Scope or \{\{channelName\}\} is provided for ordering integrations. The scope will be used in the [[Create / Cancel Order](ref:create-channel-order)]() endpoint. The scope will remain valid unless revoked and when provided should be hard coded in an integration.
</Accordion>
