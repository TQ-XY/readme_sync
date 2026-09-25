---
title: Overview
deprecated: false
hidden: false
icon: fad fa-book-open-lines
metadata:
  robots: index
---
## Introduction

Our Channel API provides the basic capabilities to:

<HTMLBlock>{`
<div class="step-list step-list--dots">
  <div class="step-list-item">
    <div class="step-list-marker step-list-marker--dot"></div>
    <div class="step-list-content">
      <p class="step-list-desc">Ingest menu data via webhooks</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker step-list-marker--dot"></div>
    <div class="step-list-content">
      <p class="step-list-desc">Create orders for POS injection</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker step-list-marker--dot"></div>
    <div class="step-list-content">
      <p class="step-list-desc">Handle the order preparation statuses, e.g. Order Acceptance → Ready for Pickup events</p>
    </div>
  </div>
  <div class="step-list-item">
    <div class="step-list-marker step-list-marker--dot"></div>
    <div class="step-list-content">
      <p class="step-list-desc">Process store operation events such as busy mode, snoozed products, etc.</p>
    </div>
  </div>
</div>
`}</HTMLBlock>

<Cards>
  <Card title="Flow Diagram" href="https://developers.deliverect.com/page/channel-flow" icon="fad fa-diagram-project">
    See the complete Channel order flow from menu ingestion to order creation
  </Card>

  <Card title="Guides" href="https://developers.deliverect.com/v3.0-ordering-experience/docs/channel-api-overview" icon="fad fa-book">
    Step-by-step guidance for integrating your ordering platform with our Channel API
  </Card>

  <Card title="FAQ" href="https://developers.deliverect.com/v3.0-ordering-experience/docs/faq" icon="fad fa-comment-question" target="_blank">
    See the most commonly asked questions about the Channel API
  </Card>
</Cards>
