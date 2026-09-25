---
api:
  file: crm.json
  operationId: post_crm-accountid-customers-lookup
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
## Purpose

Look up a customer stored in Deliverect CRM by their email/phone

<HTMLBlock>{`
<div class="callout-banner callout-banner--note">
  <span class="callout-icon"><i class="fa-duotone fa-solid fa-lightbulb"></i></span>
  <p>
    <strong>Available at account or channel level</strong><br>
POST /crm/channel/{channelLinkId}/customers/lookup
</br>
POST /crm/{accountId}/customers/lookup
  </p>
</div>
`}</HTMLBlock>

## Body parameters<br />

The search can be performed with one of the following fields:

- email
- phone
  <HTMLBlock>{`
  <div class="callout-banner callout-banner--important">
    <span class="callout-icon"><i class="fa-regular fa-triangle-exclamation"></i></span>
    <p>

      At least one of these fields is required; if neither is provided, the API returns 422 Unprocessable Entity.
  This endpoint returns exactly one profile or an error; it is not a search or list endpoint.  

    </p>
  </div>
  `}</HTMLBlock>

When email is provided, with or without phone, the API returns the most recently created matching profile; when only phone is provided, multiple matches result in an error rather than an inferred profile.

<br />