+++
title = "Profiles"
menu = "main"
weight = 30
+++

A Buffer profile represents a connection to a single social media account.

### Get

[/profiles](#get-profiles)

[/profiles/:id](#get-profiles-id)

[/profiles/:id/schedules](#get-profiles-id-schedules)

### Post

[/profiles/:id/schedules/update](#post-profiles-id-schedules-update)

### GET /profiles

Returns an array of social media profiles connected to a users account.

#### Example Request

```
GET https://api.bufferapp.com/1/profiles.json

[ {
    "avatar" : "http://a3.twimg.com/profile_images/1405180232.png",
    "created_at" :  1320703028,
    "default" : true,
    "formatted_username" : "@skinnyoteam",
    "id" : "4eb854340acb04e870000010",
    "schedules" : [{
        "days" : [
            "mon",
            "tue",
            "wed",
            "thu",
            "fri"
        ],
        "times" : [
            "12:00",
            "17:00",
            "18:00"
        ]
    }],
    "service" : "twitter",
    "service_id" : "164724445",
    "service_username" : "skinnyoteam",
    "statistics" : {
        "followers" : 246
    },
    "team_members" : [
        "4eb867340acb04e670000001"
    ],
    "timezone" : "Europe/London",
    "user_id" : "4eb854340acb04e870000010"
  },
  {
	...
  }
]
```

### GET /profiles/:id

Returns details of the single specified social media profile.

#### Example Request

```
GET https://api.bufferapp.com/1/profiles/4eb854340acb04e870000010.json

{
  "avatar" : "http://a3.twimg.com/profile_images/1405180232.png",
  "created_at" :  1320703028,
  "default" : true,
  "formatted_username" : "@skinnyoteam",
  "id" : "4eb854340acb04e870000010",
  "schedules" : [{
      "days" : [
          "mon",
          "tue",
          "wed",
          "thu",
          "fri"
      ],
      "times" : [
          "12:00",
          "17:00",
          "18:00"
      ]
  }],
  "service" : "twitter",
  "service_id" : "164724445",
  "service_username" : "skinnyoteam",
  "statistics" : {
      "followers" : 246
  },
  "team_members" : [
      "4eb867340acb04e670000001"
  ],
  "timezone" : "Europe/London",
  "user_id" : "4eb854340acb04e870000010"
}
```

### GET /profiles/:id/schedules

Returns details of the posting schedules associated with a social media profile.

#### Example Request

```
GET https://api.bufferapp.com/1/profiles/4eb854340acb04e870000010/schedules.json

[{
  "days" : [
      "mon",
      "tue",
      "wed",
      "thu",
      "fri"
  ],
  "times" : [
      "12:00",
      "17:00",
      "18:00"
  ]
},
{
  ...
}]
```

### POST /profiles/:id/schedules/update

Set the posting schedules for the specified social media profile.

#### Parameters

* `schedules` (required)
* `array`

Each item in the array is an individual posting schedule which consists of days and times to match the format return by the above method.

#### Example Request

```
POST https://api.bufferapp.com/1/profiles/4eb854340acb04e870000010/schedules/upda
te.json

POST Data
    schedules[0][days][]=mon&
    schedules[0][days][]=tue&
    schedules[0][days][]=thu&
    schedules[0][times][]=12:45&
    schedules[0][times][]=15:30&
    schedules[0][times][]=17:43&

{
    "success": true
}
```
