---
title: Overview
deprecated: false
hidden: false
icon: fad fa-book-open-lines
metadata:
  robots: index
---
<br />

<SignUp />

## Build a Loyalty integration

Follow these steps to start using the loyalty API:

<HTMLBlock>{`
<div class="step-list">
  <div class="step-list-item">
    <div class="step-list-marker">1</div>
    <div class="step-list-content">
      <p class="step-list-title"><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/loyalty_registration">Register Loyalty Partner</a></p>
      <p class="step-list-desc">See guide here on how to connect a loyalty provider.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">2</div>
    <div class="step-list-content">
      <p class="step-list-title"><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/loyalty_get_customer">GET Loyalty Customer</a></p>
      <p class="step-list-desc">In case a customer does not exist, <a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/loyalty-partner-create-customer">create a new loyalty customer</a>.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">3</div>
    <div class="step-list-content">
      <p class="step-list-title"><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/loyalty_get_wallet">GET Loyalty Customer Wallet</a></p>
      <p class="step-list-desc">It retrieves the loyalty points and cash amount for a customer.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">4</div>
    <div class="step-list-content">
      <p class="step-list-title"><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/loyalty_tiers">GET Loyalty Tiers</a> — <em>Optional</em></p>
      <p class="step-list-desc">It retrieves the available loyalty tiers for the configured merchant account.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">5</div>
    <div class="step-list-content">
      <p class="step-list-title"><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/loyalty-partner-get-programs">Get Loyalty Programs</a></p>
      <p class="step-list-desc">At least 1 type of program is required.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">6</div>
    <div class="step-list-content">
      <p class="step-list-title"><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/loyalty-partner-order">Create Loyalty Order</a></p>
      <p class="step-list-desc"></p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">7</div>
    <div class="step-list-content">
      <p class="step-list-title"><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/loyalty-partner-cancel-order">Cancel Loyalty Order</a></p>
      <p class="step-list-desc"></p>
    </div>
  </div>
</div>
`}</HTMLBlock>
