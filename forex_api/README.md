# Forex API

This Forex API delivers live currency rates, economic news, and both market sentiment indicators and real trader sentiment. Make smarter forex decisions and build powerful applications.

## Table of contents
- 1 Sentiment
	- 1.1 Trader Sentiment
	- 1.2 Technical Sentiment
- 2 Economic Calendar
	- 2.1 Economic Calendar Options
	- 2.2 Economic Calendar
- 3 Errors and warnings
	- 3.1 Errors
	- 3.2 Warnings


## 1 Sentiment

### 1.1 Trader Sentiment

Understand how real forex traders are feeling about the market through current trades.

**URL:** `/v2/sentiment/trader`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |


#### Request example

```
/v2/sentiment/trader?symbols=eurusd;USDJPY
```

#### Example response

```json
{
  "data": [
    {
      "longTrades": {
        "percentage": 28,
        "positions": 16386,
        "volumeLots": 4324.15
      },
      "shortTrades": {
        "percentage": 72,
        "positions": 34980,
        "volumeLots": 10973.49
      },
      "symbol": "EURUSD",
      "totalTrades": {
        "positions": 51366,
        "volumeLots": 15297.64
      }
    },
    {
      "longTrades": {
        "percentage": 39,
        "positions": 16168,
        "volumeLots": 5050.13
      },
      "shortTrades": {
        "percentage": 61,
        "positions": 31093,
        "volumeLots": 8051.35
      },
      "symbol": "GBPUSD",
      "totalTrades": {
        "positions": 47261,
        "volumeLots": 13101.48
      }
    },
    {
      "longTrades": {
        "percentage": 34,
        "positions": 4161,
        "volumeLots": 777.37
      },
      "shortTrades": {
        "percentage": 66,
        "positions": 3999,
        "volumeLots": 1478.04
      },
      "symbol": "USDJPY",
      "totalTrades": {
        "positions": 8160,
        "volumeLots": 2255.41
      }
    },
    {
      "longTrades": {
        "percentage": 20,
        "positions": 1477,
        "volumeLots": 217.3
      },
      "shortTrades": {
        "percentage": 80,
        "positions": 4727,
        "volumeLots": 889.17
      },
      "symbol": "GBPJPY",
      "totalTrades": {
        "positions": 6204,
        "volumeLots": 1106.47
      }
    }
  ],
  "_links": {
    "self": "/api/forex/v2/sentiment/trader?warning=true"
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": true
}

```


### 1.2 Technical Sentiment

Gain insights into market sentiment through established metrics from widely used indicators.

**URL:** `/v2/sentiment/technical`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |


#### Request example

```
/v2/sentiment/technical
```

#### Example response

```json
{
  "data": [
    {
      "lastTradePrice": 0.9249,
      "symbol": "AUDCAD",
      "todaysOpinion": "Buy",
      "todaysOpinionPercentage": 100
    },
    {
      "lastTradePrice": 0.5326,
      "symbol": "AUDCHF",
      "todaysOpinion": "Buy",
      "todaysOpinionPercentage": 88
    },
    {
      "lastTradePrice": 0.57372,
      "symbol": "AUDEUR",
      "todaysOpinion": "Buy",
      "todaysOpinionPercentage": 100
    },
    {
      "lastTradePrice": 0.49608,
      "symbol": "AUDGBP",
      "todaysOpinion": "Buy",
      "todaysOpinionPercentage": 80
    }
  ],
  "_links": {
    "self": "/api/forex/v2/sentiment/technical"
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}

```


## 2 Economic Calendar

### 2.1 Economic Calendar Options

Get all supported countries and volatilities for the `/v2/calendar/get` endpoint.

**URL:** `/v2/calendar/options`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |


#### Request example

```
/v2/calendar/options
```

#### Example response

```json
{
  "data": {
    "allowedCountries": ["us", "uk", "emu"],
    "allowedVolatilities": ["none", "low", "medium", "high"],
    "details": "`allowedCountries` and `allowedVolatilities` both are case insensitiv..."
  },
  "_links": {
    "self": "/api/forex/v2/calendar/options"
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}

```


### 2.2 Economic Calendar

Get upcoming news and economic events.

**URL:** `/v2/calendar/get`

#### Request parameters

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| includeCountries | string | us, uk, emu, de, cn, jp, ca, au, nz, ch, fr, it, es, ua, in, ru, tr, za, br, kr, id, sg, mx, se, no, dk, gr, pt, ie, at, be, nl, fi, cz, pl, hu, ro, cl, co, ar, is, hk, sk, il, sa, vn, kw, eg, ae, qa or th | **Optional**<br>Filter results by only returning news specific countries, multiple countries are possible, separated by a semicolon (;), if empty, the API will return news for all supported countries.<br>**Allowed values**<br>us, uk, emu, de, cn, jp, ca, au, nz, ch, fr, it, es, ua, in, ru, tr, za, br, kr, id, sg, mx, se, no, dk, gr, pt, ie, at, be, nl, fi, cz, pl, hu, ro, cl, co, ar, is, hk, sk, il, sa, vn, kw, eg, ae, qa or th separated by a semicolon (;) | false | us;ch;de |
| includeVolatilities | string | none, low, medium or high | **Optional**<br>Filter results by only returning news with specific impacts, multiple values are possible, separated by a semikolon (;), if empty, the API will return news for all volatilities.<br>**Allowed values**<br>none, low, medium or high separated by a semicolon (;) | false | none;low;medium;high |
| startDate | string | - | **Optional**<br>Date of the first calendar entry, if empty, it will be set to one week ago.<br>**Allowed format**<br>^\d{4}-(0[1-9]\|1[0-2])-(0[1-9]\|[12]\d\|3[01])$ | false | 2026-01-01 |
| endDate | string | - | **Optional**<br>Date of the last calendar entry, if empty, it will be set to today.<br>**Allowed format**<br>^\d{4}-(0[1-9]\|1[0-2])-(0[1-9]\|[12]\d\|3[01])$ | false | 2026-01-12 |


#### Request example

```
/v2/calendar/get?includeVolatilities=LOW;MEDIUM;HIGH&includeCountries=CH;US&endDate=2025-09-29&startDate=2025-09-29
```

#### Example response

```json
{
  "data": [
    {
      "actual": 50.1,
      "consensus": 49.2,
      "countryCode": "CN",
      "currencyCode": "CNY",
      "dateUtc": "2025-12-31T01:30:00Z",
      "id": "a16fc136-f85a-422b-9233-9e025ad1d68d",
      "name": "NBS Manufacturing PMI",
      "previous": 49.2,
      "revised": 0.0,
      "unit": "HIGH",
      "volatility": "HIGH"
    },
    {
      "actual": 50.2,
      "consensus": 49.8,
      "countryCode": "CN",
      "currencyCode": "CNY",
      "dateUtc": "2025-12-31T01:30:00Z",
      "id": "09a13d3b-0487-46b3-b770-20f7fa27c7e4",
      "name": "NBS Non-Manufacturing PMI",
      "previous": 49.5,
      "revised": 0.0,
      "unit": "HIGH",
      "volatility": "HIGH"
    },
    {
      "actual": 50.1,
      "consensus": 0.0,
      "countryCode": "CN",
      "currencyCode": "CNY",
      "dateUtc": "2025-12-31T01:45:00Z",
      "id": "280eb979-7f29-47af-94fc-6a53466b7cf9",
      "name": "RatingDog Manufacturing PMI",
      "previous": 49.9,
      "revised": 0.0,
      "unit": "HIGH",
      "volatility": "HIGH"
    },
    {
      "actual": 52.0,
      "consensus": 0.0,
      "countryCode": "CN",
      "currencyCode": "CNY",
      "dateUtc": "2026-01-05T01:45:00Z",
      "id": "9e6ffc7a-146e-4226-a5d1-67ac5d9da27d",
      "name": "RatingDog Services PMI",
      "previous": 52.1,
      "revised": 0.0,
      "unit": "HIGH",
      "volatility": "HIGH"
    }
  ],
  "_links": {
    "self": "/api/forex/v2/calendar/get?includeVolatilities=HIGH"
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