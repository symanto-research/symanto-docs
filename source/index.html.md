---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://developers.symanto.net/signup'>Sign Up for a Developer Key</a>
  # - <a href='https://developer.symanto.net/'>DeepLearning API Test</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Symanto API! You can use our API to access the API endpoints, which can get insight on text using our AI technology.

We have language binding in Shell. You can view code examples in the dark area to the right.

# Authentication

> To authorize, you need an api key. to create one visit this link:


> Make sure to replace `opensesame` with your API key.

Symanto API uses API keys to allow access to the API. You can register a new Symanto API key at our [developer portal](https://developers.symanto.net/signup).

Symanto API expects for the API key to be included in all API requests to the server in a header that looks like the following:

`x-api-key: opensesame`

<aside class="notice">
You must replace <code>opensesame</code> with your personal API key.
</aside>

# Text Analysis 

## Communication & Tonality


```shell
curl -X POST "https://api.symanto.net/communication" 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-d "[{\"id\":1,\"text\":\"I love the service\",\"language\":\"en\"}]"
```


> The above command returns JSON structured like this:

```json
[
  {
    "id": "string",
    "personalities": [
      {
        "prediction": "string",
        "probability": 0
      }
    ],
    "self": [
      {
        "prediction": "string",
        "probability": 0
      }
    ],
    "info": [
      {
        "prediction": "string",
        "probability": 0
      }
    ],
    "action": [
      {
        "prediction": "string",
        "probability": 0
      }
    ],
    "fact": [
      {
        "prediction": "string",
        "probability": 0
      }
    ]
  }
]
```

This endpoint retrieves all psychological aspects of the author. Supported Languages: ar, cn, de, en, es, fr, it, nl, pt, ru, tr

### HTTP Request

`POST http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
all | false | 

### REQUEST BODY SCHEMA : application/json

Parameter | Default | Description
--------- | ------- | -----------
id | - | id of the post
text | - | the text to analyse
language | - | language_code of the text

<aside class="success">
Remember — to successfully run this you need to authenticate using a valid api-key.
</aside>

## Emotion Analysis

```shell
curl -X POST "https://api.symanto.net/emotion" 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-d "[{\"id\":1,\"text\":\"I love the service\",\"language\":\"en\"}]"
```


> The above command returns JSON structured like this:

```json
[
  {
    "id": "string",
    "predictions": [
      {
        "prediction": "string",
        "probability": 0
      }
    ]
  }
]
```

This endpoint retrieves emotions from the written text. Supported language codes are:en,de,es
Retrieved emotions can be any of:
. anger
. joy
. love
. sadness
. unrecognized

### HTTP Request

`POST https://api.symanto.net/emotion`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
all | false | 

### REQUEST BODY SCHEMA : application/json

Parameter | Default | Description
--------- | ------- | -----------
id | - | id of the post
text | - | the text to analyse
language | - | language_code of the text


