+++
title = "Overview"
menu = "main"
weight = 1
+++

We recently made some important changes to the Buffer API in regards to Twitter content in order to comply with their 2019 Developer Policy. Please visit our [Change Logs page](/developers/api/logs) for more details!

The Buffer API provides access to [user](/developers/api/user)'s pending and sent [updates](/developers/api/updates), social media [profiles](/developers/api/profiles), [scheduled times](/developers/api/profiles#schedules) and more.

To get started, [create an app](/developers/apps/create) and [get an access token](/developers/api/oauth) for a user.

### Endpoints

All currently available endpoints are listed in this documentation. If you have ideas for further things you would like to see in the Buffer API, please contact [hello@buffer.com](mailto:hello@buffer.com) - we might build them!

But be sure to set the HTTP Content-Type header to `"application/x-www-form-urlencoded"` for your requests if you are writing your own client.

### Rate Limits

The Buffer API is rate limited to 60 authenticated requests per user per minute. If you make more than 60 requests within a 60 seconds window period, you will receive a HTTP code 429 response.

If you have a need for a higher rate limit, please get in touch so that we can try and help out.

### Response Formats

All requests to the Buffer API must end with the desired response format. Currently the only available response format is JSON and responses are of type application/json.

For well formatted JSON output, add `&pretty=true` to any request. Very useful for testing in the browser!

#### Example Request

`GET https://api.bufferapp.com/1/profiles.json?pretty=true`

### Questions & Problems

If you have any issues using the Buffer API you can contact us by emailing [hello@buffer.com](mailto:hello@buffer.com) or give us a shout over on twitter [@buffer](http://twitter.com/buffer) - we'll get back to you fast!
