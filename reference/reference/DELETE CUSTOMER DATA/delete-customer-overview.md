---
title: Overview
deprecated: false
hidden: true
icon: fad fa-book-open-lines
metadata:
  robots: index
---
## Introduction

This API enables the deletion of the customer data flow between Deliverect and the DSP system.

## End-to-End Flow Summary

<HTMLBlock>{`
<div class="step-list">
  <div class="step-list-item">
    <div class="step-list-marker">1</div>
    <div class="step-list-content">
      <p class="step-list-title">Send Deletion Request — <a href="https://developers.deliverect.com/update/reference/delete-customer-data-webhook-url">Webhook Request URL</a></p>
      <p class="step-list-desc">Deliverect sends a deletion request to the DSP system via the webhook request URL.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">2</div>
    <div class="step-list-content">
      <p class="step-list-title">Acknowledge Receipt</p>
      <p class="step-list-desc">The DSP system acknowledges receipt of the deletion request.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">3</div>
    <div class="step-list-content">
      <p class="step-list-title">Process the Deletion</p>
      <p class="step-list-desc">The DSP system processes the deletion asynchronously.</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker">4</div>
    <div class="step-list-content">
      <p class="step-list-title">Send Final Result — <a href="https://developers.deliverect.com/update/reference/get_new-endpoint">Outcome API Endpoint</a></p>
      <p class="step-list-desc">The DSP system sends the final result via the Outcome API endpoint.</p>
    </div>
  </div>
</div>
`}</HTMLBlock>

## Endpoints

| ENDPOINT                                                                                                                                                      | TYPE                                                                                                                                                                                 | FUNCTION                                 |
| :------------------------------------------------------------------------------------------------------------------------------------------------------------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------- |
| **Customer Deletion Status**<Anchor target="_blank" href="https://developers.deliverect.com/v3.0/reference/deletion-customer-data-endpoint">&#x20;🔗</Anchor> | <span style={{ backgroundColor: "#0272d9", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}> POST</span> | Submit the final deletion outcome result |

## Webhooks

| Webhook                                                                                   | TYPE                                                                                                                                                                                 | FUNCTION                               |
| :---------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------- |
| **Deletion Request**[ 🔗](https://developers.deliverect.com/v1.1/reference/get-locations) | <span style={{ backgroundColor: "#0272d9", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}> POST</span> | Receive customer data deletion request |
