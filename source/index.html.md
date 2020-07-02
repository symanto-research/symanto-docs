---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - java

toc_footers:
  - <a href='https://developers.symanto.net/signup'>Sign Up for a Developer Key</a>
  - <a href='https://api.symanto.net/docs'>Try it out in Swagger</a>
  - <a href='https://app.getpostman.com/run-collection/1a5af5975816c49e8e33'><img src="https://run.pstmn.io/button.svg"></img></a>

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

## Personality Traits

```shell
curl -X POST "https://api.symanto.net/personality" 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-H "x-api-key: opensesame" 
-d "[{\"id\":1,\"text\":\"I love the service\",\"language\":\"en\"}]"
```

```python
import requests

url = "https://api.symanto.net/personality"

payload = "[{ \"id\": \"1\", \"text\": \"I love the service\", \"language\": \"en\" }]"
headers = {
    "x-api-key": "opensesame",
    "Content-Type": "application/json"
}
response = requests.request("POST", url, headers=headers, data=payload)
```

```java
OkHttpClient client = new OkHttpClient().newBuilder().build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create("[ { \"id\": \"1\", \"text\": \"I love the service\", \"language\": \"en\" }]", mediaType);
Request request = new Request.Builder()
    .url("https://api.symanto.net/personality")
    .method("POST", body)
    .addHeader("x-api-key","opensesame")
    .build();
Response response = client.newCall(request).execute();
```

> The above command returns JSON structured like this:

```json
[
    {
        "id": "1",
        "predictions": [
            {
                "prediction": "emotional",
                "probability": 0.9997281432151794
            }
        ]
    }
]
```

Predicts the personality traits to understand how the author of the written text makes decisions, whether they are _Emotional_ (relationship-oriented, focusing on social values and empathy) or _Rational_ (objective and pragmatic, focusing on facts and logical deduction).

Supported Languages: [ `ar`, `de`, `en`, `es`, `fr`, `it`, `nl`, `pt`, `ru`, `tr`, `zh` ]

Returned labels: [`emotional`, `rational`]

### HTTP Request

`POST https://api.symanto.net/personality`

### Query Parameters

Parameter | Type    | Default | Description
--------- | ------- | ------- | -----------
all       | bool    | false   | returns all predictions, not only the most probable one


### REQUEST BODY SCHEMA : application/json

An array of max `32` items is allowed.

Parameter | Type        | Optionality | Description
--------- | ----------- | ----------- | -----------
id        | string      | Optional    | id of the post
text      | string      | Required    | the text to analyse
language  | string      | Required    | language_code of the text


## Communication Style


```shell
curl -X POST "https://api.symanto.net/communication" 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-H "x-api-key: opensesame" 
-d "[{\"id\":1,\"text\":\"I love the service\",\"language\":\"en\"}]"
```

```python
import requests

url = "https://api.symanto.net/communication"

payload = "[{ \"id\": \"1\", \"text\": \"I love the service\", \"language\": \"en\" }]"
headers = {
    "x-api-key": "opensesame",
    "Content-Type": "application/json"
}
response = requests.request("POST", url, headers=headers, data=payload)
```

```java
OkHttpClient client = new OkHttpClient().newBuilder().build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create("[ { \"id\": \"1\", \"text\": \"I love the service\", \"language\": \"en\" }]", mediaType);
Request request = new Request.Builder()
    .url("https://api.symanto.net/communication")
    .method("POST", body)
    .addHeader("x-api-key","opensesame")
    .build();
Response response = client.newCall(request).execute();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "1",
    "predictions": [
      {
        "prediction": "self-revealing",
        "probability": 0.9997937083244324
      }
    ]
  }
]
```

Detect the communication purpose and style of the text. The style includes: 
- _self-revealing_ (sharing one's one experience and opinion)
- _fact-oriented_ (focusing on factual information, objective observations or statements)
- _information-seeking_ (posing questions)
- _action-seeking_ (aiming to trigger someone's action by giving recommendation, requests or advice). 

Supported Languages: [ `ar`, `de`, `en`, `es`, `fr`, `it`, `nl`, `pt`, `ru`, `tr`, `zh` ]

Returned labels: [`action-seeking`, `fact-oriented`, `information-seeking`, `self-revealing`]

### HTTP Request

`POST https://api.symanto.net/communication`

### Query Parameters

Parameter | Type    | Default | Description
--------- | ------- | ------- | -----------
all       | bool    | false   | returns all predictions, not only the most probable one

### REQUEST BODY SCHEMA : application/json

An array of max `32` items is allowed.

Parameter | Type        | Optionality | Description
--------- | ----------- | ----------- | -----------
id        | string      | Optional    | id of the post
text      | string      | Required    | the text to analyse
language  | string      | Required    | language_code of the text

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

```python
import requests

url = "https://api.symanto.net/emotion"

payload = "[{ \"id\": \"1\", \"text\": \"I love the service\", \"language\": \"en\" }]"
headers = {
    "x-api-key": "opensesame",
    "Content-Type": "application/json"
}
response = requests.request("POST", url, headers=headers, data=payload)
```

```java
OkHttpClient client = new OkHttpClient().newBuilder().build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create("[ { \"id\": \"1\", \"text\": \"I love the service\", \"language\": \"en\" }]", mediaType);
Request request = new Request.Builder()
    .url("https://api.symanto.net/emotion")
    .method("POST", body)
    .addHeader("x-api-key","opensesame")
    .build();
Response response = client.newCall(request).execute();
```

> The above command returns JSON structured like this:

```json
[
    {
        "id": "1",
        "predictions": [
            {
                "prediction": "joy",
                "probability": 0.619248952716589
            }
        ]
    }
]
```

This endpoint retrieves emotions from the written text. 

Supported language codes are: [ `de`, `en`, `es` ]

Retrieved emotions can be any of: [`anger`, `joy`, `love`, `sadness`, `surprise`]


### HTTP Request

`POST https://api.symanto.net/emotion`

### Query Parameters

Parameter | Type    | Default | Description
--------- | ------- | ------- | -----------
all       | bool    | false   | returns all predictions, not only the most probable one

### REQUEST BODY SCHEMA : application/json

An array of max `512` items is allowed.

Parameter | Type        | Optionality | Description
--------- | ----------- | ----------- | -----------
id        | string      | Optional    | id of the post
text      | string      | Required    | the text to analyse
language  | string      | Required    | language_code of the text


## Sentiment Analysis

```shell
curl -X POST "https://api.symanto.net/sentiment" 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-H "x-api-key: opensesame" 
-d "[{\"id\":1,\"text\":\"I love the service\",\"language\":\"en\"}]"
```

```python
import requests

url = "https://api.symanto.net/sentiment"

payload = "[{ \"id\": \"1\", \"text\": \"I love the service\", \"language\": \"en\" }]"
headers = {
    "x-api-key": "opensesame",
    "Content-Type": "application/json"
}
response = requests.request("POST", url, headers=headers, data=payload)
```

```java
OkHttpClient client = new OkHttpClient().newBuilder().build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create("[{\"id\": \"1\", \"text\": \"I love the service\", \"language\": \"en\" }]", mediaType);
Request request = new Request.Builder()
    .url("https://api.symanto.net/sentiment")
    .method("POST", body)
    .addHeader("x-api-key","opensesame")
    .build();
Response response = client.newCall(request).execute();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "1",
    "predictions": [
      {
        "prediction": "positive",
        "probability": 0.8465812802314758
      }
    ]
  }
]
```
Understand whether your text has a positive or negative sentiment.

Supported Languages: [`en`, `de`, `es`]

Returned labels: [`positive`, `negative`, `unrecognized`]


### HTTP Request

`POST https://api.symanto.net/sentiment`

### Query Parameters

Parameter | Type    | Default | Description
--------- | ------- | ------- | -----------
all       | bool    | false   | returns all predictions, not only the most probable one

### REQUEST BODY SCHEMA : application/json

An array of max `32` items is allowed.

Parameter | Type        | Optionality | Description
--------- | ----------- | ----------- | -----------
id        | string      | Optional    | id of the post
text      | string      | Required    | the text to analyse
language  | string      | Required    | language_code of the text

## Topic Sentiment Extraction

```shell
curl -X POST "https://api.symanto.net/topic-sentiment" 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-H "x-api-key: opensesame" 
-d "[{\"id\":1,\"text\":\"Hello I love the service\",\"language\":\"en\"}]"
```

```python
import requests

url = "https://api.symanto.net/topic-sentiment"

payload = "[{ \"id\": \"1\", \"text\": \"Hello I love the service\", \"language\": \"en\" }]"
headers = {
    "x-api-key": "opensesame",
    "Content-Type": "application/json"
}
response = requests.request("POST", url, headers=headers, data=payload)
```

```java
OkHttpClient client = new OkHttpClient().newBuilder().build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create("[{ \"id\": \"1\", \"text\": \"Hello I love the service\",\"language\": \"en\"} ]", mediaType);
Request request = new Request.Builder()
    .url("https://api.symanto.net/topic-sentiment")
    .method("POST", "opensesame")
    .addHeader("x-api-key","opensesame")
    .build();
Response response = client.newCall(request).execute();
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
Detects topics, topic category of each topic, and then analyzes the sentiment towards each of the topics mentioned.

Supported Languages: [`en`, `de`]

### HTTP Request

`POST https://api.symanto.net/topic-sentiment`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
domain    | -       | Provide analysis domain for domain-specific extraction (optional)

### Available domains

Enum        | Description 
---------   | -----------
"Ecom"      | Use this domain to retrieve insights about experience, product and service. 
"Employee"  | Use this domain to retrieve insights about associates, communication, culture, development & resources, leadership & planning, overall perception, pay & benefits, role, treatment and work environment.

### REQUEST BODY SCHEMA : application/json

An array of max `64` items is allowed. Only the first `2000` characters from each text will be analyzed.

Parameter | Type        | Optionality | Description
--------- | ----------- | ----------- | -----------
id        | string      | Optional    | id of the post
text      | string      | Required    | the text to analyse
language  | string      | Required    | language_code of the text

## Language Detection


```shell
curl -X POST "https://api.symanto.net/language-detection" 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-H "x-api-key: opensesame" 
-d "[{\"id\":1,\"text\":\"Hello I love the service\"}]"
```

```python
import requests

url = "https://api.symanto.net/language-detection"

payload = "[{\"id\": \"1\",\"text\": \"Hello I love the service\"}]"
headers = {
    "x-api-key": "opensesame",
    "Content-Type": "application/json"
}
response = requests.request("POST", url, headers=headers, data=payload)
```

```java
OkHttpClient client = new OkHttpClient().newBuilder().build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create("[ { \"id\": \"1\", \"text\": \"Hello I love the service\" }]", mediaType);
Request request = new Request.Builder()
    .url("https://api.symanto.net/language-detection")
    .method("POST", body)
    .addHeader("x-api-key","opensesame")
    .build();
Response response = client.newCall(request).execute();
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
Identify the language of the input text. Only languages that our API supports can be analyzed.

Returned labels:
language_code of the detected language


### HTTP Request

`POST https://api.symanto.net/language-detection`

### REQUEST BODY SCHEMA : application/json

An array of max `64` items is allowed.

Parameter | Type        | Optionality | Description
--------- | ----------- | ----------- | -----------
id        | string      | Optional    | id of the post
text      | string      | Required    | the text to analyse
