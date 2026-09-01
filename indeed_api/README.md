# Indeed API

This API allows you to discover worldwide employment opportunities from Indeed, as well as income information for different locations and jobs.

## Table of contents
- 1 Job search
	- 1.1 Search and list jobs
	- 1.2 Get job details
- 2 Salary range
	- 2.1 Get job titles
	- 2.2 Get job salaries
- 3 Errors and warnings
	- 3.1 Errors
	- 3.2 Warnings


## 1 Job search

### 1.1 Search and list jobs

Get a list of jobs from Indeed.

**URL:** `/v1/jobs/search`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| query | string | - | **Optional**<br>Keywords, job-title, company-name, position or any other relevant search-query. | false | Java |
| location | string | - | **Optional**<br>Location of the job offer, like city, towns or provinces. | false | Zurich |
| countryCode | string | - | **Required if token is not set**<br>Parameter to get the titles for the required county.<br>**Allowed format**<br>^[A-Za-z]{2}$ | true | ch |
| sortType | string | relevance or date | **Optional**<br>Sorting of the results, can either be by `relevance` or by `date`, will be set to `relevance` by default.<br>**Allowed values**<br>relevance or date | false | relevance |
| radius | integer | - | **Optional**<br>Distance of the job offers from the location.<br>**Allowed format**<br>^[0-9]+$ | false | 20 |
| radiusType | string | km or miles | **Optional**<br>Type of the distance, can either be `km` or `miles`, will be set to `km` by default.<br>**Allowed values**<br>km or miles | false | km |
| token | string | - | **Optional**<br>Pagination token from previous response as the `meta.nextToken` to get the next batch of results. | false |  |


#### Request example

```
/v1/jobs/search?location=zurich&query=java&countryCode=ch
```

#### Example response

```json
{
  "data": [
    {
      "applyUrl": "https://click.appcast.io/t/Jo4WXZskvtPZ9WgFwqnpCUVCv-vN0fkkJ6ip_S65XSY=",
      "company": {
        "addresses": ["Bethesda, MD"],
        "image": "https://d2q79iu7y748jz.cloudfront.net/s/_squarelogo/256x256/debbff68624041821d0c56fbccbcc330",
        "name": "Lockheed Martin"
      },
      "dateOnIndeedTimestamp": -2023594907,
      "datePublishedTimestamp": -749158656,
      "description": "Job ID: 691465BR\nDate posted: Nov. 30, 2025...",
      "id": "56a1b7550fa78bba",
      "location": {
        "country": "United States",
        "countryCode": "US",
        "location": "King of Prussia, PA"
      },
      "title": "Java Software Engineer III"
    },
    {
      "applyUrl": "https://click.appcast.io/t/q7vuN9iOmz3dRG2xAe7KoxP7I6Z7SQdG-wpiMdJf9nw=",
      "company": {
        "addresses": ["Bethesda, MD"],
        "image": "https://d2q79iu7y748jz.cloudfront.net/s/_squarelogo/256x256/debbff68624041821d0c56fbccbcc330",
        "name": "Lockheed Martin"
      },
      "dateOnIndeedTimestamp": -2023595367,
      "datePublishedTimestamp": -749158656,
      "description": "Job ID: 698997BR\nDate posted: Nov. 30, 2025...",
      "id": "6c588ac5af1876cc",
      "location": {
        "country": "United States",
        "countryCode": "US",
        "location": "King of Prussia, PA"
      },
      "title": "Java Software Engineer III- Space Mission Applications"
    },
    {
      "applyUrl": "https://click.appcast.io/t/TgmDjYI9cOSltDS4D0tQ4RxKivariwQLFIXeX5CIrPk=",
      "company": { "addresses": [], "image": "", "name": "GEICO" },
      "dateOnIndeedTimestamp": -2023807598,
      "datePublishedTimestamp": -2106525952,
      "description": "At GEICO, we offer a rewarding career...",
      "id": "5f9b5f874e6ab3a5",
      "location": {
        "country": "United States",
        "countryCode": "US",
        "location": "Chevy Chase, MD"
      },
      "title": "Staff Engineer - Applied AI"
    },
    {
      "applyUrl": "https://click.appcast.io/t/oP7qQFlODRAEfszK6tVzUXyMH5xMSoExd3UgIeLXVRQ=",
      "company": { "addresses": [], "image": "", "name": "GEICO" },
      "dateOnIndeedTimestamp": -2023808358,
      "datePublishedTimestamp": -2106525952,
      "description": "At GEICO, we offer a rewarding career...",
      "id": "2bcbfe330ed5c52f",
      "location": {
        "country": "United States",
        "countryCode": "US",
        "location": "New York, NY"
      },
      "title": "Senior Staff ML Engineer, Fraud Risk Modeling"
    }
  ],
  "meta": {
    "position": 0,
    "count": 20,
    "nextToken": "dD1BQlFBQVFBVUFBQUFBQ..."
  },
  "_links": {
    "self": "/v2/indeed/search?countryCode=us&query=java",
    "next": "/v2/indeed/search?token=dD1BQlFBQVFBVUFBQUFBQ..."
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
    "next": "/v1/jobs/search?token=dG9rZW49ODY5ODU..."
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}
```

#### token example request:

`/v1/jobs/search?token=dG9rZW49ODY5ODU...`



### 1.2 Get job details

Get job details by its ID, use the `/v1/jobs/search` endpoint to search for jobs and get valid IDs.

**URL:** `/v1/jobs/get`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| id | string | - | **Required**<br>ID of the job, to get allowed values, use the `search` endpoint. | true |  |


#### Request example

```
/v1/jobs/get?id=aWQ9ODRiYzJmMjY5ZTZlNGFkYjtjYz11cw==
```

#### Example response

```json
{
    "data": {
        "applyUrl": "https://careers.alaska.edu/jobs/junior-software-engineer-alaska-satellite-facility-asf-fairbanks-alaska-united-states",
        "company": {
            "addresses": [
                "2025 Yukon Drive, Fairbanks, AK 99775"
            ],
            "image": "https://d2q79iu7y748jz.cloudfront.net/s/_squarelogo/256x256/20a95ff792bbde097a2d4106d339944a",
            "name": "University of Alaska"
        },
        "dateOnIndeedTimestamp": 1788250823727,
        "datePublishedTimestamp": 1788238800000,
        "description": "533372\nFairbanks, Alaska, United States\nHybrid\nOn Campus\nRemote\nRemote within Alaska....",
        "id": "aWQ9NTI1YjhhN2I1MGY2NzAwYTtjYz11cw==",
        "location": {
            "country": "United States",
            "countryCode": "US",
            "location": "Fairbanks, AK"
        },
        "title": "Junior Software Engineer - Alaska Satellite Facility (ASF)"
    },
    "_links": {
        "self": "/v2/indeed/get?id=aWQ9NTI1YjhhN2I1MGY2NzAwYTtjYz11cw%3D%3D"
    },
    "errors": [],
    "warnings": [],
    "hasError": false,
    "hasWarning": false
}

```


## 2 Salary range

### 2.1 Get job titles

Find job titles from your query to use in `/v1/salary/range`.

**URL:** `/v1/salary/autocomplete`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| query | string | - | **Required**<br>Search query for valid job titles. | true | programming |
| countryCode | string | - | **Required**<br>Parameter to get the titles for the required county.<br>**Allowed format**<br>^[A-Za-z]{2}$ | true | de |


#### Request example

```
/v1/salary/range?query=programming&countryCode=de
```

#### Example response

```json
{
  "data": {
    "jobTitles": [
      { "count": 31, "jobTitle": "software engineer" },
      { "count": 19, "jobTitle": "full stack developer" },
      { "count": 15, "jobTitle": "machine learning engineer" },
      { "count": 14, "jobTitle": "senior software engineer" },
      { "count": 13, "jobTitle": "data scientist" },
      { "count": 9, "jobTitle": "data engineer" },
      { "count": 9, "jobTitle": "r&d engineer" },
      { "count": 8, "jobTitle": "back end developer" },
      { "count": 8, "jobTitle": "senior engineer" },
      { "count": 7, "jobTitle": "ai developer" },
      { "count": 6, "jobTitle": "automation engineer" },
      { "count": 5, "jobTitle": "application developer" },
      { "count": 5, "jobTitle": "computer vision engineer" },
      { "count": 5, "jobTitle": "model" },
      { "count": 5, "jobTitle": "physicist" },
      { "count": 5, "jobTitle": "quantitative analyst" },
      { "count": 5, "jobTitle": "research engineer" },
      { "count": 5, "jobTitle": "research intern" },
      { "count": 5, "jobTitle": "senior java developer" },
      { "count": 5, "jobTitle": "student researcher" },
      { "count": 4, "jobTitle": "devops engineer" },
      { "count": 4, "jobTitle": "electronics engineer" },
      { "count": 4, "jobTitle": "engineer" },
      { "count": 4, "jobTitle": "infrastructure engineer" },
      { "count": 4, "jobTitle": "senior research engineer" }
    ]
  },
  "meta": { "count": 25 },
  "_links": { "self": "/v2/salary/titles?query=programming&countryCode=ch" },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}

```


### 2.2 Get job salaries

Get salary ranges for jobs, use `/v1/salary/autocomplete` to get a list of valid job titles.

**URL:** `/v1/salary/range`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| query | string | - | **Required**<br>Job title, valid titles can be found with the `job title search` endpoint. | true | developer |
| countryCode | string | - | **Required**<br>Parameter to get the titles for the required county.<br>**Allowed format**<br>^[A-Za-z]{2}$ | true | de |


#### Request example

```
/v1/salary/range?query=developer&countryCode=de
```

#### Example response

```json
{
  "data": {
    "country": "Switzerland",
    "countryCode": "CH",
    "currency": "CHF",
    "dailySalary": {
      "max": 1006.060859127188,
      "mean": 849.55082984955,
      "median": 841.320182765177,
      "min": 703.555499159465
    },
    "hourlySalary": {
      "max": 81.7029013044972,
      "mean": 68.9926130955627,
      "median": 68.3241965278114,
      "min": 57.1362308637385
    },
    "lastUpdatedTimestamp": 1761956344,
    "monthlySalary": {
      "max": 9668.88383959108,
      "mean": 8164.72305340431,
      "median": 8085.62130736033,
      "min": 6761.61519888569
    },
    "weeklySalary": {
      "max": 2498.644050376289,
      "mean": 2109.937094995819,
      "median": 2089.495531067015,
      "min": 1747.344354107386
    },
    "yearlySalary": {
      "max": 136562.9666689806,
      "mean": 115318.253968254,
      "median": 114201.0237597132,
      "min": 95500.8092302153
    }
  },
  "_links": {
    "self": "/v2/salary/range?query=full%20stack%20developer&countryCode=ch"
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}

```




## 3 Errors and warnings

There are two types of possible issues, either you have an error, then nothing will be returned, except the error, or
you have warnings then the result will be returned, but also some warnings will be set.

The fields **hasError** and **hasWarning** in the response indicate whether the response contains errors or warnings:

- **hasError**: This field is `true` if the response contains any errors. If set to `false`, the response has no errors.
- **hasWarning**: This field is `true` if the response contains any warnings. If set to `false`, the response has no
  warnings.

### 3.1 Errors

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

### 3.2 Warnings

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