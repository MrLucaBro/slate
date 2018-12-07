---
title: RAYPACK API Platform Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python

toc_footers:
  - <a href='https://raypack.ai'>Sign Up for a trial API-key</a>


includes:
  - errors

search: true
---

# Introduction

Welcome to the RAYPACK AI Platform! You can use our API to run AI models and receive their output via jpeg or json.

We have language bindings mainly in Shell, but we also set up some experimental Python code! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.



# Authentication

> To authorize, use your API-key in the blank space after 'apikey='in every request you send:


```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request.
curl -X POST -F "apikey=meowmeowmeow" ... 
```

> Make sure to replace `meowmeowmeow` with your API key.

RAYPACK AI uses API-keys to allow access to the API. You can register for a trial key at our [homepage](http://raypack.ai).

The API expects for the API-key to be included in all API requests to the server in a header that looks like the following:

F "apikey: meowmeowmeow"

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# RAYPACK AI models
Currently the RAYPACK AI platform offers face detection, food detection and object recognition

## RAYPACK Face AI

```python
import ...
```

```shell
curl -X POST -F "meowmeowmeow"
-F "threshold=0.9" -F "imagef=https://cvdazzle.com/assets/img/look5r-md.jpg" 
-F "mode=json" -F "facemode=default" -F "hex=00ff00" "http://otc.raypack.ai:5000/raypackfacev3"

```


> The above command returns JSON structured like this:

```json
{
    "totalfaces": 1,
    "time": 1.422919750213623,
    "faces": [
        {
            "xpos": 268,
            "ypos": 102,
            "width": 463,
            "height": 318,
            "score": 0.9999999957373409
        }
    ]
}
```

This endpoint lets you use FACE AI with your own images.

Our Face AI is very accurate in a broad range of circumstances. One output example would be:
![alt text](/source/images/logo.png)

### HTTP Request

POST `http://otc.raypack.ai:5000/raypackfacev3`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | 0.9 | Sets the threshold of detection certainty.
imagef | - | Lets you specify the location of your input file.
Mode |image | Defines the form of returned output. Can be jpg, json .
facemode | - | Lets you determine the level of anonymization in the output. default (none), pixel (blurred), fill (face replaced by colored rectangle) and black (only bounding boxes) and jsonimage (both image and json)

<aside class="success">
Remember — always use your API-key to validate your request!
</aside>

## Object Detection

<img src="/source/images/logo.png" class="lang-specific python">

```shell
curl -X POST -F "apikey=meowmeowmeow" -F "threshold=1.0" 
-F "file=@/Users/luca/Documents/Aiso.Lab/API_Doku/Bilder/richard-clark-1177371-unsplash.jpg"
-F "model=1" -F "lang=de" "https://apiv3.raypack.ai/recog"
```

> The above command returns JSON structured like this:

```json
{
"name":"Raypack_AI_Filecontainer",
"version":"1.0",
"license":"commercial",
"results":
	{"stats": 
		{"modelname":"Raypack_Food",
		 "modelid":"2",
		 "originalfile":"https://static.chefkoch-cdn.de/ck.de/rezepte/177/177746/480010-960x720-nudelauflauf-hawaii.jpg",
		 "starttime":1544183968616,
		 "endtime":1544183970545,
		 "duration":1.929},
	"tags":
		[{"name":"pasta","value":"1.00000000"},
                 {"name":"sauce","value":"1.00000000"},
		 {"name":"cheese","value":"1.00000000"},{"name":"macaroni","value":"1.00000000"}]}
}
```

This endpoint lets you detect objects in pictures and videos.

<aside class="warning">Videos are not supported yet.</aside>

### HTTP Request

POST `https://apiv3.raypack.ai/recog`

### URL Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | 0.9 | Sets the threshold of detection certainty.
File | - | Lets you specify the location of your input file.
model | - | Lets you specify if you want to detect objects in general (1) or foods (2).
lang | de | Language of the output json



