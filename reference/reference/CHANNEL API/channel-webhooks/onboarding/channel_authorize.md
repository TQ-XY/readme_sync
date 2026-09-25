---
api:
  file: channel_webhooks.json
  operationId: channel_authorize
hidden: true
---
This endpoint needs to be implemented in case the channel wants to support login and authorization from an external platform.

The data that identifies a customer is sent as a payload, the response should be an authorization code.

The authorization code is then sent as a query parameter to the same url in a REDIRECT request. The channel should then exchange the authorization code for an internal access token and redirect the user back again to the ordering experience.

The url when the authorization request will be performed, should be returned in the response of the [register channel endpoint](https://developers.deliverect.com/v3.0/reference/channel_register) in the field `authorizationURL`.