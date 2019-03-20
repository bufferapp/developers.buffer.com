+++
title = "Updates"
menu = "main"
weight = 40
+++

An update represents a single post to a single social media account. An update can also include media attachments such as pictures and links.

### Get

[/updates/:id](#get-updates-id)

[/profiles/:id/updates/pending](#get-profiles-id-updates-pending)

[/profiles/:id/updates/sent](#get-profiles-id-updates-sent)

### Post

[/profiles/:id/updates/reorder](#post-profiles-id-updates-reorder)

[/profiles/:id/updates/shuffle](#post-profiles-id-updates-shuffle)

[/updates/create](#post-updates-create)
[/updates/:id/update](#post-updates-id-update)

[/updates/:id/share](#post-updates-id-share)
[/updates/:id/destroy](#post-updates-id-destroy)

[/updates/:id/move_to_top](#post-updates-id-move-to-top)

### GET /updates/:id

Returns a single social media update.

Please note that in the "statistics" section for Twitter updates, "favorites" is equivalent to "likes". We have left this as "favorites" for now for backward compatibility and will be changing it to "likes" in the next version of the Buffer API.

#### Example Request

```
GET https://api.bufferapp.com/1/updates/4eb8565e0acb04bb82000004.json

{
  "id": "4eb8565e0acb04bb82000004",
  "created_at": 1320703582,
  "day": "Monday 7th November",
  "due_at": 1320742680,
  "due_time": "10:09 pm",
  "profile_id": "4eb854340acb04e870000010",
  "profile_service": "twitter",
  "sent_at": 1320744001,
  "service_update_id": "133667319959392256",
  "statistics": {
    "reach": 2460,
    "clicks": 56,
    "retweets": 20,
    "favorites": 1,
    "mentions": 1
  },
  "status": "sent",
  "text": "This is just the beginning, the very beginning...",
  "text_formatted": "This is just the beginning, the very beginning...",
  "user_id": "4eb9276e0acb04bb81000067",
  "via": "chrome"
}
```

### GET /profiles/:id/updates/pending

Returns an array of updates that are currently in the buffer for an individual social media profile.

Parameter          | Type    | Description
------------------ | ------- | -------------
`page` optional | integer | Specifies the page of status updates to receive. If not specified the first page of results will be returned.
`count` optional | integer | Specifies the number of status updates to receive. If provided, must be between 1 and 100.
`since` optional | timestamp | Specifies a unix timestamp which only status updates created after this time will be retrieved.
`utc` optional | boolean | If utc is set times will be returned relative to UTC rather than the users associated timezone.

#### Example Request

```
GET https://api.bufferapp.com/1/profiles/4eb854340acb04e870000010/updates/pending
    .json

{
  "total": 8,
  "updates": [ {
    "id": "4ec93ae4512f7e6307000002",
    "created_at": 1320703582,
    "day": "Monday 7th November",
    "due_at": 1320543480,
    "due_time": "07:01 pm",
    "profile_id" : "4eb854340acb04e870000010",
    "profile_service" : "twitter",
    "status" : "buffer",
    "text" : "This is me in an alternate life where i can breakdance j.mp/w...",
    "text_formatted" : "This is me in an alternate life where i can breakda...",
    "user_id" : "4eb9276e0acb04bb81000067",
    "via" : "firefox"
  },
  {
    ...
  }]
}
```

### GET /profiles/:id/updates/sent

Returns an array of updates that have been sent from the buffer for an individual social media profile.

Please note that in the "statistics" section for Twitter updates, "favorites" is equivalent to "likes". We have left this as "favorites" for now for backward compatibility and will be changing it to "likes" in the next version of the Buffer API.

Parameter          | Type    | Description
------------------ | ------- | -------------
`page` optional | integer | Specifies the page of status updates to receive. If not specified the first page of results will be returned.
`count` optional | integer |Specifies the number of status updates to receive. If provided, must be between 1 and 100.
`since` optional | timestamp |Specifies a unix timestamp which only status updates sent after this time will be retrieved.
`utc` optional | boolean | If utc is set times will be returned relative to UTC rather than the users associated timezone.
`filter` optional | string | Controls what sort of updates are returned. 'all' will return everything, while the default 'default' will return everything except replies not posted via Buffer.

#### Example Request

```
GET https://api.bufferapp.com/1/profiles/4eb854340acb04e870000010/updates/sent
    .json

{
  "total": 97,
  "updates": [ {
    "id": "4ebc559d0acb04221b000008",
    "created_at": 1320703582,
    "day": "Monday 7th November",
    "due_at": 1320742680,
    "due_time": "10:09 pm",
    "profile_id": "4eb854340acb04e870000010",
    "profile_service": "twitter",
    "sent_at": 1320744001,
    "service_update_id": "133667319959392256",
    "statistics": {
      "reach": 2460,
      "clicks": 56,
      "retweets": 20,
      "favorites": 1,
      "mentions": 1
    },
    "status": "sent",
    "text": "This is just the beginning, the very beginning...",
    "text_formatted": "This is just the beginning, the very beginning...",
    "user_id": "4eb9276e0acb04bb81000067",
    "via": "chrome"
  },
  {
    ...
  }]
}
```

### POST /profiles/:id/updates/reorder

Edit the order at which statuses for the specified social media profile will be sent out of the buffer.

#### Parameters

Parameter          | Type    | Description
------------------ | ------- | -------------
`order` required | integer | An ordered array of status update id’s. This can be a partial array in combination with the offset parameter or a full array of every update in the profiles Buffer.
`offset` optional | integer | Specifies the number of status updates to receive. If provided, must be between 1 and 100.
`utc` optional | boolean | If utc is set times will be returned relative to UTC rather than the users associated timezone.

#### Example Request

```
POST https://api.bufferapp.com/1/profiles/4eb854340acb04e870000010/updates/
     reorder.json

POST Data
offset=10&
order[]=4eb854340acb04e870000010&
order[]=4eb9276e0acb04bb81000067&
order[]=4eb2567e0ade04ba51000001

{
  "success": true,
  "updates": [{
    "id": "4eb854340acb04e870000010",
    "created_at": 1320703582,
    "day": "Saturday 5th November",
    "due_at": 1320742680,
    "due_time": "08:01 am",
    "profile_id": "4eb854340acb04e870000010",
    "profile_service": "twitter",
    "status": "buffer",
    "text": "3 Incredible Stories Made Possible Through Twitter j.mp/u...",
    "text_formatted": "3 Incredible Stories Made Possible Through Twit...",
    "user_id": "4eb9276e0acb04bb81000067",
    "via": "safari"
  },
  {
    ...
  }]
}
```

### POST /profiles/:id/updates/shuffle

Randomize the order at which statuses for the specified social media profile will be sent out of the buffer.

#### Parameters

Parameter          | Type    | Description
------------------ | ------- | -------------
`count` optional | integer | Specifies the number of status updates returned. These will correspond to the first status updates that will be posted.
`utc` optional | boolean | If utc is set times will be returned relative to UTC rather than the users associated timezone.

#### Example Request

```
POST https://api.bufferapp.com/1/profiles/4eb854340acb04e870000010/updates/
     shuffle.json

POST Data
count=10

{
  "success": true,
  "updates": [{
    "id": "4eb854340acb04e870000010",
    "created_at": 1320703582,
    "day": "Saturday 5th November",
    "due_at": 1320742680,
    "due_time": "08:01 am",
    "profile_id": "4eb854340acb04e870000010",
    "profile_service": "twitter",
    "status": "buffer",
    "text": "3 Incredible Stories Made Possible Through Twitter j.mp/u...",
    "text_formatted": "3 Incredible Stories Made Possible Through Twit...",
    "user_id": "4eb9276e0acb04bb81000067",
    "via": "safari"
  },
  {
    ...
  }]
}
```

### POST /updates/create

Create a new status update for one or more profiles.

Parameter          | Type    | Description
------------------ | ------- | -------------
`profile_ids` required | array | An array of Buffer profile id’s that the status update should be sent to. Invalid profile_id’s will be silently ignored.
`text` optional | string | The status update text
`shorten` optional | boolean | If shorten is false links within the text will not be automatically shortened, otherwise they will.
`now` optional | boolean | If now is set, this update will be sent immediately to all profiles instead of being added to the buffer.
`top` optional | boolean | If top is set, this update will be added to the top of the buffer and will become the next update sent.
`media` optional | associative array | An associative array of media to be attached to the update containing some of the following parameters: `link`, `description`, `title`, `picture`, `photo`, `thumbnail`

Please note that not all of those fields are required for an update. Here are some scenarios explaining when to use each field:

#### To share an image:

Provide the url of that image with the `photo` parameter

#### To share an update w/ a link preview

For Facebook, Google+ and Linkedin, you can add a large clickable link preview with your update. To do this, provide the url of the content with the `link` parameter. Optionally, you can provide the `picture`, `title`, and `description` parameters to customize what the link preview looks like. Example on Facebook:

![](/images/developers/example-link-preview.png)

#### Sharing to multiple profiles

When sharing to profiles on different networks (ex. Facebook and Twitter), not all parameters will be used. All parameters not applying to that network will be silently ignored. For example, if you're posting to Facebook and Twitter, Twitter will ignore the `link`, `picture`, `title`, and `description` parameters. If these parameters are missing from your API request's response, it simply means they were not required and ignored.

**Note:** the `thumbnail` parameter is optional and is only used by for display in the Buffer dashboard.

Parameter          | Type    | Description
------------------ | ------- | -------------
`attachment` optional | boolean | In the absence of the `media` parameter, controls whether a link in the `text` should automatically populate the `media` parameter. Defaults to `true`.
`scheduled_at` optional | timestamp **or** ISO 8601 formatted date-time | A date describing when the update should be posted. Overrides any `top` or `now` parameter. When using ISO 8601 format, if no UTC offset is specified, UTC is assumed.
`retweet` optional | associative array | (Twitter only) This parameter can be used to create a 'retweet' update. It will be silently ignored for any other profiles. Currently accepts the following parameters: `tweet_id` (required) - the id of the tweet which is to be retweeted, `comment` (optional)

#### Example Request

```
POST https://api.bufferapp.com/1/updates/create.json

POST Data
text=This%20is%20an%20example%20update&
profile_ids[]=4eb854340acb04e870000010&
profile_ids[]=4eb9276e0acb04bb81000067&
media[link]=http%3A%2F%2Fgoogle.com&
media[description]=The%20google%20homepage

{
  "success": true,
  "buffer_count": 10,
  "buffer_percentage": 20,
  "updates": [{
    "id": "4ecda256512f7ee521000004",
    "created_at": 1320703582,
    "day": "Saturday 26th November",
    "due_at": 1320742680,
    "due_time": "11:05 am",
    "media": {
      "link": "http://google.com",
      "title": "Google",
      "description": "The google homepage"
    },
    "profile_id": "4eb854340acb04e870000010",
    "profile_service": "twitter",
    "status": "buffer",
    "text": "This is an example update",
    "text_formatted": "This is an example update",
    "user_id": "4eb9276e0acb04bb81000067",
    "via": "api"
  },
  {
    ...
  }]
}
```

Create a new status update with an image.

#### Example Request

```
POST https://api.bufferapp.com/1/updates/create.json

POST Data
text=This%20is%20an%20example%20image%20%based%20update&
profile_ids[]=4eb854340acb04e870000010&
profile_ids[]=4eb9276e0acb04bb81000067&
media[photo]=http%3A%2F%2Fgoogle.com%2Fimages%2Flogo.png&
media[thumbnail]=http%3A%2F%2Fgoogle.com%2Fimages%2Flogo_thumb.png

{
  "success": true,
  "buffer_count": 10,
  "buffer_percentage": 20,
  "updates": [{
    "id": "4ecda256512f7ee521000004",
    "created_at": 1320703582,
    "day": "Saturday 26th November",
    "due_at": 1320742680,
    "due_time": "11:05 am",
    "media": {
      "thumbnail": "http://google.com/images/logo_thumb.png",
      "picture": "http://google.com/images/logo.png"
    },
    "profile_id": "4eb854340acb04e870000010",
    "profile_service": "twitter",
    "status": "buffer",
    "text": "This is an example image based update",
    "text_formatted": "This is an example image based update",
    "user_id": "4eb9276e0acb04bb81000067",
    "via": "api"
    },
    {
      ...
    }]
}
```

Create a retweet update.

#### Example Request

POST https://api.bufferapp.com/1/updates/create.json

POST Data
profile_ids[]=4eb854340acb04e870000010&
retweet[tweet_id]=654043184394207232

### POST /updates/:id/update

Edit an existing, individual status update.

Parameter          | Type    | Description
------------------ | ------- | -------------
`text` required | string | The status update text
`now` optional | boolean | If now is set, this update will be sent immediately to all profiles instead of being added to the buffer.
`media` optional | associative array | An associative array of media to be attached to the update, currently accepts link, description, title and picture parameters.
`utc` optional | boolean | If utc is set times will be returned relative to UTC rather than the users associated timezone.
`scheduled_at` optional  | timestamp **or** ISO 8601 formatted date-time | A date describing when the update should be posted. Overrides any `top` or `now` parameter. When using ISO 8601 format, if no UTC offset is specified, UTC is assumed.

#### Example Request

```
POST https://api.bufferapp.com/1/updates/4ecda256512f7ee521000004/update.json

POST Data
text=This%20is%20an%20edited%20update

{
  "success": true,
  "buffer_count": 10,
  "buffer_percentage": 20,
  "update": {
    "id": "4ecda256512f7ee521000004",
    "client_id": "4f850cc93733aa9301000002",
    "created_at": 1320703582,
    "day": "Saturday 26th November",
    "due_at": 1320742680,
    "due_time": "11:05 am",
    "media": {
      "link": "http://google.com",
      "title": "Google",
      "description": "The google homepage"
    },
    "profile_id": "4eb854340acb04e870000010",
    "profile_service": "twitter",
    "status": "buffer",
    "text": "This is an edited update",
    "text_formatted": "This is an edited update",
    "user_id": "4eb9276e0acb04bb81000067",
    "via": "api"
  }
}
```

### POST /updates/:id/share

Immediately shares a single pending update and recalculates times for updates remaining in the queue.

#### Example Request

```
POST https://api.bufferapp.com/1/updates/4ecda256512f7ee521000001/share.json

{
  "success": true
}
```

### POST /updates/:id/destroy

Permanently delete an existing status update.

#### Example Request

```
POST https://api.bufferapp.com/1/updates/4ecda256512f7ee521000004/destroy.json

{
  "success": true
}
```

### POST /updates/:id/move_to_top

Move an existing status update to the top of the queue and recalculate times for all updates in the queue. Returns the update with its new posting time.

Please note that in the "statistics" section for Twitter updates, "favorites" is equivalent to "likes". We have left this as "favorites" for now for backward compatibility and will be changing it to "likes" in the next version of the Buffer API.

#### Example Request

```
POST https://api.bufferapp.com/1/updates/4ecda256512f7ee521000004/move_to_top
     .json

{
  "id": "4eb8565e0acb04bb82000004",
  "created_at": 1320703582,
  "day": "Monday 7th November",
  "due_at": 1320742680,
  "due_time": "10:09 pm",
  "profile_id": "4eb854340acb04e870000010",
  "profile_service": "twitter",
  "sent_at": 1320744001,
  "service_update_id": "133667319959392256",
  "statistics": {
    "reach": 2460,
    "clicks": 56,
    "retweets": 20,
    "favorites": 1,
    "mentions": 1
  },
  "status": "sent",
  "text": "This is just the beginning, the very beginning, of the transfor...",
  "text_formatted": "This is just the beginning, the very beginning, of th...",
  "user_id": "4eb9276e0acb04bb81000067",
  "via": "chrome"
}
```
