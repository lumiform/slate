---
title: Lumiform Public API

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://admin.lumiformapp.com/public-api'>Go to API Management Page</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - filters
  - inspections 
  - issues
  - errors

search: true

code_clipboard: true
---

# Introduction

Welcome to the Lumiform Public API documentation! You can use our API to get your organization's Inspections, Questions and Issues.
Lists of Inspections and Issues are paginated. Paginated responses also have a `meta` and a `links` property 
useful for navigation - or even for helping you build a navigation UI if you desire!
 
You can view cURL request examples in the dark area to the right, as well as examples of the responses you should expect to get.

# Authentication

> To obtain your API Bearer token, use this code:

```shell
curl GET 'https://public-api.lumiformapp.com/api/v1/oauth2/token' \
  -H 'Authorization: Basic yourbase64token'
```

> Make sure to replace `yourbase64token` with the token you have obtained by base 64 encoding your API key and API secret concatenated with a colon.

> If all went well you should receive a response like the following:

```json
{
  "access_token": "yourtoken",
  "expires_in": 3600,
  "token_type": "Bearer"
}
```

> To authorize requests, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "[api_endpoint_here]" \
  -H "Accept: application/json" \
  -H "Authorization: Bearer yourtoken"
```

> Make sure to replace `yourtoken` with the token you got from the previous response.

Lumiform uses API keys to allow access to the API. Your organization can obtain an API key and secret by visiting the [API management page](https://admin.lumiformapp.com/public-api).
Once you have obtained them, you can get your API key by following these steps:

1. Concatenate your API key and API secret with a colon like so: `apikey:apisecret`
2. Generate a base64 encoded token from your key and secret concatenated string. You can use [this website](https://www.base64encode.org/) for example.
3. Make a request to our OAuth 2.0 Token endpoint using Basic Authorization, and your base64 token as the key, as shown in the code example.
4. You should now receive your bearer token in the `access_token` field which you can use for authorization!

<aside class="notice">
Take note of the token expiration timer by checking the `expires_in` field.
</aside>

Lumiform expects your `access_token` bearer token to be included in the header of all API requests you make:

`Authorization: Bearer [your token here]`

<aside class="notice">
You must replace <code>[your token here]</code> with your organization's access token.
</aside>
