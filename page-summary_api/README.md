# Page Summary API

Extracts website metadata and/or page body from a given URL, useful for SEO analysis, web scraping, and content summarization.

## Table of contents
- 1 summary
	- 1.1 Website to JSON
- 2 Errors and warnings
	- 2.1 Errors
	- 2.2 Warnings


## 1 summary

### 1.1 Website to JSON

Get website metadata and page content as a JSON.

**URL:** `/v1/json`

#### Request body

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| url | string | - | **Required**<br>URL of the website you want information from.<br>**Allowed format**<br>https?:\/\/(www\.)?[-a-zA-Z0-9@:%._\+~#=]{1,256}\.[a-zA-Z]{2,63}\b([-a-zA-Z0-9()@:%_\+.~#?&\/=]*)? | true | https://www.rapidapi.com |
| getMetadata | boolean | true or false | **Optional**<br>Get the website metadata from the head, is set to true by default.<br>**Allowed values**<br>true or false separated by a semicolon (;) | false | true |
| getBody | boolean | true or false | **Optional**<br>Get the website body, is set to true by default.<br>**Allowed values**<br>true or false separated by a semicolon (;) | false | true |
| additionalHeaders | object | - | **Optional**<br>Set additional headers, this will add or overwrite headers in the backend. | false | {"Cookies": "cookie1;cookie2",
"CustomHeader": "CustomValue"} |


#### Request example

```json
{
    "url": "https://bbc.com/",
    "getMetadata": true,
    "getBody": true,
    "additionalHeaders": {
        "Cookies": "Cookie1;Cookie2",
        "MyHeader": "MyHeaderValue"
    }
}
```

#### Example response

```json
{
  "data": {
    "body": {
      "a": [
        {
          "href": "https://www.bbc.com/weather",
          "text": "Weather"
        },
        {
          "href": "https://www.bbc.com/newsletters",
          "text": "Newsletters"
        },
        {
          "href": "https://www.bbc.com/news/live/c5yqygxe41pt",
          "text": "LIVEMaduro in custody at New York detention centre as Trump says US will 'run' Venezuela"
        },
        {
          "href": "/news/articles/czx1rpxzyx9o",
          "text": "'Deeply shocked': World leaders react to US attack on Venezuela"
        }
      ],
      "h1": [
        "Make me perfect: Manufacturing beauty in China",
        "Is social media dead?",
        "Business Daily meets: Jimmy Choo",
        "Making Jaws"
      ],
      "h2": [
        "Maduro in custody at New York detention centre as Trump says US will 'run' Venezuela",
        "Who's in charge of Venezuela and what happens next?",
        "'A long road ahead': Venezuelans react to Maduro's arrest with hope and worry",
        "BBC Mundo reports from a quiet Venezuela-Colombia border after Maduro's arrest"
      ],
      "h3": ["The BBC is in multiple languages"],
      "h4": [
        "'Deeply shocked': World leaders react to US attack on Venezuela",
        "Spies, drones and blowtorches: How the US captured Maduro",
        "Analysis: Venezuela could now define Trump's legacy - and America's place in the world",
        "Read the BBC In your own language"
      ],
      "h5": [],
      "h6": [],
      "img": [
        {
          "alt": "Venezuela's President Nicolas Maduro at the offices of the U.S. Drug Enforcement Administration (DEA) in New York",
          "src": "https://ichef.bbci.co.uk/ace/standard/480/cpsprodpb/8de6/live/93bb51e0-e939-11f0-8af9-1d7a0fb391df.jpg.webp",
          "text": ""
        },
        {
          "alt": "Trump at Mar-a-Lago press conference in a suit with blue tie",
          "src": "https://ichef.bbci.co.uk/news/480/cpsprodpb/68de/live/f8510680-e93a-11f0-aae2-2191c0e48a3b.jpg.webp",
          "text": ""
        }
      ],
      "ol": [],
      "p": [
        "Donald Trump says the US will \"run\" Venezuela until a \"safe\"...",
        "Caracas residents worry about what comes after US intervention...",
        "A once-busy commercial district at the Venezuela-Colombia border...",
        "RAF Typhoon jets joined French aircraft in a strike on an..."
      ],
      "table": [],
      "ul": [
        {
          "items": ["Home", "News", "Sport", "Business"]
        },
        {
          "items": ["Home", "News", "Sport", "Business"]
        },
        {
          "items": [
            "Terms of Use",
            "Subscription Terms",
            "About the BBC",
            "Privacy Policy"
          ]
        }
      ]
    },
    "metadata": {
      "author": "",
      "canonicalUrl": "https://www.bbc.com",
      "charset": "utf-8",
      "description": "Visit BBC for trusted reporting on the latest world and US news, sports, business, climate, innovation, culture and much more.",
      "faviconUrls": [
        "https://static.files.bbci.co.uk/bbcdotcom/web/20251210-151139-37baf2dfdd-web-2.36.1-1/favicon-32x32.png",
        "https://static.files.bbci.co.uk/bbcdotcom/web/20251210-151139-37baf2dfdd-web-2.36.1-1/favicon-16x16.png"
      ],
      "keywords": "",
      "language": "en-GB",
      "ogDescription": "Visit BBC for trusted reporting on the latest world and US news, sports, business, climate, innovation, culture and much more.",
      "ogImage": "",
      "ogLocale": "",
      "ogTitle": "BBC Home - Breaking News, World News, US News, Sports, Business, Innovation, Climate, Culture, Travel, Video & Audio",
      "ogUrl": "",
      "title": "BBC Home - Breaking News, World News, US News, Sports, Business, Innovation, Climate, Culture, Travel, Video & Audio",
      "viewport": "width=device-width"
    }
  },
  "meta": {
    "responseCode": 200
  },
  "_links": {
    "self": "/v1/json"
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}

```




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