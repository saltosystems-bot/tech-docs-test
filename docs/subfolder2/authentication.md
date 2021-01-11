---
title: "Authentication"
---

SALTO Nebula uses [OAuth 2.0](https://oauth.net/2/) to authenticate connections that use the API.
OAuth 2.0 is the industry-standard protocol for authentication and authorization used with web, mobile, and desktop applications.
Every use of the API requires authentication so SALTO can make sure that only authorized users can interact with Nebula content.

The API uses the OAuth Client Credentials flow which the IETF OAuth Working Group recommends for use in machine-to-machine authentication.
Your application needs to securely store its Client ID and Client Secret and pass those to the authorization server in exchange for an access token.
At a high-level, the flow has two steps:

* Your application passes its client credentials to the authorization server
* If the credentials are correct, the authorization server responds with an access token

## Authorize

TBC

## Generate an access token

`https://account.saltonebula.com/oauth2/token` is the URL of the API token endpoint, the endpoint that returns access tokens.
An access token is a data string that enables Nebula to verify that a request belongs to an authorized session.
An authorization code must be sent to the token endpoint in a request for an access token.
You can then use the returned access token to make API calls.

To exchange an authorization code for an access token, send a request like the following: (Remember to replace the placeholder values with your credentials)

```bash
curl --request POST \
     --url https://account.saltonebula.com/oauth2/token \
     --header 'content-type: application/x-www-form-urlencoded' \
     --data 'grant_type=client_credentials&client_id={{YOUR_CLIENT_ID}}&client_secret={{YOUR_CLIENT_SECRET}}'
```

This returns a response something like this:

```json
{
  "access_token": "{{YOUR_ACCESS_TOKEN}}",
  "expires_in": 299,
  "scope": "",
  "token_type": "bearer"
}
```

## Parameters

|Parameters|Type|Description|
|---|---|---|
|`access_token`|String|A data string that enables the API to verify that a request belongs to an authorized session|
|`expires_in`|Integer|When the file will be automatically deleted. This attribute cannot be set|
|`scope`|String|This optional parameter identifies the scopes available to the application once it's authenticated. If you do not supply this parameter then the API grants access to the default scopes configured for the application in its configuration page|
|`token_type`|String|Always set to `bearer`|
|`grant_type`|String|Always set to `client_credentials`|

## Refresh tokens

Refresh tokens are used to get a new access token when your current access token expires.
For more information, see the OAuth 2.0 [RFC](https://tools.ietf.org/html/rfc6749#section-1.5).

Nebula refresh tokens are valid for a fixed length of time.
By default, access tokens are valid for 1 hour and refresh tokens are valid for 90 days.

If your application is authorized for programmatic refresh tokens, the following fields are returned when you exchange the authorization code for an access token:

* `refresh_token`—Your refresh token for the application. This token must be kept secure
* `refresh_token_expires_in`—The number of seconds remaining until the refresh token expires. Refresh tokens can have a longer lifespan than access tokens

## Make API requests

Once you've received an access token, you can make API requests by including an Authorization header with your access token in the HTTP call to the API.

For example:

```bash
curl --request GET \
     --url https://api.saltonebula.com/v1/installations/acme/users \
     --header "Authorization: Bearer {{YOUR_ACCESS_TOKEN}}" \
     --data "page_size=10" \
     --data "filter=display_name.startsWith('A')"
```
