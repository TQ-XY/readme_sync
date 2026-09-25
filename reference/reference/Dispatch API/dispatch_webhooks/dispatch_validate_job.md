---
api:
  file: dispatch_webhooks.json
  operationId: post_validate-job
hidden: false
link:
  new_tab: false
---
# Purpose&#x20;

The initial dispatch notification that one or multiple delivery jobs are needing validated as being deliverable i.e. a Courier is available for the provided delivery job specification.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>

    The Validate Webhook URL needs to be standardised, i.e.
    <strong>the same URL should be used for every customer installation</strong>.
  </p>
</div>
`}</HTMLBlock>

## Request Parameters

See full list of order attributes below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/page/dispatch-delivery-job-model" target="_blank" class="doc-button">▶ Delivery Job Model</a>
`}</HTMLBlock>

### Error codes

If delivery is not possible, one or more of the following error codes are expected to be returned in the response;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/page/dispatch-error-codes" target="_blank" class="doc-button">▶ Error Codes</a>
`}</HTMLBlock>

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>
    <strong>Delivery Address Coordinates</strong><br>
     In the rare event that the coordinates are not included in the payload, you should still validate the delivery job, as the delivery address details are always provided.
  </p>
</div>
`}</HTMLBlock>

## Response

Below is an examples of the expected response from the dispatch platform;

<HTMLBlock>{`
<div class="callout-banner callout-banner--important">
  <span class="callout-icon"><i class="fa-duotone fa-solid fa-triangle-exclamation"></i></span>
  <p>
    <strong>Required Parameters</strong><br>
   All parameters shown in the response model are required. Omitting any of these parameters will prevent the
    <strong>Create Delivery Job</strong> request from being triggered
  </p>
</div>
`}</HTMLBlock>

## Response Parameters

All parameters shown in the response payload are required. Missing out will result in the create call request not to be triggered, see full list delivery model in link below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/page/dispatch-delivery-job-model#response-parameters" target="_blank" class="doc-button">▶ Delivery Job Model</a>
`}</HTMLBlock>