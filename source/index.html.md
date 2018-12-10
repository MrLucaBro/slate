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

Welcome to the RAYPACK AI Platform. Our platform is a fully integrated solution enabling users to deploy and develop AI models . We offer ready-to-deploy as well as custom models to improve the efficiency of your business with AI. All our models are deployable as a service on our platform or can be conveniently embedded in existing systems on-premise. You can use our API to run AI models and receive their output as an image (.jpg) or as a JSON file. The main language to access our API is Shell, but we also set up some experimental Python code. You can view code examples in the dark area to the right, and you can switch to the programming language of your choice with the tabs in the top right.



# Authentication

> To authorize, use your API-key in the blank space after 'apikey='in every request you send:


```python
import RAYPACK

api = RAYPACK.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request.
curl -X POST -F "apikey=meowmeowmeow" ...
```


Our platforms uses API-keys to allow access to the API. You can register for a trial key at our [homepage](http://raypack.ai).

In general the API expects for the API-key to be included in all API requests to the server as a parameter, that looks like the following example:

-F "apikey: meowmeowmeow"

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# RAYPACK AI models
Currently the RAYPACK AI platform offers 5 pre-trained models.
These models are:

* Multi-object detection
* Food detection
* Face AI
* Celebrity recognition US
* Demographics analyzer.

## RAYPACK Multi-Object detection

```python
import
```
> The command below requests the analysis of the image given in file and returns a JSON:

```shell
curl -X POST -F "apikey=meowmeowmeow" -F "threshold=1.0"
-F "file=@/Users/luca/Documents/Aiso.Lab/API_Doku/Bilder/richard-clark-1177371-unsplash.jpg"
-F "model=1" -F "lang=de" "https://apiv3.raypack.ai/recog"
```

> The above command returns a JSON like so:

```json
{
"name":"Raypack_AI_Filecontainer",
"version":"1.0",
"license":"commercial",
"results":{
    "stats":{
    "modelname":"Raypack_Food",
	 "modelid":"2",
	 "originalfile":"https://static.chefkoch-cdn.de/ck.de/rezepte/177/177746/480010-960x720-nudelauflauf-hawaii.jpg",
	 "starttime":1544183968616,
	 "endtime":1544183970545,
	 "duration":1.929},
	"tags":[
      {"name":"pasta","value":"1.00000000"},
      {"name":"sauce","value":"1.00000000"},
      {"name":"cheese","value":"1.00000000"},
      {"name":"macaroni","value":"1.00000000"}
    ]
  }
}
```

RAYPACK Multi-Object Detection is a ready-to-deploy AI model, that enables simultaneous detection of all kinds of objects. It comes with a large number of pre-trained objects and can be extended to other objects relevant to your business needs. Its highly accurate performance and flexibility make RAYPACK Multi-Object Detection your best choice for almost any camera-based business application.

<aside class="warning">Videos are not supported yet.</aside>

### HTTP Request

POST `https://apiv3.raypack.ai/recog`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | 0.9 | Sets the threshold of detection certainty required to return an object as detected.
file | - | Lets you specify your input file.
model | - | Lets you specify if you want to detect objects in general (1), foods (2) or celebrities (3).
lang | de | Language of the output. Can be English (lang=en) or German (lang=de).

### JSON response schema

Parameter | Type | Description
--------- | ------- | -----------
name | string | Name of the response
version | float | Version of the response container
license | string |  Type of the purchased API-key
results | dict |  Contains the results of the analysis in stats and tags
stats | dict |  Contains model statistics
modelname | string |  Name of the model used
modelid | string |  Internal model identifier
originalfile | string |  File given to the model in the request
starttime | float |  System time of the start of model execution
endtime | float |  System time of the end of the calculation
duration | float |  Processing time
tags | dict |  Contains Name and confidence of the detected objects (both strings)


## RAYPACK Face AI

```python
import ...
```
> The command below requests the analysis of the image in imagef and returns the results as a JSON or JPEG:

```shell
curl -X POST -F "meowmeowmeow"
-F "threshold=0.9" -F "imagef=https://cvdazzle.com/assets/img/look5r-md.jpg"
-F "mode=json" -F "facemode=default" -F "hex=00ff00" "http://otc.raypack.ai:5000/raypackfacev3"

```


> The above command returns JSON structured like so:

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

> Or an image like so, if you chose the default option for anonymization:    
<img src="/images/test_default_grün.jpg">

RAYPACK Face AI is a ready-to-deploy AI model, that enables detection as well as identification of faces. Its unprecedented performance in a broad range of circumstances, including massive occlusion and crowds, makes RAYPACK Face AI an accurate and versatile tool for commercial face detection.  


### HTTP Request

POST `http://otc.raypack.ai:5000/raypackfacev3`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | 0.9 | Sets the threshold of detection certainty required to return an object as detected.
imagef | - | Lets you specify your input file.
mode |image | Defines the form of returned output. The model can return jpeg images (mode=image), JSON structures (mode=json) or both(mode=jsonimage).
facemode | - | Lets you determine the level of anonymization in the output. You can decide if you want the original image with a bounding box (facemode=default), blurred faces (facemode=pixel), faces replaced with rectangles (facemode=fill) or only core information on black background (facemode=black).

<aside class="success">
Remember — always use your API-key to validate your request!
</aside>

### JSON response schema

Parameter | Type | Description
--------- | ------- | -----------
totalfaces | integer | Number of detected faces within the image
time | float | Time spent processing the image
faces | dict |  Bounding box(es) of the detected face(s) with xpos, ypos, width, height and confidence


## RAYPACK Celebrity detection US

```python
import
```

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
		 {"name":"cheese","value":"1.00000000"},
     {"name":"macaroni","value":"1.00000000"}]}
}
```

RAYPACK Celebrity detection US lets you automatically detect the identity of celebrities in videos and images.
The model can be expanded with any desired celebrity or common person.

<aside class="warning">Videos are not supported yet.</aside>

### HTTP Request

POST `https://apiv3.raypack.ai/recog`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | 0.9 | Sets the threshold of detection certainty.
file | - | Lets you specify the location of your input file.
model | - | Lets you specify if you want to detect objects in general (1), foods (2) or celebrities (3).
lang | de | Language of the output.

## RAYPACK Demographics detection

```python
import
```

```shell
curl -X POST -F "apikey=meowmeowmeow" -F "threshold=0.2"
-F "url=https://www.br.de/fernsehen/das-erste/sendungen/report-muenchen/videos-und-manuskripte/kuenstliche-intelligenz-126~_v-img__16__9__xl_-d31c35f8186ebeb80b0cd843a7c267a0e0c81647.jpg"
-F "model=5" -F "lang=de" "https://apiv3.raypack.ai/recog"
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
		 {"name":"cheese","value":"1.00000000"},
     {"name":"macaroni","value":"1.00000000"}]}
}
```

RAYPACK Demographics


### HTTP Request

POST `https://apiv3.raypack.ai/recog`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | 0.9 | Sets the threshold of detection certainty.
file | - | Lets you specify the location of your input file.
model | - | Lets you specify if you want to detect objects in general (1), foods (2) or celebrities (3).
lang | de | Language of the output.
