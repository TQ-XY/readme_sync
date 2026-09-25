---
api:
  file: payapi.json
  operationId: post_pay-events-integrationname-gatewayprofiles-gatewayprofileid
hidden: false
link:
  new_tab: false
metadata:
  robots: index
next:
  pages:
    - slug: pay-platform-request-payment
      title: Request Payment
      type: endpoint
---
## Purpose

Payment platforms should call this endpoint to confirm the status of a payment request

<HTMLBlock>{`
<div class="callout-banner callout-banner--important">
  <span class="callout-icon"><i class="fa-duotone fa-solid fa-triangle-exclamation"></i></span>
  <p>
    <strong>Payment Authorization Timeout</strong><br>
    Updates to authorize or refuse a payment should be sent within <strong>10 minutes</strong> of the initial payment request being received.
  </p>
</div>
`}</HTMLBlock>