# Soundcloud API

SoundCloud API. Search for artists, tracks, albums, and playlists. Get detailed info on your favorites and grab stream URLs for listening or downloading.

## Table of contents
- 1 Album
	- 1.1 Search albums
	- 1.2 Get album
- 2 Playlist
	- 2.1 Search playlists
	- 2.2 Get playlist
- 3 Track
	- 3.1 Search tracks
	- 3.2 Get track
- 4 User
	- 4.1 Search users
	- 4.2 Get user
- 5 Stream
	- 5.1 Get stream or download
- 6 Errors and warnings
	- 6.1 Errors
	- 6.2 Warnings


## 1 Album

### 1.1 Search albums

Find albums by a query, use `/v2/album/get` endpoint for a single album, using the IDs from this endpoint

**URL:** `/v2/album/search`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| query | string | - | **Required if token is not set**<br>The query to find results from. | true | Marshmello |
| token | string | - | **Optional**<br>Pagination token from previous response as the `meta.nextToken` to get the next batch of results. | false |  |


#### Request example

```
/v2/album/search?query=album
```

#### Example response

```json
{
  "data": [
    {
      "artistId": 135929695,
      "artworkUrl": "",
      "createdAt": "2017-03-25T13:33:19Z",
      "description": "This is the Full Album Vario by Savant. [I don't own this music]",
      "durationMs": 4512233,
      "genre": "Electro",
      "id": 310254094,
      "labelName": "",
      "lastModified": "2017-04-16T06:51:46Z",
      "license": "all-rights-reserved",
      "likesCount": 42,
      "publishedAt": "2012-01-15T00:00:00Z",
      "repostsCount": 5,
      "soundcloudUrl": "https://api.soundcloud.com/playlists/soundcloud%3Aplaylists%3A310254094",
      "title": "Savant - Vario [Full Album]",
      "trackCount": 16,
      "tracks": [
        {
          "artistId": 2409289,
          "artworkUrl": "https://i1.sndcdn.com/artworks-000023027261-roxkbo-large.jpg",
          "caption": "",
          "commentCount": 616,
          "createdAt": "2012-05-09T04:04:55Z",
          "description": "",
          "downloadCount": 0,
          "durationMs": 297058,
          "genre": "Electro House",
          "id": 45784550,
          "labelName": "SectionZ Records",
          "lastModified": "2021-11-10T17:03:18Z",
          "license": "all-rights-reserved",
          "likesCount": 17221,
          "permalink": "savant-splinter",
          "playbackCount": 1300587,
          "repostsCount": 2179,
          "soundcloudUrl": "https://api.soundcloud.com/tracks/soundcloud%3Atracks%3A45784550",
          "title": "Savant - Splinter",
          "trackAuthorization": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
          "tracks": [
            {
              "durationMs": 297058,
              "mimeType": "audio/mp4; codecs=\"mp4a.40.2\"",
              "preset": "aac_160k",
              "protocol": "hls",
              "quality": "sq",
              "streamId": "soundcloud:tracks:45784550/e66bdde0-d57d-40fc-a142-6f566b55593f/stream/hls"
            }
          ],
          "visuals": []
        },
        {
          "artistId": 14087059,
          "artworkUrl": "https://i1.sndcdn.com/artworks-000020455058-e5rpr8-large.jpg",
          "caption": "",
          "commentCount": 44,
          "createdAt": "2012-03-24T08:06:40Z",
          "description": "",
          "downloadCount": 0,
          "durationMs": 200248,
          "genre": "Dubstep, Glitch Hop, Electro House",
          "id": 40781264,
          "labelName": "",
          "lastModified": "2017-06-19T18:06:29Z",
          "license": "all-rights-reserved",
          "likesCount": 1651,
          "permalink": "02-savant-vario-original-mix",
          "playbackCount": 135131,
          "repostsCount": 189,
          "soundcloudUrl": "https://api.soundcloud.com/tracks/soundcloud%3Atracks%3A40781264",
          "title": "Vario (Original Mix)",
          "trackAuthorization": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
          "tracks": [
            {
              "durationMs": 200248,
              "mimeType": "audio/mp4; codecs=\"mp4a.40.2\"",
              "preset": "aac_160k",
              "protocol": "hls",
              "quality": "sq",
              "streamId": "soundcloud:tracks:40781264/5eb74492-9d36-4c54-b647-eb1bfe124822/stream/hls"
            }
          ],
          "visuals": []
        }
      ]
    }
  ],
  "meta": {
    "position": 0,
    "count": 23,
    "nextToken": ""
  },
  "_links": {
    "self": "/v2/album/search?query=savant",
    "next": ""
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}

```

### Pagination

To get the next batch of results the `meta.nextToken` from the response can be used.
For how the request should look, the `_links.next` gives an example.

Generally the other URL-parameters can be left out if the `token` is set, but it will work even when the other
parameters are present.

#### nextToken example from response:

```json
{
  "data": [],
  "meta": {
    "nextToken": "dG9rZW49ODY5ODU..."
  },
  "_links": {
    "next": "/v2/album/search?token=dG9rZW49ODY5ODU..."
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}
```

#### token example request:

`/v2/album/search?token=dG9rZW49ODY5ODU...`



### 1.2 Get album

Get an album by ID, use the `/v2/album/search` endpoint to search for albums and IDs.

**URL:** `/v2/album/get`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| id | string | - | **Required**<br>ID of the item, to get allowed values, use the `search` endpoint.<br>**Allowed format**<br>^\d+$ | true |  |


#### Request example

```
/v2/album/get?id=4175032607
```

#### Example response

```json
{
  "data": {
    "artistId": 99451619,
    "artworkUrl": "",
    "createdAt": "2014-08-04T15:56:09Z",
    "description": "",
    "durationMs": 3053482,
    "genre": "",
    "id": 45784550,
    "labelName": "",
    "lastModified": "2014-08-04T15:56:09Z",
    "license": "all-rights-reserved",
    "likesCount": 1,
    "publishedAt": "",
    "repostsCount": 1,
    "soundcloudUrl": "https://api.soundcloud.com/playlists/soundcloud%3Aplaylists%3A45784550",
    "title": "Bayrtsengel",
    "trackCount": 12,
    "tracks": [
      {
        "artistId": 46214235,
        "artworkUrl": "https://i1.sndcdn.com/artworks-000058345218-85umeg-large.jpg",
        "caption": "",
        "commentCount": 88,
        "createdAt": "2013-09-22T02:59:03Z",
        "description": "",
        "downloadCount": 0,
        "durationMs": 240216,
        "genre": "House",
        "id": 111654054,
        "labelName": "",
        "lastModified": "2021-01-05T06:52:23Z",
        "license": "all-rights-reserved",
        "likesCount": 8440,
        "permalink": "animal-martin-garrix",
        "playbackCount": 861847,
        "repostsCount": 911,
        "soundcloudUrl": "https://api.soundcloud.com/tracks/soundcloud%3Atracks%3A111654054",
        "title": "Animal - Martin Garrix",
        "trackAuthorization": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
        "tracks": [
          {
            "durationMs": 240216,
            "mimeType": "audio/mp4; codecs=\"mp4a.40.2\"",
            "preset": "aac_160k",
            "protocol": "hls",
            "quality": "sq",
            "streamId": "soundcloud:tracks:111654054/cf436c2e-01b2-4a4b-9ff5-94ebc316ff80/stream/hls"
          }
        ],
        "visuals": []
      }
    ]
  },
  "_links": {
    "self": "/v2/album/get?id=45784550"
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}

```


## 2 Playlist

### 2.1 Search playlists

Find playlists by a query, use `/v2/playlist/get` endpoint for a single playlist, using the IDs from this endpoint

**URL:** `/v2/playlist/search`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| query | string | - | **Required if token is not set**<br>The query to find results from. | true | Marshmello |
| token | string | - | **Optional**<br>Pagination token from previous response as the `meta.nextToken` to get the next batch of results. | false |  |


#### Request example

```
/v2/playlist/search?query=playlist
```

#### Example response

```json
{
  "data": [
    {
      "artistId": 38913086,
      "artworkUrl": "https://i1.sndcdn.com/artworks-ddAyLnZaEq1Af6TI-gtusqA-large.jpg",
      "createdAt": "2019-05-26T03:08:00Z",
      "description": "",
      "durationMs": 6108870,
      "genre": "Savant",
      "id": 789349965,
      "labelName": "",
      "lastModified": "2021-07-08T17:59:48Z",
      "license": "all-rights-reserved",
      "likesCount": 58,
      "publishedAt": "",
      "repostsCount": 3,
      "soundcloudUrl": "https://api.soundcloud.com/playlists/soundcloud%3Aplaylists%3A789349965",
      "title": "Savant - Alchemist",
      "trackCount": 22,
      "tracks": [
        {
          "artistId": 173883661,
          "artworkUrl": "https://i1.sndcdn.com/artworks-000207829231-22ti54-large.jpg",
          "caption": "",
          "commentCount": 1,
          "createdAt": "2017-02-15T01:06:42Z",
          "description": "A sweet bass house track from Savant...",
          "downloadCount": 0,
          "durationMs": 309859,
          "genre": "House",
          "id": 307792608,
          "labelName": "",
          "lastModified": "2017-12-20T20:14:54Z",
          "license": "all-rights-reserved",
          "likesCount": 229,
          "permalink": "savant-mother-earth-reupload",
          "playbackCount": 14050,
          "repostsCount": 12,
          "soundcloudUrl": "https://api.soundcloud.com/tracks/soundcloud%3Atracks%3A307792608",
          "title": "Savant - Mother Earth [ReUpload]",
          "trackAuthorization": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
          "tracks": [
            {
              "durationMs": 309859,
              "mimeType": "audio/mp4; codecs=\"mp4a.40.2\"",
              "preset": "aac_160k",
              "protocol": "hls",
              "quality": "sq",
              "streamId": "soundcloud:tracks:307792608/4a90f615-0c63-440d-a58f-2e32b59f88b7/stream/hls"
            }
          ],
          "visuals": []
        }
      ]
    }
  ],
  "meta": {
    "position": 0,
    "count": 24,
    "nextToken": ""
  },
  "_links": {
    "self": "/v2/playlist/search?query=savant",
    "next": ""
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}

```

### Pagination

To get the next batch of results the `meta.nextToken` from the response can be used.
For how the request should look, the `_links.next` gives an example.

Generally the other URL-parameters can be left out if the `token` is set, but it will work even when the other
parameters are present.

#### nextToken example from response:

```json
{
  "data": [],
  "meta": {
    "nextToken": "dG9rZW49ODY5ODU..."
  },
  "_links": {
    "next": "/v2/playlist/search?token=dG9rZW49ODY5ODU..."
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}
```

#### token example request:

`/v2/playlist/search?token=dG9rZW49ODY5ODU...`



### 2.2 Get playlist

Get a playlist by ID, use the `/v2/playlist/search` endpoint to search for playlists and IDs.

**URL:** `/v2/playlist/get`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| id | string | - | **Required**<br>ID of the item, to get allowed values, use the `search` endpoint.<br>**Allowed format**<br>^\d+$ | true |  |


#### Request example

```
/v2/playlist/get?id=4175032607
```

#### Example response

```json
{
  "data": {
    "artistId": 38913086,
    "artworkUrl": "https://i1.sndcdn.com/artworks-ddAyLnZaEq1Af6TI-gtusqA-large.jpg",
    "createdAt": "2019-05-26T03:08:00Z",
    "description": "",
    "durationMs": 6108870,
    "genre": "Savant",
    "id": 789349965,
    "labelName": "",
    "lastModified": "2021-07-08T17:59:48Z",
    "license": "all-rights-reserved",
    "likesCount": 58,
    "publishedAt": "",
    "repostsCount": 3,
    "soundcloudUrl": "https://api.soundcloud.com/playlists/soundcloud%3Aplaylists%3A789349965",
    "title": "Savant - Alchemist",
    "trackCount": 22,
    "tracks": [
      {
        "artistId": 173883661,
        "artworkUrl": "https://i1.sndcdn.com/artworks-000207829231-22ti54-large.jpg",
        "caption": "",
        "commentCount": 1,
        "createdAt": "2017-02-15T01:06:42Z",
        "description": "A sweet bass house track from Savant...",
        "downloadCount": 0,
        "durationMs": 309859,
        "genre": "House",
        "id": 307792608,
        "labelName": "",
        "lastModified": "2017-12-20T20:14:54Z",
        "license": "all-rights-reserved",
        "likesCount": 229,
        "permalink": "savant-mother-earth-reupload",
        "playbackCount": 14050,
        "repostsCount": 12,
        "soundcloudUrl": "https://api.soundcloud.com/tracks/soundcloud%3Atracks%3A307792608",
        "title": "Savant - Mother Earth [ReUpload]",
        "trackAuthorization": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
        "tracks": [
          {
            "durationMs": 309859,
            "mimeType": "audio/mp4; codecs=\"mp4a.40.2\"",
            "preset": "aac_160k",
            "protocol": "hls",
            "quality": "sq",
            "streamId": "soundcloud:tracks:307792608/4a90f615-0c63-440d-a58f-2e32b59f88b7/stream/hls"
          }
        ],
        "visuals": []
      }
    ]
  },
  "_links": {
    "self": "/v2/playlist/get?id=789349965"
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}

```


## 3 Track

### 3.1 Search tracks

Find tracks by a query, use `/v2/track/get` endpoint for a single track, using the IDs from this endpoint

**URL:** `/v2/track/search`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| query | string | - | **Required if token is not set**<br>The query to find results from. | true | Marshmello |
| token | string | - | **Optional**<br>Pagination token from previous response as the `meta.nextToken` to get the next batch of results. | false |  |


#### Request example

```
/v2/track/search?query=track
```

#### Example response

```json
{
  "data": [
    {
      "artistId": 1348672314,
      "artworkUrl": "https://i1.sndcdn.com/artworks-TNYBA5lGWxkTjRxc-BL4WAQ-large.jpg",
      "caption": "",
      "commentCount": 6,
      "createdAt": "2024-11-22T02:25:21Z",
      "description": "t.me/killmylove",
      "downloadCount": 0,
      "durationMs": 181133,
      "genre": "Hip-hop & Rap",
      "id": 1964289683,
      "labelName": "",
      "lastModified": "2025-08-20T15:36:34Z",
      "license": "all-rights-reserved",
      "likesCount": 624,
      "permalink": "ivycraft-ayena-savant-angels",
      "playbackCount": 34524,
      "repostsCount": 12,
      "soundcloudUrl": "https://api.soundcloud.com/tracks/soundcloud%3Atracks%3A1964289683",
      "title": "ivycraft, ayena savant - angels watching from a distance",
      "trackAuthorization": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
      "tracks": [
        {
          "durationMs": 181133,
          "mimeType": "audio/mpegurl",
          "preset": "abr_sq",
          "protocol": "hls",
          "quality": "sq",
          "streamId": "soundcloud:tracks:1964289683/6422f8c8-a1f2-4838-bc0b-f5d851c2b166/stream/hls"
        }
      ],
      "visuals": []
    }
  ],
  "meta": {
    "position": 0,
    "count": 25,
    "nextToken": "cD0xO3E9c2F2YW50"
  },
  "_links": {
    "self": "/v2/track/search?query=savant",
    "next": "/v2/track/search?token=cD0xO3E9c2F2YW50"
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}

```

### Pagination

To get the next batch of results the `meta.nextToken` from the response can be used.
For how the request should look, the `_links.next` gives an example.

Generally the other URL-parameters can be left out if the `token` is set, but it will work even when the other
parameters are present.

#### nextToken example from response:

```json
{
  "data": [],
  "meta": {
    "nextToken": "dG9rZW49ODY5ODU..."
  },
  "_links": {
    "next": "/v2/track/search?token=dG9rZW49ODY5ODU..."
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}
```

#### token example request:

`/v2/track/search?token=dG9rZW49ODY5ODU...`



### 3.2 Get track

Get a track by ID, use the `/v2/track/search` endpoint to search for tracks and IDs.

**URL:** `/v2/track/get`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| id | string | - | **Required**<br>ID of the item, to get allowed values, use the `search` endpoint.<br>**Allowed format**<br>^\d+$ | true |  |


#### Request example

```
/v2/track/get?id=4175032607
```

#### Example response

```json
{
  "data": {
    "artistId": 46214235,
    "artworkUrl": "https://i1.sndcdn.com/artworks-000058345218-85umeg-large.jpg",
    "caption": "",
    "commentCount": 88,
    "createdAt": "2013-09-22T02:59:03Z",
    "description": "",
    "downloadCount": 0,
    "durationMs": 240216,
    "genre": "House",
    "id": 111654054,
    "labelName": "",
    "lastModified": "2021-01-05T06:52:23Z",
    "license": "all-rights-reserved",
    "likesCount": 8440,
    "permalink": "animal-martin-garrix",
    "playbackCount": 861847,
    "repostsCount": 911,
    "soundcloudUrl": "https://api.soundcloud.com/tracks/soundcloud%3Atracks%3A111654054",
    "title": "Animal - Martin Garrix",
    "trackAuthorization": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...",
    "tracks": [
      {
        "durationMs": 240216,
        "mimeType": "audio/mp4; codecs=\"mp4a.40.2\"",
        "preset": "aac_160k",
        "protocol": "hls",
        "quality": "sq",
        "streamId": "soundcloud:tracks:111654054/cf436c2e-01b2-4a4b-9ff5-94ebc316ff80/stream/hls"
      }
    ],
    "visuals": []
  },
  "_links": {
    "self": "/v2/track/get?id=111654054"
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}

```


## 4 User

### 4.1 Search users

Find users and artists by a query, use `/v2/user/get` endpoint for a single user, using the IDs from this endpoint

**URL:** `/v2/user/search`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| query | string | - | **Required if token is not set**<br>The query to find results from. | true | Marshmello |
| token | string | - | **Optional**<br>Pagination token from previous response as the `meta.nextToken` to get the next batch of results. | false |  |


#### Request example

```
/v2/user/search?query=user
```

#### Example response

```json
{
  "data": [
    {
      "avatarUrl": "https://i1.sndcdn.com/avatars-MyDIDwvBqWsxb03q-1phWFQ-large.jpg",
      "city": "https://i1.sndcdn.com/avatars-MyDIDwvBqWsxb03q-1phWFQ-large.jpg",
      "countryCode": "",
      "createdAt": "2016-03-04T04:49:15Z",
      "description": "MGMT: z@zyon.io",
      "firstName": "Aleksander",
      "followerCount": 20447,
      "followingCount": 11,
      "id": 209960820,
      "isVerified": false,
      "lastModified": "2025-04-25T15:12:20Z",
      "lastName": "Aleksander",
      "permalink": "savantofficial",
      "playlistCount": 7,
      "soundcloudUrl": "https://api.soundcloud.com/users/soundcloud%3Ausers%3A209960820",
      "trackCount": 183,
      "type": "user",
      "username": "Savant",
      "visuals": [
        "https://i1.sndcdn.com/visuals-000209960820-EL9JHX-original.jpg"
      ]
    }
  ],
  "meta": {
    "position": 0,
    "count": 25,
    "nextToken": "cD0xO3E9c2F2YW50"
  },
  "_links": {
    "self": "/v2/user/search?query=savant",
    "next": "/v2/user/search?token=cD0xO3E9c2F2YW50"
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}

```

### Pagination

To get the next batch of results the `meta.nextToken` from the response can be used.
For how the request should look, the `_links.next` gives an example.

Generally the other URL-parameters can be left out if the `token` is set, but it will work even when the other
parameters are present.

#### nextToken example from response:

```json
{
  "data": [],
  "meta": {
    "nextToken": "dG9rZW49ODY5ODU..."
  },
  "_links": {
    "next": "/v2/user/search?token=dG9rZW49ODY5ODU..."
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}
```

#### token example request:

`/v2/user/search?token=dG9rZW49ODY5ODU...`



### 4.2 Get user

Get a user or artist by ID, use the `/v2/user/search` endpoint to search for users and IDs.

**URL:** `/v2/user/get`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| id | string | - | **Required**<br>ID of the item, to get allowed values, use the `search` endpoint.<br>**Allowed format**<br>^\d+$ | true |  |


#### Request example

```
/v2/user/get?id=4175032607
```

#### Example response

```json
{
  "data": {
    "avatarUrl": "https://i1.sndcdn.com/avatars-auktj8Y7Qeuun8sL-u9qyFw-large.jpg",
    "city": "https://i1.sndcdn.com/avatars-auktj8Y7Qeuun8sL-u9qyFw-large.jpg",
    "countryCode": "US",
    "createdAt": "2014-06-13T06:02:21Z",
    "description": "",
    "firstName": "Post Malone",
    "followerCount": 2272574,
    "followingCount": 11,
    "id": 99685284,
    "isVerified": true,
    "lastModified": "2025-12-18T15:43:54Z",
    "lastName": "Post Malone",
    "permalink": "postmalone",
    "playlistCount": 18,
    "soundcloudUrl": "https://api.soundcloud.com/users/soundcloud%3Ausers%3A99685284",
    "trackCount": 190,
    "type": "user",
    "username": "Post Malone",
    "visuals": [
      "https://i1.sndcdn.com/visuals-000099685284-Gi1rUp-original.jpg"
    ]
  },
  "_links": {
    "self": "/v2/user/get?id=99685284"
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}

```


## 5 Stream

### 5.1 Get stream or download

Get a stream or a download by the `streamId` and `trackAuthorization`, to get those values use either the `/v2/track/search` or `/v2/track/get` endpoint.

**URL:** `/v2/stream/get`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| streamId | string | - | **Required**<br>ID of the stream, use the track-endpoints to get this value. | true | soundcloud:tracks:1516134547/96e00d35-0212-4081-b327-bac176d19325/stream/hls |
| trackAuthorization | string | - | **Required**<br>Authorization of the stream, use the track-endpoints to get this value. | true | eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJnZW8iOiJERSIsInN1YiI6IiIsInJpZCI6IjI3NWY0ZWJjLWRiMDItNDVkNi04NzMxLWE0OTU0ZGI3YmExMyIsImlhdCI6MTc2OTk0MjE2MX0.5tl35gVpDdLlNY5-lje8NC_APG5dPFwRy93kiFdEcpM |


#### Request example

```
/v2/stream/get?streamId=soundcloud:tracks:15794.../stream/hls&trackAuthorization=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9...
```

#### Example response

```json
{
  "data": {
    "streamUrl": "https://cf-media.sndcdn.com/E82p48GVrxFp..."
  },
  "_links": {
    "self": "/v2/stream/get?streamId=soundcloud:tracks..."
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}

```




## 6 Errors and warnings

There are two types of possible issues, either you have an error, then nothing will be returned, except the error, or
you have warnings then the result will be returned, but also some warnings will be set.

The fields **hasError** and **hasWarning** in the response indicate whether the response contains errors or warnings:

- **hasError**: This field is `true` if the response contains any errors. If set to `false`, the response has no errors.
- **hasWarning**: This field is `true` if the response contains any warnings. If set to `false`, the response has no
  warnings.

### 6.1 Errors

#### Common error Codes

| code | error                    | message                                                                   | description                                                          |
|------|--------------------------|---------------------------------------------------------------------------|----------------------------------------------------------------------|
| 400  | MISSING_PARAMETER        | 400: Required parameter '...' is missing.                                 | A mandatory URL-parameter is missing.                                |
| 400  | MISSING_OR_PARAMETER     | 400: Either parameter '...' or parameter '...' must to be set.            | One of two URL-parameters must be set, but both are missing.         |
| 400  | INVALID_PARAMETER        | 400: Parameter '...' contains an invalid value, valid values are ...      | An invalid value has been set for an URL-parameter.                  |
| 400  | INVALID_PARAMETER_FORMAT | 400: The value of parameter '...' does not match the expected format: ... | The format of the URL-parameter is not valid, or has the wrong type. |
| 504  | PROXY_TIMEOUT            | 504: Proxy timed out, please try again.                                   | The proxy service timed-out, this usually works again after a retry. |
| 500  | UNEXPECTED_EXCEPTION     | 500: An unexpected error occurred.                                        | Something happened that was not planned for.                         |

#### Error response example

```json
{
  "data": [],
  "meta": {},
  "_links": {},
  "errors": [
    {
      "code": 400,
      "error": "MISSING_OR_PARAMETER",
      "message": "400: Either parameter 'countryCode' or parameter 'token' must to be set.",
      "field": "countryCode OR token"
    },
    {
      "code": 400,
      "error": "MISSING_OR_PARAMETER",
      "message": "400: Either parameter 'query' or parameter 'token' must to be set.",
      "field": "query OR token"
    }
  ],
  "warnings": [],
  "hasError": true,
  "hasWarning": false
}
```

### 6.2 Warnings

#### Common warning Codes

| code | error                     | message                                          | description                                                                                                   |
|------|---------------------------|--------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| 200  | UNKNOWN_PARAMETER         | 200: Parameter '...' is unknown and was ignored. | A unknown URL-parameter has been set, it will be ignored and the endpoint will return the result as expected. |
| 200  | NOT_RECOMMENDED_PARAMETER | 200: Parameter '...' is not recommended.         | A not recommended URL-parameter has been set, this message will also include a better approach.               |

#### Warning response example

```json
{
  "data": [],
  "meta": {},
  "_links": {},
  "errors": [],
  "warnings": [
    {
      "code": 200,
      "error": "UNKNOWN_PARAMETER",
      "message": "200: Parameter 'invalidParam' is unknown and was ignored.",
      "field": "invalidParam"
    }
  ],
  "hasError": false,
  "hasWarning": true
}
```