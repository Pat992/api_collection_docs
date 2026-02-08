# Search API

Search API to find results across multiple Search-engines like Google, Bing, Yahoo or DuckDuckGo

## Table of contents
- 1 Search
	- 1.1 Search Bing
	- 1.2 Search DuckDuckGo
	- 1.3 Search Google
	- 1.4 Search Yahoo
	- 1.5 Search Yahoo Japan
- 2 Errors and warnings
	- 2.1 Errors
	- 2.2 Warnings


## 1 Search

### 1.1 Search Bing

Search Bing and get results in a unified JSON format.

**URL:** `/v1/search/bing`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| query | string | - | **Required if token is not set**<br>Any Keywords to get results from. | true | test |
| countryCode | string | - | **Required if token is not set**<br>Country code from what country the results are from.<br>**Allowed format**<br>^[A-Za-z]{2}$ | true | us |
| datePosted | string | - | **Optional**<br>The maximum age of when a result was added to the search-engine, will return everything by default. | false | month |
| safeSearch | string | off, moderate or strict | **Optional**<br>Filter sensitive content, is moderate by default.<br>**Allowed values**<br>off, moderate or strict | false | off |
| token | string | - | **Optional**<br>Pagination token from previous response as the `meta.nextToken` to get the next batch of results. | false |  |


#### Request example

```
/v1/search/bing?query=Test&countryCode=us&datePosted=month&safeSearch=off
```

#### Example response

```json
{
  "data": [
    {
      "description": "Rust is blazingly fast and memory-efficient…",
      "title": "Rust Programming Language",
      "url": "https://www.bing.com/ck/a?!&&p=c79..."
    },
    {
      "description": "The only aim in Rust is to survive...",
      "title": "Rust — Explore, Build and Survive",
      "url": "https://www.bing.com/ck/a?!&&p=27..."
    },
    {
      "description": "Rust is a general-purpose programming language…",
      "title": "Rust (programming language) - Wikipedia",
      "url": "https://www.bing.com/ck/a?!&&p=29..."
    },
    {
      "description": "The only aim in Rust is to survive...",
      "title": "Save 50% on Rust on Steam",
      "url": "https://www.bing.com/ck/a?!&&p=50..."
    }
  ],
  "meta": {
    "position": 0,
    "count": 10,
    "nextToken": "dD1NVUlEJTVCRVE..."
  },
  "_links": {
    "self": "/v1/search/bing?query=rust&countryCode=us",
    "next": "/v1/search/bing?token=dD1NVUlEJTVCRVE..."
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
    "next": "/v1/search/bing?token=dG9rZW49ODY5ODU..."
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}
```

#### token example request:

`/v1/search/bing?token=dG9rZW49ODY5ODU...`



### 1.2 Search DuckDuckGo

Search DuckDuckGo and get results in a unified JSON format.

**URL:** `/v1/search/duckduckgo`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| query | string | - | **Required if token is not set**<br>Any Keywords to get results from. | true | test |
| countryCode | string | - | **Required if token is not set**<br>Country code from what country the results are from.<br>**Allowed format**<br>^[A-Za-z]{2}$ | true | us |
| datePosted | string | - | **Optional**<br>The maximum age of when a result was added to the search-engine, will return everything by default. | false | month |
| safeSearch | string | off, moderate or strict | **Optional**<br>Filter sensitive content, is moderate by default.<br>**Allowed values**<br>off, moderate or strict | false | off |
| token | string | - | **Optional**<br>Pagination token from previous response as the `meta.nextToken` to get the next batch of results. | false |  |


#### Request example

```
/v1/search/duckduckgo?query=Test&countryCode=us&datePosted=month&safeSearch=off
```

#### Example response

```json

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
    "next": "/v1/search/duckduckgo?token=dG9rZW49ODY5ODU..."
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}
```

#### token example request:

`/v1/search/duckduckgo?token=dG9rZW49ODY5ODU...`



### 1.3 Search Google

Search Google and get results in a unified JSON format.

**URL:** `/v1/search/google`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| query | string | - | **Required if token is not set**<br>Any Keywords to get results from. | true | test |
| countryCode | string | - | **Required if token is not set**<br>Country code from what country the results are from.<br>**Allowed format**<br>^[A-Za-z]{2}$ | true | us |
| datePosted | string | - | **Optional**<br>The maximum age of when a result was added to the search-engine, will return everything by default. | false | month |
| safeSearch | string | off, moderate or strict | **Optional**<br>Filter sensitive content, is moderate by default.<br>**Allowed values**<br>off, moderate or strict | false | off |
| token | string | - | **Optional**<br>Pagination token from previous response as the `meta.nextToken` to get the next batch of results. | false |  |


#### Request example

```
/v1/search/google?query=Test&countryCode=us&datePosted=month
```

#### Example response

```json
{
  "data": [
    {
      "description": "<b>Rust</b> is blazingly fast and memory-efficient...",
      "title": "Rust Programming Language",
      "url": "https://rust-lang.org/"
    },
    {
      "description": "The only aim in <b>Rust</b> is to survive...",
      "title": "Rust — Explore, Build and Survive",
      "url": "https://rust.facepunch.com/"
    },
    {
      "description": "The only aim in <b>Rust</b> is to survive...",
      "title": "Save 50% on Rust on Steam",
      "url": "https://store.steampowered.com/app/252490/Rust/"
    },
    {
      "description": "It&#39;s a simple terminal tool to test download/upload speeds...",
      "title": "The Rust Programming Language - Reddit",
      "url": "https://www.reddit.com/r/rust/"
    }
  ],
  "meta": {
    "position": 0,
    "count": 10,
    "nextToken": "dD1wc2h5TGZ..."
  },
  "_links": {
    "self": "/v1/search/google?query=rust&countryCode=us",
    "next": "/v1/search/google?token=dD1wc2h5TGZ..."
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
    "next": "/v1/search/google?token=dG9rZW49ODY5ODU..."
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}
```

#### token example request:

`/v1/search/google?token=dG9rZW49ODY5ODU...`



### 1.4 Search Yahoo

Search Yahoo and get results in a unified JSON format.

**URL:** `/v1/search/yahoo`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| query | string | - | **Required if token is not set**<br>Any Keywords to get results from. | true | test |
| datePosted | string | - | **Optional**<br>The maximum age of when a result was added to the search-engine, will return everything by default. | false | month |
| token | string | - | **Optional**<br>Pagination token from previous response as the `meta.nextToken` to get the next batch of results. | false |  |


#### Request example

```
/v1/search/yahoo?query=Test&datePosted=month
```

#### Example response

```json
{
  "data": [
    {
      "description": "Rust is a fast, memory-safe, and productive...",
      "title": "",
      "url": "https://rust-lang.org/"
    },
    {
      "description": "The only aim in Rust is to survive...",
      "title": "",
      "url": "https://rust.facepunch.com/"
    },
    {
      "description": "Rust is a general-purpose programming language...",
      "title": "",
      "url": "https://en.wikipedia.org/wiki/Rust_(programming_language)"
    },
    {
      "description": "About This GameExploreBuildSurvive",
      "title": "",
      "url": "https://store.steampowered.com/app/252490/Rust/"
    }
  ],
  "meta": {
    "position": 0,
    "count": 7,
    "nextToken": "dD0lNUIlM0El..."
  },
  "_links": {
    "self": "/v1/search/yahoo?query=rust",
    "next": "/v1/search/yahoo?token=dD0lNUIlM0El..."
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
    "next": "/v1/search/yahoo?token=dG9rZW49ODY5ODU..."
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}
```

#### token example request:

`/v1/search/yahoo?token=dG9rZW49ODY5ODU...`



### 1.5 Search Yahoo Japan

Search Yahoo-Japan and get results in a unified JSON format.

**URL:** `/v1/search/yahoo-japan`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| query | string | - | **Required if token is not set**<br>Any Keywords to get results from. | true | test |
| datePosted | string | - | **Optional**<br>The maximum age of when a result was added to the search-engine, will return everything by default. | false | month |
| japaneseOnly | boolean | false or true | **Optional**<br>Filter by only japanese results, is set to `false` by default<br>**Allowed values**<br>false or true | false | false |
| token | string | - | **Optional**<br>Pagination token from previous response as the `meta.nextToken` to get the next batch of results. | false |  |


#### Request example

```
/v1/search/yahoo-japan?query=Test&datePosted=month&japaneseOnly=false
```

#### Example response

```json
{
  "data": [
    {
      "description": "『Rust』における唯一の目的は...",
      "title": "Steamで50% OFF：Rust",
      "url": "https://store.steampowered.com/app/252490/Rust/?l=japanese"
    },
    {
      "description": "Rustの豊かな型システム...",
      "title": "Rustプログラミング言語",
      "url": "https://rust-lang.org/ja/"
    },
    {
      "description": "Rust（ラスト）は、性能、...",
      "title": "Rust (プログラミング言語) - Wikipedia",
      "url": "https://ja.wikipedia.org/wiki/Rust..."
    },
    {
      "description": "2025年11月初開催！1st Closed...",
      "title": "今すぐ事前登録！ - Rust Mobile",
      "url": "https://www.rustmobile.com/ja/"
    }
  ],
  "meta": {
    "position": 0,
    "count": 10,
    "nextToken": "dD07cT1yd..."
  },
  "_links": {
    "self": "/v1/search/yahoo-japan?query=rust&japaneseOnly=true",
    "next": "/v1/search/yahoo-japan?token=dD07cT1yd..."
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
    "next": "/v1/search/yahoo-japan?token=dG9rZW49ODY5ODU..."
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}
```

#### token example request:

`/v1/search/yahoo-japan?token=dG9rZW49ODY5ODU...`





## 2 Errors and warnings

There are two types of possible issues, either you have an error, then nothing will be returned, except the error, or
you have warnings then the result will be returned, but also some warnings will be set.

The fields **hasError** and **hasWarning** in the response indicate whether the response contains errors or warnings:

- **hasError**: This field is `true` if the response contains any errors. If set to `false`, the response has no errors.
- **hasWarning**: This field is `true` if the response contains any warnings. If set to `false`, the response has no
  warnings.

### 2.1 Errors

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

### 2.2 Warnings

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