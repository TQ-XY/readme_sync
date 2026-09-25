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

## Build a dispatch integration

<HTMLBlock>{`
<div class="step-list">
  <div class="step-list-item">
    <div class="step-list-marker">1</div>
    <div class="step-list-content">
      <p class="step-list-title"><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/dispatch_webhooks">Configure Dispatch Webhooks</a></p>
      <p class="step-list-desc">Configure your Dispatch webhooks in Deliverect. A webhook is an HTTP callback that Deliverect sends to your integration when an event occurs.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">2</div>
    <div class="step-list-content">
      <p class="step-list-title">Create a Test Order</p>
      <p class="step-list-desc">Create a test order from Deliverect. This triggers a call to your configured <strong>Validate</strong> webhook.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">3</div>
    <div class="step-list-content">
      <p class="step-list-title">Respond to the Validate Webhook</p>
      <p class="step-list-desc">Return a response that includes <code>"canDeliver": true</code> only when your integration can deliver the order. Deliverect then calls your <a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/dispatch_create_job">Create webhook</a>.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">4</div>
    <div class="step-list-content">
      <p class="step-list-title">Process the Create Webhook</p>
      <p class="step-list-desc">Process the Create webhook payload from Deliverect and create the delivery job in your dispatch system.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">5</div>
    <div class="step-list-content">
      <p class="step-list-title"><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/update-delivery-job">Send Delivery Status Updates</a></p>
      <p class="step-list-desc">Use this endpoint to provide delivery status, pickup time, delivery time, and courier information.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">6</div>
    <div class="step-list-content">
      <p class="step-list-title"><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/delivery-job-cancel">Cancel Delivery</a> — <em>Optional</em></p>
      <p class="step-list-desc">If you need to cancel a delivery, send the cancellation with the reason documented in the endpoint reference.</p>
    </div>
  </div>
</div>
`}</HTMLBlock>

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>

    You can use the Delivery Manager App to test the order flow. <a href="https://developers.deliverect.com/v3.0-ordering-experience/docs/how-to-test-orders" target="_blank" rel="noopener noreferrer">Learn more</a>.
  </p>
</div>
`}</HTMLBlock>
