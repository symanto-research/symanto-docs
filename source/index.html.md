---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://developers.symanto.net/signup'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Symanto API! You can use our API to access the API endpoints, which can get insight on text using our AI technology.

We have language binding in Shell. You can view code examples in the dark area to the right.

# Authentication

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
-H "x-api-key: opensesame" 
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

`POST https://api.symanto.net/communication`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
all | false | returns all predictions, not only the most probable one

### REQUEST BODY SCHEMA : application/json

Parameter | Optionality | Description
--------- | ------- | -----------
id | Optional | id of the post
text | Required | the text to analyse
language | Required | language_code of the text

<aside class="success">
Remember — to successfully run this you need to authenticate using a valid api-key.
</aside>

## Emotion Analysis

```shell
curl -X POST "https://api.symanto.net/emotion" 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-H "x-api-key: opensesame" 
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
all | false | returns all predictions, not only the most probable one

### REQUEST BODY SCHEMA : application/json

Parameter | Optionality | Description
--------- | ------- | -----------
id | Optional | id of the post
text | Required | the text to analyse
language | Required | language_code of the text



## Personality Traits

```shell
curl -X POST "https://api.symanto.net/personality" 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-H "x-api-key: opensesame" 
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

Personality traits evaluates content and writing style to determine how the author makes decisions.
Our model identifies whether an author is Emotional (relationship-oriented, focusing on social values and empathy) or Rational (objective and pragmatic, focusing on facts and logical deduction).

Supported Languages: ar, cn, de, en, es, fr, it, nl, pt, ru, tr

Returned labels:
. yes
. no

### HTTP Request

`POST https://api.symanto.net/personality`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
all | false | returns all predictions, not only the most probable one

### REQUEST BODY SCHEMA : application/json

Parameter | Optionality | Description
--------- | ------- | -----------
id | Optional | id of the post
text | Required | the text to analyse
language | Required | language_code of the text

## Sentiment Analysis

```shell
curl -X POST "https://api.symanto.net/sentiment" 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-H "x-api-key: opensesame" 
-d "[{\"id\":1,\"text\":\"I love the service\",\"language\":\"en\"}]"
```

> The above command returns JSON structured like this:

```json
[
    {
        "id": "1",
        "predictions": [
            {
                "prediction": "positive",
                "probability": 0.9802348613739014
            }
        ]
    }
]

```
Understand whether your text has a positive or negative sentiment.
Supported Languages: en, de, es
Returned labels:
. positive
. negative
. unrecognized

### HTTP Request

`POST https://api.symanto.net/sentiment`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
all | false | returns all predictions, not only the most probable one

### REQUEST BODY SCHEMA : application/json

Parameter | Optionality | Description
--------- | ------- | -----------
id | Optional | id of the post
text | Required | the text to analyse
language | Required | language_code of the text

## Extract topics and sentiments and relate them

```shell
curl -X POST "https://api.symanto.net/topic-sentiment" 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-H "x-api-key: opensesame" 
-d "[{\"id\":1,\"text\":\"I love the service\",\"language\":\"en\"}]"
```

> The above command returns JSON structured like this:

```json
[
    {
        "id": "1",
        "text": "Hello I love the service",
        "language": "en",
        "topicSentiments": [
            {
                "topic": {
                    "start": 3,
                    "end": 5,
                    "topic": "Service",
                    "text": "the service",
                    "category": "Service General"
                },
                "sentiment": {
                    "start": 2,
                    "end": 3,
                    "text": "love",
                    "positive": true,
                    "scale": 1.0
                },
                "sentence": "love the service"
            }
        ],
        "sentiments": [
            {
                "start": 2,
                "end": 3,
                "text": "love",
                "positive": true,
                "scale": 1.0,
                "category": "",
                "parentCategory": ""
            }
        ],
        "topics": [
            {
                "start": 3,
                "end": 5,
                "topic": "Service",
                "text": "the service",
                "category": "Service General"
            }
        ]
    }
]
```
This endpoint extracts topics and sentiments from the text and tries to see if there is a meaningful relation between them. 

### HTTP Request

`POST https://api.symanto.net/topic-sentiment`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
domain | - | Enum: "Ecom" "Employee". Provide analysis domain for better extraction (optional)

### REQUEST BODY SCHEMA : application/json

Parameter | Optionality | Description
--------- | ------- | -----------
id | Optional | id of the post
text | Required | the text to analyse
language | Required | language_code of the text

## Language Detection


```shell
curl -X POST "https://api.symanto.net/language-detection" 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-H "x-api-key: opensesame" 
-d "[{\"id\":1,\"text\":\"I love the service\"}]"
```

> The above command returns JSON structured like this:

```json
[
    {
        "id": "1",
        "detected_language": "en"
    }
]
```
Identifies what language a text is written in. Only languages that our API supports can be analyzed.
Returned labels:
language_code of the detected language


### HTTP Request

`POST https://api.symanto.net/language-detection`

### REQUEST BODY SCHEMA : application/json

Parameter | Optionality | Description
--------- | ------- | -----------
id | Optional | id of the post
text | Required | the text to analyse
