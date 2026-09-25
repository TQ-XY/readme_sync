---
title: Endpoints
deprecated: false
hidden: false
icon: fad fa-plug
metadata:
  robots: index
---
<BaseURLsTable />

## Coupons Endpoints

This documentation will cover the following API endpoints;

| ENDPOINT                                 | TYPE                                                                                                                                                                                | FUNCTION                                                                                                   |
| :--------------------------------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------- |
| [Get Coupons](ref:get-coupons)           | <span style={{ backgroundColor: "#008756", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}>GET</span>  | Get the enabled Coupons that can be used by a given Channel Link ID. Returns a paginated Coupons response. |
| [Validate Coupons](ref:validate-coupons) | <span style={{ backgroundColor: "#0272d9", color: "white", borderRadius: "16px", fontFamily: "Helvetica", fontWeight: "light", fontSize: "11px", padding: "5px 10px" }}>POST</span> | Validates the coupons against a customer's order.                                                          |
