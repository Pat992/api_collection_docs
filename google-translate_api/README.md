# Google Translate API

Translation API, powered by Google Translate. With the API, you have the flexibility to choose between a comprehensive response, including alternate writing styles and alternative translations, or a simple and streamlined output for quick and efficient language conversion.

## Table of contents
- 1 Translate
	- 1.1 Full translation
	- 1.2 Minified translation
- 2 Errors and warnings
	- 2.1 Errors
	- 2.2 Warnings


## 1 Translate

### 1.1 Full translation

Get a full translation with additional information, including alternative writing styles, synonyms, definitions and more.

**URL:** `/v2/translate/full`

#### Request body

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| input | string | - | **Required**<br>The input text (words, or sentences) you want to translate. | true | Hello |
| inputLanguage | string | - | **Optional**<br>The language-code of the input, if not set, the API will get the language automatically.<br>**Allowed format**<br>^[A-Za-z]{2}$ | false | en |
| outputLanguage | string | - | **Required**<br>The language-code you want to translate to.<br>**Allowed format**<br>^[A-Za-z]{2}$ | true | de |


#### Request example

```json
{
    "input": "hello",
    "inputLanguage": "en",
    "outputLanguage": "fr"
}
```

#### Example response

```json
{
  "data": {
    "input": "hallo",
    "inputAlternatives": [],
    "inputDefinition": "",
    "inputLanguage": "en",
    "inputSynonyms": [],
    "output": "Hola",
    "outputAlternatives": [],
    "outputLanguage": "es",
    "outputSynonyms": []
  },
  "_links": {
    "self": "/v2/translate/full"
  },
  "errors": [],
  "warnings": [],
  "hasError": false,
  "hasWarning": false
}

```


### 1.2 Minified translation

Get a simple and straightforward 1 to 1 translation of the input.

**URL:** `/v2/translate/mini`

#### Request body

| key | type | allowedValues | description | isRequired | example |
| --- | ---| --- | --- | --- | --- |
| input | string | - | **Required**<br>The input text (words, or sentences) you want to translate. | true | Hello |
| inputLanguage | string | - | **Optional**<br>The language-code of the input, if not set, the API will get the language automatically.<br>**Allowed format**<br>^[A-Za-z]{2}$ | false | en |
| outputLanguage | string | - | **Required**<br>The language-code you want to translate to.<br>**Allowed format**<br>^[A-Za-z]{2}$ | true | de |


#### Request example

```json
{
    "input": "hello",
    "inputLanguage": "en",
    "outputLanguage": "fr"
}
```

#### Example response

```json
{
  "data": {
    "input": "good day",
    "output": "Guter Tag"
  },
  "_links": {
    "self": "/v2/translate/mini"
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