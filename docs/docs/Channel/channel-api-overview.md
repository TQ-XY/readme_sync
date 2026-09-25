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

## Build a channel integration

The steps to build a channel integration with Deliverect are as follows:

<HTMLBlock>{`
<div class="step-list">
  <div class="step-list-item">
    <div class="step-list-marker">1</div>
    <div class="step-list-content">
      <p class="step-list-title"><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/channel_register">Channel Registration Webhook URL</a></p>
      <p class="step-list-desc">Implement this webhook to allow registering or activating new channels. The response should include all the relevant webhooks for the integration.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">2</div>
    <div class="step-list-content">
      <p class="step-list-title"><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/channel_menu_update">Menu Push</a></p>
      <p class="step-list-desc">Implement Menu Push, including Menu Availabilities.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">3</div>
    <div class="step-list-content">
      <p class="step-list-title"><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/create-channel-order">Create Orders via Endpoint</a></p>
      <p class="step-list-desc"></p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">4</div>
    <div class="step-list-content">
      <p class="step-list-title"><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/channel_order_status">Order Status Webhook URL</a></p>
      <p class="step-list-desc">Receive the status updates coming from the POS.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">5</div>
    <div class="step-list-content">
      <p class="step-list-title"><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/channel_snooze">Snooze/Unsnooze Products Webhook</a></p>
      <p class="step-list-desc"></p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">6</div>
    <div class="step-list-content">
      <p class="step-list-title"><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/busy-mode">Busy Mode Webhook</a></p>
      <p class="step-list-desc"></p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">7</div>
    <div class="step-list-content">
      <p class="step-list-title"><a href="https://developers.deliverect.com/v3.0-ordering-experience/reference/courier-update-webhook">Courier Status Update</a> — <em>Optional</em></p>
      <p class="step-list-desc"></p>
    </div>
  </div>
</div>
`}</HTMLBlock>
