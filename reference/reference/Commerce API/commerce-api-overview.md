---
title: Overview
deprecated: false
hidden: false
icon: fad fa-book-open-lines
metadata:
  robots: index
next:
  pages:
    - slug: commerce-endpoints
      title: Endpoints
      type: endpoint
    - slug: commerce-webhooks
      title: Webhooks
      type: endpoint
---
## Overview

Below is a high-level overview of the key Commerce API interactions, with a brief description of the role they play in supporting the complete ordering journey from store discovery through to POS order injection;

<HTMLBlock>{`
<div class="step-list">
  <div class="step-list-item">
    <div class="step-list-marker step-list-marker--green">1</div>
    <div class="step-list-content">
      <p class="step-list-title">Get an Access Token — <a href="https://developers.deliverect.com/reference/access-token" target="_blank">Get Access Token</a></p>
      <p class="step-list-desc">Retrieve a token granting you access to our endpoints.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker step-list-marker--green">2</div>
    <div class="step-list-content">
      <p class="step-list-title">Retrieve Linked Customer Accounts — <a href="https://developers.deliverect.com/v1.1-restaurants/reference/get-linked-accounts" target="_blank">Get Linked Accounts</a></p>
      <p class="step-list-desc">Retrieve the customer accounts linked to your partner account.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker step-list-marker--green">3</div>
    <div class="step-list-content">
      <p class="step-list-title">Get Stores — <a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/commerce-get-stores" >Get Stores</a></p>
      <p class="step-list-desc">Retrieve the <code>channelLinkId</code> for a customer account.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker step-list-marker--green">4</div>
    <div class="step-list-content">
      <p class="step-list-title">Get Store Menu(s) — <a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/commerce-get-menus" >Get Store Menu(s)</a></p>
      <p class="step-list-desc">Retrieve menus for a given store.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker step-list-marker--green">5</div>
    <div class="step-list-content">
      <p class="step-list-title">Create Basket — <a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/commerce-create-basket" >Create Basket</a></p>
      <p class="step-list-desc">Create a basket to begin building the order.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker step-list-marker--green">6</div>
    <div class="step-list-content">
      <p class="step-list-title">Update Basket (optional)</p>
      <p class="step-list-desc">Update the basket as needed using the following endpoints:</p>
      <ul class="step-list-sublist">
        <li><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/update-basket-customer" >Update Customer</a></li>
        <li><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/update-basket-items" >Update Items</a></li>
        <li><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/commerce-update-basket-discounts" >Update Discounts</a></li>
        <li><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/update-basket-fulfillment" >Update Fulfillment</a></li><li><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/update-basket-charges" >Update Charges</a></li>
        <li><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/update-basket-payments" >Update Tips</a></li>
        <li><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/update-donations" >Update Donations</a></li>
      </ul>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker step-list-marker--green">7</div>
    <div class="step-list-content">
      <p class="step-list-title">Request Payment (optional) — <a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/request-payment" >Request Payment</a></p>
      <p class="step-list-desc">Only applies for DPAY (Deliverect Pay) payment type.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker step-list-marker--green">8</div>
    <div class="step-list-content">
      <p class="step-list-title">Checkout — <a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/commerce-checkout" >Basket Checkout</a></p>
      <p class="step-list-desc">Proceed to checkout and specify the payment method.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker step-list-marker--green">9</div>
    <div class="step-list-content">
      <p class="step-list-title">Checkout Status Webhook — <a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/commerce-api-checkout-update" >Basket Checkout Status Webhook</a></p>
      <p class="step-list-desc">Monitor the status of the checkout.</p>
    </div>
  </div>
</div>
`}</HTMLBlock>

<Cards>
  <Card title="Flow Diagram" href="https://developers.deliverect.com/page/commerce-api-flow-diagram" icon="fad fa-diagram-project">
    Visualise the complete Commerce order flow, from retrieving store details to processing orders in checkout
  </Card>

  <Card title="Guides" href="https://developers.deliverect.com/v3.0-ordering-experience/docs/commerce-guide-overview" icon="fad fa-book">
    Step-by-step guidance for integrating your ordering platform with our Commerce API
  </Card>

  <Card title="Partners" href="https://www.deliverect.com/integrations/loyalty" icon="fad fa-handshake" target="_blank">
    Explore our network of **dispatch**, **loyalty** and **payment** partners to enhance the ordering experience
  </Card>
</Cards>

<br />

<br />
