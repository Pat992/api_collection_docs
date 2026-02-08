# LinkedIn API

Search LinkedIn for jobs, companies and more, easily extract structured data from public LinkedIn pages, no login, cookies, or session management required. This API is ideal for developers, recruiters, data analysts, and job platforms looking to integrate real-time LinkedIn data.

## Table of contents
- 1 Jobs
	- 1.1 Search and list jobs
	- 1.2 Get job details
	- 1.3 Search and list organization IDs
- 2 Company
	- 2.1 Search and list companies
	- 2.2 Get company details
	- 2.3 Get company feed
- 3 Errors and warnings
	- 3.1 Errors
	- 3.2 Warnings


## 1 Jobs

### 1.1 Search and list jobs

Get a list of jobs, use the `/v1/jobs/get` for full details on a specific job.

**URL:** `/v1/jobs/search`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| query | string | - | **Optional**<br>Keywords, job-title, company-name, position or any other relevant search-query. | false | java |
| organizationIds | string | - | **Optional**<br>ID of organizations like companies and schools the job-postings should be from, use the `Search and list organization IDs` endpoint for valid IDs. Will return everything by default.<br>**Allowed format**<br>^\d+(;\d+)*;?$ | false | 1441 |
| location | string | - | **Optional**<br>Location of the job offer, like country or city. Will be `Worldwide` if empty. | false | Worldwide |
| datePosted | string | month, week or day | **Optional**<br>The maximum age of when a result was added to LinkedIn, will return everything by default.<br>**Allowed values**<br>month, week or day | false | month |
| employmentTypes | string | contractor, fulltime, parttime, intern or temporary | **Optional**<br>Filter by job-types, like fulltime, contractor, etc. Multiple values are possible and need to be separated by semicolon (;). Will return everything by default.<br>**Allowed values**<br>contractor, fulltime, parttime, intern or temporary separated by a semicolon (;) | false | contractor;fulltime;parttime;intern;temporary |
| experienceLevels | string | intern, entry, associate, midSenior or director | **Optional**<br>Filter by experience-levels, like intern, director, etc. Multiple values are possible and need to be separated by semicolon (;). Will return everything by default.<br>**Allowed values**<br>intern, entry, associate, midSenior or director separated by a semicolon (;) | false | intern;entry;associate;midSenior;director |
| workplaceTypes | string | remote, hybrid or onSite | **Optional**<br>Filter by workplace-types, like remote, hybrid, etc. Multiple values are possible and need to be separated by semicolon (;). Will return everything by default.<br>**Allowed values**<br>remote, hybrid or onSite separated by a semicolon (;) | false | remote;hybrid;onSite |
| token | string | - | **Optional**<br>Pagination token from previous response as the `meta.nextToken` to get the next batch of results. | false |  |


#### Request example

```
/v1/jobs/search?query=web&location=Switzerland&datePosted=month&jobTypes=contractor;fulltime;parttime;intern;temporary&experienceLevels=intern;entry;associate;midSenior;director&workplaceTypes=remote;hybrid;onSite
```

#### Example response

```json
{
  "data": [
    {
      "companyName": "Netflix",
      "datePosted": "2025-12-18",
      "id": "4344905017",
      "linkedinCompanyName": "netflix",
      "linkedinUrl": "https://www.linkedin.com/jobs/view/hr-coordinator-netflix-animation-studios-at-netflix-4344905017",
      "location": "Burbank, CA",
      "postedTimeAgo": "2 weeks ago",
      "title": "HR Coordinator - Netflix Animation Studios"
    },
    {
      "companyName": "Prospect Equities®",
      "datePosted": "2025-12-10",
      "id": "4342895176",
      "linkedinCompanyName": "prospect-equities-",
      "linkedinUrl": "https://www.linkedin.com/jobs/view/front-end-developer-intern-at-prospect-equities%C2%AE-4342895176",
      "location": "Chicago, IL",
      "postedTimeAgo": "3 weeks ago",
      "title": "Front-End Developer Intern"
    },
    {
      "companyName": "LinkedIn",
      "datePosted": "2025-12-17",
      "id": "4344456572",
      "linkedinCompanyName": "linkedin",
      "linkedinUrl": "https://www.linkedin.com/jobs/view/software-engineer-frontend-at-linkedin-4344456572",
      "location": "Mountain View, CA",
      "postedTimeAgo": "2 weeks ago",
      "title": "Software Engineer - Frontend"
    },
    {
      "companyName": "Notion",
      "datePosted": "2025-12-19",
      "id": "4334367155",
      "linkedinCompanyName": "notionhq",
      "linkedinUrl": "https://www.linkedin.com/jobs/view/software-engineer-fullstack-early-career-at-notion-4334367155",
      "location": "New York, NY",
      "postedTimeAgo": "2 weeks ago",
      "title": "Software Engineer, Fullstack, Early Career"
    },
    {
      "companyName": "Notion",
      "datePosted": "2025-12-19",
      "id": "4334158613",
      "linkedinCompanyName": "notionhq",
      "linkedinUrl": "https://www.linkedin.com/jobs/view/software-engineer-fullstack-early-career-at-notion-4334158613",
      "location": "San Francisco, CA",
      "postedTimeAgo": "2 weeks ago",
      "title": "Software Engineer, Fullstack, Early Career"
    },
    {
      "companyName": "Bounteous",
      "datePosted": "2026-01-01",
      "id": "4329962289",
      "linkedinCompanyName": "bounteous",
      "linkedinUrl": "https://www.linkedin.com/jobs/view/front-end-developer-jr-mid-react-at-bounteous-4329962289",
      "location": "United States",
      "postedTimeAgo": "2 days ago",
      "title": "Front End Developer (Jr-Mid React)"
    },
    {
      "companyName": "Resonance",
      "datePosted": "2026-01-01",
      "id": "4350920574",
      "linkedinCompanyName": "ssg-advisors",
      "linkedinUrl": "https://www.linkedin.com/jobs/view/front-end-engineer-at-resonance-4350920574",
      "location": "New York County, NY",
      "postedTimeAgo": "3 days ago",
      "title": "Front End Engineer"
    },
    {
      "companyName": "D3",
      "datePosted": "2025-11-16",
      "id": "4343087718",
      "linkedinCompanyName": "d3inc",
      "linkedinUrl": "https://www.linkedin.com/jobs/view/frontend-engineer-new-grad-at-d3-4343087718",
      "location": "Los Angeles, CA",
      "postedTimeAgo": "1 month ago",
      "title": "Frontend Engineer - New Grad"
    },
    {
      "companyName": "Saransh Inc",
      "datePosted": "2025-12-08",
      "id": "4342765629",
      "linkedinCompanyName": "saransh-inc-usa",
      "linkedinUrl": "https://www.linkedin.com/jobs/view/ui-react-developer-at-saransh-inc-4342765629",
      "location": "Jersey City, NJ",
      "postedTimeAgo": "3 weeks ago",
      "title": "UI React Developer"
    },
    {
      "companyName": "Signals",
      "datePosted": "2025-12-27",
      "id": "4346531130",
      "linkedinCompanyName": "signalsai",
      "linkedinUrl": "https://www.linkedin.com/jobs/view/junior-web-developer-at-signals-4346531130",
      "location": "Provo, UT",
      "postedTimeAgo": "1 week ago",
      "title": "Junior Web Developer"
    }
  ],
  "meta": {
    "position": 0,
    "count": 10,
    "nextToken": "dD0xMDtxPXJlYW..."
  },
  "_links": {
    "self": "/v1/jobs/search?query=react",
    "next": "/v1/jobs/search?token=dD0xMDtxPXJlYW..."
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

Get job details by its ID, use the `/v1/jobs/search` endpoint to search for jobs.

**URL:** `/v1/jobs/get`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| id | string | - | **Required**<br>ID of the job, to get allowed values, use the `search` endpoint.<br>**Allowed format**<br>^\d+$ | true |  |


#### Request example

```
/v1/jobs/get?id=4175032607
```

#### Example response

```json
{
  "data": {
    "acceptingApplications": true,
    "applicants": 200,
    "companyName": "Netflix",
    "description": "Netflix Animation Studios is on a mission...",
    "employmentType": "Full-time",
    "id": "4344905017",
    "industries": "Entertainment Providers",
    "jobFunction": "Other",
    "linkedinCompanyName": "netflix",
    "linkedinUrl": "https://www.linkedin.com/jobs/view/hr-coordinator-netflix-animation-studios-at-netflix-4344905017",
    "location": "Burbank, CA",
    "postedTimeAgo": "2 weeks ago",
    "seniorityLevel": "Not Applicable",
    "title": "HR Coordinator - Netflix Animation Studios"
  },
  "_links": { "self": "/v1/jobs/get?id=4344905017" },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}

```


### 1.3 Search and list organization IDs

Get a list of organization IDs, use the IDs in the organizationIds in `/v1/jobs/search` to filter by companies or schools.

**URL:** `/v1/jobs/organizations`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| query | string | - | **Required**<br>Organization name or query, can be companies or schools, etc. | true | google |


#### Request example

```
/v1/jobs/organizations?query=google
```

#### Example response

```json
{
  "data": [
    { "displayName": "Google", "id": 1441 },
    { "displayName": "Google DeepMind", "id": 1594050 },
    { "displayName": "Google Operations Center", "id": 14547137 },
    { "displayName": "Google Fiber", "id": 2171947 },
    { "displayName": "Google for Startups", "id": 18336369 },
    { "displayName": "Google Developers Group", "id": 11162656 },
    { "displayName": "Mandiant (part of Google Cloud)", "id": 28103 },
    { "displayName": "Google Cloud Security", "id": 18451491 },
    { "displayName": "Google Summer of Code", "id": 19184331 },
    { "displayName": "Google Cloud Skills Boost", "id": 98808973 }
  ],
  "meta": { "count": 10 },
  "_links": { "self": "/v1/jobs/organizations?query=google" },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}

```


## 2 Company

### 2.1 Search and list companies

Get company LinkedIn names and short descriptions, use the `/v1/companies/get` endpoint with the linkedinName to get the full details.

**URL:** `/v1/companies/search`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| query | string | - | **Required if token is not set**<br>Name of the organization to find. | true | google |
| siteCountryCode | string | - | **Optional**<br>Companies can create sites for specific countries, use this parameter if you want a page made for a specific country, or leave it to get the default result.<br>**Allowed format**<br>^[A-Za-z]{2}$ | false | de |
| token | string | - | **Optional**<br>Pagination token from previous response as `meta.nextToken`. | false |  |


#### Request example

```
/v1/companies/search?query=Google&siteCountryCode=de
```

#### Example response

```json
{
  "data": [
    {
      "companyName": "Google - LinkedIn",
      "linkedinName": "google",
      "shortDescription": "7 Jul 1999...",
      "siteCountryCode": ""
    },
    {
      "companyName": "Google for Startups - LinkedIn",
      "linkedinName": "google-for-startups",
      "shortDescription": "Google for Startups...",
      "siteCountryCode": ""
    },
    {
      "companyName": "Google Labs | LinkedIn",
      "linkedinName": "googlelabs",
      "shortDescription": "Google Labs...",
      "siteCountryCode": ""
    },
    {
      "companyName": "Google Operations Center | LinkedIn",
      "linkedinName": "googleoperationscenter",
      "shortDescription": "Google Operations Center...",
      "siteCountryCode": ""
    }
  ],
  "meta": {
    "position": 0,
    "count": 10,
    "nextToken": "dD11TE1haVlSZlJ5czAyM..."
  },
  "_links": { "self": "/v1/companies/search?query=google" },
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
    "next": "/v1/companies/search?token=dG9rZW49ODY5ODU..."
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}
```

#### token example request:

`/v1/companies/search?token=dG9rZW49ODY5ODU...`



### 2.2 Get company details

Get company details by its LinkedIn name, use the `/v1/companies/search` to get valid LinkedIn names.

**URL:** `/v1/companies/get`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| linkedinName | string | - | **Required**<br>LinkedIn name of the company, to get allowed values, use the `$path/search` endpoint. | true | google |
| siteCountryCode | string | - | **Optional**<br>Companies can create sites for specific countries, use this parameter if you want a page made for a specific country, or leave it to get the default result.<br>**Allowed format**<br>^[A-Za-z]{2}$ | false | de |


#### Request example

```
/v1/companies/get?linkedinName=google&siteCountryCode=de
```

#### Example response

```json
{
  "data": {
    "about": "A problem isn't truly solved until it's solved for all...",
    "employees": "10,001+",
    "followers": 40146259,
    "funding": {
      "lastRoundDate": "1999-07-07",
      "lastRoundFunding": "US$ 25.0M",
      "rounds": "3 total rounds"
    },
    "headquarters": "Mountain View, CA",
    "id": 1441,
    "industry": "Software Development",
    "linkedinCompanyName": "Google",
    "linkedinUrl": "https://www.linkedin.com/company/google",
    "locations": [
      {
        "address": "1600 Amphitheatre Parkway Mountain View, CA 94043, US",
        "bingDirections": "https://www.bing.com/maps?where=1600+Amphitheatre+Parkway+Mountain+View+94043+CA+US&trk=org-locations_url",
        "isPrimary": true
      },
      {
        "address": "111 8th Ave New York, NY 10011, US",
        "bingDirections": "https://www.bing.com/maps?where=111+8th+Ave+New+York+10011+NY+US&trk=org-locations_url",
        "isPrimary": false
      },
      {
        "address": "Claude Debussylaan 34 Amsterdam, North Holland 1082 MD, NL",
        "bingDirections": "https://www.bing.com/maps?where=Claude+Debussylaan+34+Amsterdam+1082+MD+North+Holland+NL&trk=org-locations_url",
        "isPrimary": false
      },
      {
        "address": "Avenida Brigadeiro Faria Lima, 3477 Sao Paulo, SP 04538-133, BR",
        "bingDirections": "https://www.bing.com/maps?where=Avenida+Brigadeiro+Faria+Lima%2C+3477+Sao+Paulo+04538-133+SP+BR&trk=org-locations_url",
        "isPrimary": false
      }
    ],
    "organizationType": "Public Company",
    "specialities": [
      "search",
      "ads",
      "mobile",
      "android",
      "online video",
      "apps",
      "machine learning",
      "virtual reality",
      "cloud",
      "hardware",
      "artificial intelligence",
      "youtube",
      "software"
    ],
    "stock": {
      "delay": "",
      "growth": "",
      "high": 0.0,
      "last_update": "",
      "low": 0.0,
      "market": "",
      "name": "",
      "open": 0.0,
      "price": ""
    },
    "website": "https://goo.gle/3DLEokh"
  },
  "meta": {
    "feedToken": "dD0xNDQxOjAtMTc2NzUxNjUwNTY3Ny1lN2JmNjIwMDJkM2Q4OGRjNzg4ZmMyYzJiYzg1YWVlMTtwPTA="
  },
  "_links": { "self": "/v1/companies/get?linkedinName=google" },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}

```


### 2.3 Get company feed

Get the company feed and posts, including text, videos and images.

**URL:** `/v1/companies/feed`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| token | string | - | **Required**<br>Get the token from the `/v1/companies/get` endpoint or from the `meta.nextToken`. Important: This token will expire after some time. | true |  |


#### Request example

```
/v1/companies/feed?token=MTEyNDYwODI1Mi5SZXRybw==
```

#### Example response

```json
{
  "data": [
    {
      "comments": 83,
      "content": "Martina thought she was taking a short break before...",
      "images": [],
      "postedAgo": "1d",
      "reactions": 0,
      "videos": [
        {
          "bitrate": 699541,
          "type": "video/mp4",
          "videoUrl": "https://dms.licdn.com/playlist/vid/v2/D4E0..."
        },
        {
          "bitrate": 914001,
          "type": "video/mp4",
          "videoUrl": "https://dms.licdn.com/playlist/vid/v2/D4E0..."
        }
      ]
    },
    {
      "comments": 116,
      "content": "Winter mode: activated...",
      "images": [
        "https://media.licdn.com/dms/image/v2/D5610AQF...",
        "https://media.licdn.com/dms/image/v2/D5610AQG...",
        "https://media.licdn.com/dms/image/v2/D5610AQH...",
        "https://media.licdn.com/dms/image/v2/D5610AQE..."
      ],
      "postedAgo": "1w",
      "reactions": 0,
      "videos": []
    },
    {
      "comments": 86,
      "content": "This week, we expanded the Gemini 3 model...",
      "images": [],
      "postedAgo": "2w",
      "reactions": 0,
      "videos": []
    }
  ],
  "meta": {
    "companyName": "Google",
    "linkedinCompanyName": "google",
    "position": 0,
    "count": 10,
    "nextToken": "dD0xNDQxOjAtMTc2..."
  },
  "_links": {
    "self": "/v1/companies/feed?token=dD0xNDQxOjAtMTc2...",
    "next": "/v1/companies/feed?token=dD0xNDQxOjAtMTc2..."
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
    "next": "/v1/companies/feed?token=dG9rZW49ODY5ODU..."
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}
```

#### token example request:

`/v1/companies/feed?token=dG9rZW49ODY5ODU...`





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