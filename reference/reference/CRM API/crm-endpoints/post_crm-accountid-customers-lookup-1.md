---
api:
  file: crm.json
  operationId: post_crm-accountid-customers-lookup-1
hidden: false
link:
  new_tab: false
metadata:
  robots: index
---
## Purpose

Look up customers stored in Deliverect CRM by their email/phone. <br />

<HTMLBlock>{`
<div class="callout-banner callout-banner--note">
  <span class="callout-icon"><i class="fa-duotone fa-solid fa-lightbulb"></i></span>
  <p>
    <strong>Available at account or channel level</strong><br>
POST /crm/channel/{channelLinkId}/customers/lookup-many
</br>

POST /crm/{accountId}/customers/lookup-many
  </p>
</div>
`}</HTMLBlock>

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-square-info"></i></span>
  <p>

    Use the <a href="https://developers.deliverect.com/v3.0-ordering-experience/update/reference/customer_by_email">Lookup Customer endpoint</a> when a single customer profile is expected and the API should return exactly one match or an error. Use <strong>Lookup Many</strong> when the provided identifiers may match multiple customer profiles and all matching results need to be retrieved.
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

      At least one of these fields (email or phone) is required; if neither is provided, the API returns 422 Unprocessable Entity.
  <br>

  Unlike lookup, lookup-many returns 200 OK with total: 0 and an empty items array when no profiles match.
  </br>
  It never returns ambiguous_profile_lookup, making it the appropriate endpoint when a phone number may be associated with multiple profiles.

    </p>
  </div>
  `}</HTMLBlock>
