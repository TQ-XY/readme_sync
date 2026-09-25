---
api:
  file: commerce.json
  operationId: commerce-channel-api-menus-get-root-menus
hidden: false
---
### Purpose

A “Root Menu” is the general menu sold at a brand-level.  This will be associated to the primary location in the account and is representative of all items offered across the brand without including details on location-specific availability or pricing. It's primary role is as an entry point for users to browse the products sold before entering a store specific ordering experience.

### Store status

The store status returns the current status of availability. It can have the following values:

- **open**: the store is open and accepting orders.
- **closed**: the store is either closed or outside of the opening hours.
- **busy**: the store is open, but with a delay in the preparation time which is shown as `preparationTimeDelay` in minutes
- **paused**: the store is temporarily closed within the normal opening hours and not accepting orders

### Glossary

For a full list of all menu attributes and their definition, see the link below;

<HTMLBlock>{`
<a href="https://developers.deliverect.com/page/menu-glossary" target="_blank" class="doc-button">▶ Menu Model</a>
`}</HTMLBlock>

<br />