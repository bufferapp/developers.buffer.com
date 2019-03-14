+++
title = "Users"
menu = "main"
weight = 20
+++

A user represents a single Buffer user account.

### Get

[/user](#get-user)

### Post

[/user/deauthorize](#post-user-deauthorize)

### GET /user

Returns a single user.

#### Example Request

```
GET https://api.bufferapp.com/1/user.json

{
  "_id":"4f0c0a06512f7ef214000000",
  "activity_at":1343654640,
  "created_at":1326189062,
  "id":"4f0c0a06512f7ef214000000",
  "plan":"free",
  "timezone":"Asia/Tel_Aviv"
}
```

### POST /user/deauthorize

Deauthorize your client for the user.

#### Example Request

```
POST https://api.bufferapp.com/1/user/deauthorize.json

{
  "success": true,
  "message": "Access successfully revoked!"
}
```
