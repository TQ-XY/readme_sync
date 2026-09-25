---
api:
  file: vault.json
  operationId: post_
hidden: false
next:
  pages:
    - slug: request-payment
      title: Request Payment
      type: endpoint
---
# Purpose

This is a proxy endpoint allowing ordering platforms to process card payments via Deliverect Pay (<Glossary>Dpay</Glossary>) **without ever handling stored card data themselves**. This will help achieve the following;

1. **Accept PCI data for tokenization** — an external party can securely send us PCI data (raw PAN, expiry, CVC and other card details) for tokenization. The proxy is the _only_ surface that receives raw card data; Deliverect Pay itself only ever sees encrypted, vaulted representations.
2. **Verify and vault** — submitted PCI data is verified with the underlying PSP and, on success, stored as a token associated with the customer (`customerId`) for later use (see Commerce API <Anchor target="_blank" href="ref:commerce-create-basket">Create Basket</Anchor>​ )
3. **Retrieve customer tokens** — previously vaulted tokens can be retrieved per customer via [Get Customer Tokens](ref:pay-api-get-customer-tokens) enabling return customer experiences such as "pay with saved card" without re-entering details.
4. **Capture funds using a token** — a verified customer token can be used to acquire funds via the Deliverect Pay payments endpoint, with immediate capture or manual (pre-authorize now, capture later) modes.

### Overview

To process card payments in this format, the following interactions will take place;

- **Channel → Proxy** — raw card details are submitted to the proxy over the custom hostname.

- **Proxy → Deliverect Pay** — the proxy vaults the card and forwards a create-token request with encrypted data.

- **Deliverect Pay → PSP** — the card is verified with the PSP.

- **PSP → Deliverect Pay → Channel** — the verification result flows back and the channel receives the token with its `status`.

### Sequence Diagram

Click the link below to see the full Tokenization > Payment flow;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/page/creating-a-token-diagram" target="_blank" class="doc-button">▶ Tokenization Payment Flow</a>
`}</HTMLBlock>

<HTMLBlock>{`
<div class="callout-banner callout-banner--note">
  <span class="callout-icon"><i class="fa-duotone fa-solid fa-lightbulb"></i></span>
  <p>
    <strong>Basis Theory</strong><br>
    Deliverect uses <a href="https://basistheory.com" target="_blank" rel="noopener noreferrer">BasisTheory</a> as a token vault, surfacing a proxy to channel partners. The proxy securely receives PCI data (raw card details) and passes encrypted data on to the PSP. This means <strong>channels never send raw card data to Deliverect Pay directly</strong>, keeping the channel's PCI scope to a minimum.
  </p>
</div>
`}</HTMLBlock>

## 1.Card Tokenization

A channel will first collect a customer's card details and submit them to the basis theory proxy which will store this to a vault in a PCI compliant manner. Deliverect Pay will then request the customer's integrated Payment Service Provider to verify the card. When verified, the channel will be returned a reusable token along with the verification status of the card.

<HTMLBlock>{`
<div class="callout-banner callout-banner--neutral">
  <span class="callout-icon"><i class="fa-regular fa-triangle-exclamation"></i></span>
  <p>
    <strong>Failed Verification</strong><br>
    A token can be returned with a failed verification <code>"status": "failed"</code>, e.g. a declined card or invalid details. In this case, do not proceed to process payment with a failed token and instead prompt the customer for another payment method.
  </p>
</div>
`}</HTMLBlock>

## 2.Process Payment

Once verified, a channel can proceed to request a payment via [Request Payment](ref:request-payment)

<br />
