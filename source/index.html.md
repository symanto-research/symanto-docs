---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - java

toc_footers:
  - <p><a href='https://www.symanto.com/get-in-touch/' target='_blank'>Get in Touch</a></p>
  - <p><a href='https://api.symanto.net/docs' target='_blank'>Try it out in Swagger</a></p>
  - <p><a href='https://app.getpostman.com/run-collection/f464466e1f0bc5af1f18' target='_blank'><img src="https://run.pstmn.io/button.svg"></img></a></p>
    - <p><a href="https://rapidapi.com/collection/symanto-symanto-default-apis" target="_blank"><img src="https://storage.googleapis.com/code-snippets/connect-on-rapidapi-light.png" width="150" alt="Connect on RapidAPI"></a></p>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Symanto API! You can use our API to access the API endpoints, which can get insight on text using our AI technology.

We have language binding in Shell. You can view code examples in the dark area to the right.

# Authentication

> Make sure to replace `opensesame` with your API key.

Symanto API uses API keys to allow access to the API. Please [get in touch](https://www.symanto.com/get-in-touch/) to receive an API key.

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

Predict the personality traits to understand how the author of the written text makes decisions, whether they are Emotional (relationship-oriented, focusing on social values and empathy) or Rational (objective and pragmatic, focusing on facts and logical deduction).

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

## Emotion Analysis `experimental`

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

Detect the emotion expressed in the text. 

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





## Ekman Emotion Analysis

```shell
curl -X POST "https://api.symanto.net/ekman-emotion" 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-H "x-api-key: opensesame" 
-d "[{\"id\":1,\"text\":\"I love the service\",\"language\":\"en\"}]"
```

```python
import requests

url = "https://api.symanto.net/ekman-emotion"

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
    .url("https://api.symanto.net/ekman-emotion")
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
                "probability": 0.8415710926055908
            }
        ]
    }
]
```

Detect the emotion expressed in the text. 

Supported language codes are: [ `de`, `en`, `es` ]

Retrieved emotions can be any of: [`anger`, `disgust`, `fear`, `joy`,`no-emotion`, `sadness`, `surprise`]


### HTTP Request

`POST https://api.symanto.net/ekman-emotion`

### Query Parameters

Parameter | Type    | Default | Description
--------- | ------- | ------- | -----------
all       | bool    | false   | returns all predictions, not only the most probable one

### REQUEST BODY SCHEMA : application/json

An array of max `8` items is allowed.

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
Detect the text-level sentiment from a piece of text.

Supported Languages: [`en`, `de`, `es`, `ar`, `zh`, `tr` ]

Returned labels: [`positive`, `negative`]


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

Supported Languages: [`de`, `en`, `es`, `ar`]

### HTTP Request

`POST https://api.symanto.net/topic-sentiment`

### Query Parameters

Parameter | Default | Optionality | Description
--------- | ------- | ----------- | -----------
domain    | -       | Optional    | Provide analysis domain for domain-specific extraction. When not provided a generic model will be applied.

### Available domains

Enum        | Description | Supported Languages
---------   | ----------- | -----------
Automotive  | Use this domain to retrieve insights about attitude & behaviour, brand, communication, components, functions & services, location & facility, mobility & transfer, monetary, overall experience, product, service. | en, de, es
Banking     | Use this domain to retrieve insights about banking, borrowing, customer service, digital experience, financial fitness, location & facility, product.  | en, es
ConsumerElectronics     | Use this domain to retrieve insights about appearance&handling, attitude&behavior, brand, connectivity, delivery service, online experience, performance, product components, retailer, service and software.  | en, de, es, ar
Ecom        | Use this domain to retrieve insights about experience, product and service.  | en, de, es, ar
Employee    | Use this domain to retrieve insights about associates, communication, culture, development & resources, leadership & planning, overall perception, pay & benefits, role, treatment and work environment.  | en, de, es
Hotel       | Use this domain to retrieve insights about associates, booking process, brand, facilities, food&beverage, hotel areas, hotel front office, hotel room, marketing, monetary, overall experience, parking, transport, venue, washrooms, website, wellness/recreation.   | en, de, es
Pharma      | Use this domain to retrieve insights about disease, duration, healthcare professional, healthtech, interaction, medication names, mode of administration, patient characteristics, product attributes, quality of life, studies & education.  | en, es
Restaurant  | Use this domain to retrieve insights about app/website, eating frequency, eating time, health & dietry needs, marketing, overall experience, process, product, service, social, venue.  | en, de, es, ar
Retail      | Use this domain to retrieve insights about marketing, experience, product, service, staff service, store.  | en, de, es, ar




### REQUEST BODY SCHEMA : application/json

An array of max `64` items is allowed. Only the first `2000` characters from each text will be analyzed.

Parameter | Type        | Optionality | Description
--------- | ----------- | ----------- | -----------
id        | string      | Optional    | id of the post
text      | string      | Required    | the text to analyse
language  | string      | Required    | language_code of the text


## Brand recommendation analysis

```shell
curl -X POST "https://api.symanto.net/brand-recommendation" 
-H "accept: application/json" 
-H "Content-Type: application/json" 
-H "x-api-key: opensesame" 
-d "[{\"id\":1,\"text\":\"Hello I love the service\",\"language\":\"en\"}]"
```

```python
import requests

url = "https://api.symanto.net/brand-recommendation"

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
    .url("https://api.symanto.net/brand-recommendation")
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
        "predictions": [
            {
                "probability": 1.0,
                "prediction": "Promote"
            }
        ]
    }
]
```
Detects if the text is a promoter, detractor or an indifferent suggestion.

Supported Languages: [`de`, `en`, `es`]

### HTTP Request

`POST https://api.symanto.net/brand-recommendation`

### Query Parameters

Parameter | Default | Optionality | Description
--------- | ------- | ----------- | -----------
domain    | -       | Optional    | Provide analysis domain for domain-specific extraction. When not provided a generic model will be applied.

### Available domains

Enum        | Description | Supported Languages
---------   | ----------- | -----------
Automotive  | Use this domain to retrieve insights about attitude & behaviour, brand, communication, components, functions & services, location & facility, mobility & transfer, monetary, overall experience, product, service. | en, de, es
Banking     | Use this domain to retrieve insights about banking, borrowing, customer service, digital experience, financial fitness, location & facility, product.  | en
ConsumerElectronics     | Use this domain to retrieve insights about appearance&handling, attitude&behavior, brand, connectivity, delivery service, online experience, performance, product components, retailer, service and software.  | en
Ecom        | Use this domain to retrieve insights about experience, product and service.  | en, de, es
Employee    | Use this domain to retrieve insights about associates, communication, culture, development & resources, leadership & planning, overall perception, pay & benefits, role, treatment and work environment.  | en, de
Hotel       | Use this domain to retrieve insights about associates, booking process, brand, facilities, food&beverage, hotel areas, hotel front office, hotel room, marketing, monetary, overall experience, parking, transport, venue, washrooms, website, wellness/recreation.   | en, de, es
Pharma      | Use this domain to retrieve insights about disease, duration, healthcare professional, healthtech, interaction, medication names, mode of administration, patient characteristics, product attributes, quality of life, studies & education.  | en
Restaurant  | Use this domain to retrieve insights about app/website, eating frequency, eating time, health & dietry needs, marketing, overall experience, process, product, service, social, venue.  | en, de, es
Retail      | Use this domain to retrieve insights about marketing, experience, product, service, staff service, store.  | en, de, es




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
Identify the language of the input text. 

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
