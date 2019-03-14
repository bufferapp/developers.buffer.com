+++
title = "Authentication"
menu = "main"
weight = 10
+++

Authentication with Buffer is the first step in building your app.

Buffer is an OAuth 2.0 provider. We recommend using one of the many great OAuth 2.0 libraries to do the heavy lifting!

### Getting Started

All of the Buffer API endpoints require authentication. To get an `access_token` you must first [register an application here](/developers/apps/create). Once you have registered an app follow the steps below to gain authorized access to a users account.

Please note: **a good OAuth library will handle most of these steps for you.** You should only need to supply a client ID and secret.

### Redirect Your Users for Authorization

First, redirect your user to the authorize endpoint. Note, the `redirect_uri` must match the Callback URL given when your app was registered.

#### Example Request

```
GET https://bufferapp.com/oauth2/authorize?
    client_id=...&
    redirect_uri=...&
    response_type=code
```

The user will then approve or deny the request to authorize your application. At this point they will be redirected back to the redirect_uri location with an authorization code or error message as a query parameter. This should look something like:

`http://example.com/back?code=1/mWot20jTwojsd00jFlaaR45`

### Getting an Access Token

Note: If you only need a single access token, we will automatically generate that for you after you have [created an app.](/developers/apps/create)

Your app should swap the authorization code for an access token by `POST`ing it along with your `client_id`, `client_secret`, `redirect_uri` and `grant_type=authorization_code` to our token endpoint. **Note, a code is valid for 30 seconds only** - this swap should be performed as soon as the code is received. Also note that the code parameter must not be url encoded - ie. it should be formatted like `1/mWot20jTwojsd00jFlaaR45` and not `1%2FmWot20jTwojsd00jFlaaR45`.

#### Example Request

POST https://api.bufferapp.com/1/oauth2/token.json

POST Data
     client_id=...&
     client_secret=...&
     redirect_uri=...&
     code=...&
     grant_type=authorization_code

If your request is successful we will return a long-lived access token which can be used to access the users account details for all further api requests.

### Using The Token

All requests to the Buffer API must be made using HTTPS, with the access token provided in the HTTP Authorization header, request body or query string. For example, using the query string:

#### Example Request

`GET https://api.bufferapp.com/1/profiles.json?access_token=...`

### Implementation

The implementation is based on [version 20 of the IETF draft](http://tools.ietf.org/html/draft-ietf-oauth-v2-20).

### Deauthorizing your client

To deauthorize your client, see [/user/deauthorize](/developers/api/user#deauthorize).
