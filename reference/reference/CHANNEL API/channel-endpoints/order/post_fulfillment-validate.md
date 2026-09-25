---
api:
  file: channel.json
  operationId: post_fulfillment-validate
hidden: false
link:
  new_tab: false
---
## Purpose

Pre-validate if an integrated Dispatch partner has available couriers to handle a delivery before placing an order. This enables platforms without their own delivery integrations to route orders through Deliverect’s Dispatch network.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Dispatch Integration Required</strong><br>
      a Dispatch provider needs to be integrated within a customer location for this endpoint to return courier availability.
  </p>
</div>
`}</HTMLBlock>

## Validation Id

A successful response where `"available": true,` will also include a`"validationId"` which is a unique ID (valid for 10 minutes) to be used when creating an order

Include the `validationId` in the [Create / Cancel Order](ref:create-channel-order) or [Checkout](doc:checkout) request

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>

    When applying the  <code>validationId</code> to an order, 
    <strong>the originally validated address</strong> will be applied. To update to a new address, set
    <code>validationId</code> to <code>null</code> to trigger a new validation with the Dispatch provider.
  </p>
</div>
`}</HTMLBlock>

## Check availability for multiple stores

An array of `channelLinkIds` can be provided to determine the best possible pickup location for a specific delivery, based on price and distance.

In the examples on the right hand side, see **"Dispatch Availability - Multiple Locations"** where two stores are checked by their unique store identifier <Glossary>channelLinkId</Glossary> and the response **"Offers Available - Multiple Stores"** confirms the best pickup location to set for the order

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>When providing the array  <code>channelLinkIds</code> , the <code>"channelLinkId"</code> field will be disregarded
  </p>
</div>
`}</HTMLBlock>

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>

    A <code>200</code>response only confirms that your request was successful; it does not confirm Dispatch availability.
    Always check the <code>available</code> flag in the response.
  </p>
</div>
`}</HTMLBlock>
