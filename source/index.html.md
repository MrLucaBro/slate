---
title: RAYPACK API Platform Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://raypack.ai'>Sign Up for a trial API-key</a>
  - <a>Documentation Version 1.0.1.</a>


includes:
  - errors

search: true
---

# Introduction

Welcome to the RAYPACK AI Platform. Our platform is a fully integrated solution enabling users to deploy and develop AI models. We offer ready-to-deploy as well as custom models to improve the efficiency of your business with AI. All our models are deployable as a service on our platform or can be conveniently embedded into existing systems on-premise. You can use our API to run AI models and receive their output as an image (.jpg) or as a JSON file. The main language used to access our API is Shell, but you can customize the code examples to any language you prefer. You can view code examples in the dark area to the right.



# Authentication

> To authorize, use your API-key in the blank space after 'apikey='in every request you send:


```shell
# With shell, you can just pass the correct header with each request.
curl -X POST -F "apikey= " ...
```


Our platform uses API-keys to allow access to the API. You can register for a trial key at our [homepage](http://raypack.ai).

The server expects the API-key to be included in all API requests as a parameter, that looks like the following example:

-F "apikey:****"

<aside class="notice">
You must replace <code>****</code> with your personal API key.
</aside>

# RAYPACK AI models
> The call below requests a list of available models and returns it as a JSON:

```shell
curl -X POST -F 'apikey= ' 'https://api.raypack.ai/getmodels'
```

The RAYPACK AI platform offers a number of ready-to-deploy models.
These models are:

* Multi-object detection
* Food detection
* Face AI
* Celebrity Detection US
* Demographics Detection

You can connect with the RAYPACK Platform API by sending http requests to our API server `https://api.raypack.ai`.
You can get an overview over all available models by sending the http request on the right to the endpoint `https://api.raypack.ai/getmodels`. The models themselves are available under the endpoint `https://api.raypack.ai/recog`. In this section we will give detailed examples of how you could use each of our ready-to-deploy models.

## RAYPACK Multi-Object Detection

> The call below requests the analysis of the image given in file and returns a JSON:  
Here is an example:  
<img src="/images/rawpixel-645294-unsplash.jpg">

```shell
curl -X POST -F "apikey= " -F "threshold=0.9"
-F "file=rawpixel-645294-unsplash.jpg"
-F "model=1" -F "lang=de" "https://api.raypack.ai/recog"

```

> The above call returns a JSON like so:

```json
{
  "name":"Raypack_AI_Filecontainer",
  "version":"1.0",
  "license":"commercial",
  "results":
  {
    "stats":
    {
      "modelname":"Raypack_General",
      "modelid":"1",
      "originalfile":"rawpixel-645294-unsplash.jpg",
      "starttime":1544690825238,
      "endtime":1544690827012,
      "duration":1.774
    },
    "tags":
    [
      {"name":"keine Person","value":"1.00000000"},
      {"name":"papier","value":"1.00000000"},
      {"name":"unternehmen","value":"1.00000000"},
      {"name":"laptop","value":"0.97501550"},
      {"name":"Daten","value":"0.95598294"},
      {"name":"dokument","value":"0.91890140"},
      {"name":"technologie","value":"0.91787786"},
      {"name":"büro","value":"0.91769530"}
    ]
  }
}
```

RAYPACK Multi-Object Detection is a ready-to-deploy AI model, that enables simultaneous detection of all kinds of objects. It comes with a large number of pre-trained objects and can be extended to others relevant to your business needs. Its highly accurate performance and flexibility make RAYPACK Multi-Object Detection your best choice for almost any camera-based business application.

<aside class="warning">Videos are not supported yet.</aside>

### HTTP Request

POST `https://api.raypack.ai/recog`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | - | Sets the threshold of detection certainty required to return an object as detected.
file | - | Lets you specify your input file.
url | - | Lets you upload your file from the internet without saving it on your system.
model | - | Indicates which model you want to use. Multi-Object `model=1`, Food `model=2`, Celebrity US `model=3`, Face AI `model=4`, Demographics `model=5`
lang | - | Language of the output. You can choose between English `lang=en` or German `lang=de`.

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
tags | dict |  Contains name and confidence value of the detected objects (both strings)

## RAYPACK Food Detection

> The call below requests the analysis of the image given in file and returns a JSON:  
Here is an example:  
<img src="/images/burger.jpg">

```shell
curl -X POST -F "apikey= " -F "threshold=0.9"
-F "file=burger.jpg"
-F "model=2" -F "lang=de" "https://api.raypack.ai/recog"

```

> The above call returns a JSON like so:

```json
{
"name":"Raypack_AI_Filecontainer",
"version":"1.0",
"license":"commercial",
"results":
{
  "stats":
  {
    "modelname":"Raypack_Food",
    "modelid":"2",
    "originalfile":"burger.jpg",
    "starttime":1545033109771,
    "endtime":1545033112489,
    "duration":2.718
  },
  "tags":
  [
    {"name":"hamburger","value":"0.97055126"},
    {"name":"bun","value":"0.94517506"},
    {"name":"beef","value":"0.91858010"},
    {"name":"onion","value":"0.91512306"}
  ]
}
}
```

RAYPACK Food Detection is a ready-to-deploy AI model, that enables detection of foods. It can be used to detect many different classes of foods and can be expanded upon request.

<aside class="warning">Videos are not supported yet.</aside>

### HTTP Request

POST `https://api.raypack.ai/recog`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | - | Sets the threshold of detection certainty required to return an object as detected.
file | - | Lets you specify your input file.
url | - | Lets you upload your file from the internet without saving it on your system.
model | - | Indicates which model you want to use. Multi-Object `model=1`, Food `model=2`, Celebrity US `model=3`, Face AI `model=4`, Demographics `model=5`
lang | - | Language of the output. You can choose between English `lang=en` or German `lang=de`.

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
tags | dict |  Contains name and confidence value of the detected food objects (both as strings)

## RAYPACK Celebrity Detection US

> The call below requests the analysis of the image given in file and returns a JSON:  
Here is an example:  
<img src="/images/Brad_Pitt_at_Incirlik2.jpg">

```shell
curl -X POST -F "apikey= " -F "threshold=0.9"
-F "file=Brad_Pitt_at_Incirlik2.jpg"
-F "model=3" -F "lang=de" "https://api.raypack.ai/recog"

```

> The above call returns JSON structured like so:

```json
{
  "name":"Raypack_AI_Filecontainer",
  "version":"1.0",
  "license":"commercial",
  "results":
  {
    "stats":
    {
      "modelname":"Raypack Celeb US",
      "modelid":"3",
      "originalfile":"Brad_Pitt_at_Incirlik2.jpg",
      "starttime":1544679684188,
      "endtime":1544679685623,
      "duration":1.435
    },
    "tags":
    [
      {
        "top":0.13956678,
        "left":0.5285845,
        "bottom":0.32516763,
        "right":0.769893,
        "idents":
        [
          {
            "name":"brad pitt",
            "value":0.9541806
          },
        ]
      }
    ]
  }
}
```

RAYPACK Celebrity detection US lets you automatically detect the identity of celebrities in videos and images.
The model can be expanded with any desired celebrity or common person.

<aside class="warning">Videos are not supported yet.</aside>

### HTTP Request

POST `https://api.raypack.ai/recog`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | - | Sets the threshold of detection certainty required to return an object as detected.
file | - | Lets you specify your input file.
url | - | Lets you upload your file from the internet without saving it on your system.
model | - | Indicates which model you want to use. Multi-Object `model=1`, Food `model=2`, Celebrity US `model=3`, Face AI `model=4`, Demographics `model=5`
lang | - | Language of the output. You can choose between English `lang=en` or German `lang=de`.

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
tags | dict |  Contains Name and confidence value of the detected celebrity as well as the location on the image

## RAYPACK Face AI

> The call below requests the analysis of the image in url and returns the results as a JSON or JPEG:

```shell
curl -X POST -F "apikey= "
-F "threshold=0.9" -F "url=https://cvdazzle.com/assets/img/look5r-md.jpg"
-F "mode=json" -F "facemode=default" -F "hex=00ff00" "https://api.raypack.ai/recog"

```


> The above call returns JSON structured like so:

```json

{
  "name":"Raypack_AI_Filecontainer",
  "version":"1.0",
  "license":"commercial",
  "results":
  {
    "stats":
    {
      "modelname":"RaypackFace",
      "modelid":"4",
      "originalfile":"https://cvdazzle.com/assets/img/look5r-md.jpg",
      "starttime":1545035189345,
      "endtime":1545035195714,
      "duration":1.23
    },
    "totalfaces": 1,
    "faces":
    [
        {
            "xpos": 123,
            "ypos": 81,
            "width": 220,
            "height": 216,
            "score": 0.9990518015849545
        }
    ],
  }
}
```

> Or an image like so, if you chose the default option for anonymization:    
<img src="/images/test-default-gruen.jpg">

RAYPACK Face AI is a ready-to-deploy AI model, that enables detection as well as identification of faces. Its unprecedented performance in a broad range of difficult conditions, including massive occlusion of faces, and large crowds, makes RAYPACK Face AI an accurate and versatile tool for commercial face detection.   


### HTTP Request

POST `https://api.raypack.ai/recog`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | - | Sets the threshold of detection certainty required to return an object as detected.
file | - | Lets you specify your input file.
url | - | Lets you upload your file from the internet without saving it on your system.
model | - | Indicates which model you want to use. Multi-Object `model=1`, Food `model=2`, Celebrity US `model=3`, Face AI `model=4`, Demographics `model=5`
lang | - | Language of the output. You can choose between English `lang=en` or German `lang=de`.
mode | - | Defines the form of returned output. The model can return JPEG images `mode=image`, JSON files `mode=json` or both `mode=jsonimage`.
facemode | - | Lets you determine the level of anonymization in the output. You can decide if you want the original image with a bounding box `facemode=default`, blurred faces `facemode=pixel`, faces replaced with rectangles `facemode=fill` or only core information on black background `facemode=black`.
facefinder | 3 | Lets you determine the level of upscaling of the image given to the model. The options are: No upscaling `facefinder=1`, upscaling by a factor of 0.5 `facefinder=1` and upscaling by the factors 2, 1 and 0.5 `facefinder=3` .
hex | - | Lets you determine the color of the bounding boxes drawn onto the output images. For example `hex=#FF0000` for red bounding boxes. You can enter the value in upper and lower cases and with or without the #.

<aside class="success">
Remember — always use your API-key to validate your http request!
</aside>

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
totalfaces | integer | Number of detected faces within the image
faces | dict |  Bounding box(es) of the detected face(s)
xpos | float |  Top left bounding box corner x-coordinate
ypos | float |  Top left bounding box corner y-coordinate
height | float |  Height of the bounding box
width | float |  Width of the bounding box
score | float |  Confidence score of the accuracy of the detection

## RAYPACK Face AI v4

> The call below requests the analysis of the image given in file and returns a JSON:  
Here is an example:  
<img src="/images/CVD_4.jpg">

```shell
curl -X POST -F "apikey= " -F "threshold=0.5"
-F "file=CVD_4.jpg"
-F "model=41" -F "lang=de" "https://api.raypack.ai/recog"

```

> The above call returns JSON structured like this:

```json
{
  "name":"Raypack_AI_Filecontainer",
  "version":"1.0",
  "license":"commercial",
  "results":
  {
    "stats":
    {
      "modelname":"Raypack_Face_V4",
      "modelid":"41",
      "originalfile":"CVD_4.jpg",
      "starttime":1545044610981,
      "endtime":1545044612198,
      "duration":1.217
    },
    "totalfaces": 1,
    "faces":
    [
        {
            "top":0.23464786,
            "left":0.37956652,
            "right":0.8106986,
            "bottom":0.53359973,
        }
    ],
  }
}
```

RAYPACK Face AI v4 is faster and more efficient than the standard Face AI.


### HTTP Request

POST `https://apiv3.raypack.ai/recog`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | - | Sets the threshold of detection certainty required to return an object as detected.
file | - | Lets you specify your input file.
url | - | Lets you upload your file from the internet without saving it on your system.
model | - | Indicates which model you want to use. Multi-Object `model=1`, Food `model=2`, Celebrity US `model=3`, Face AI `model=4`, Demographics `model=5`
lang | - | Language of the output. You can choose between English `lang=en` or German `lang=de`.

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
totalfaces | integer | Number of detected faces within the image
faces | dict |  Bounding box(es) of the detected face(s)
top | float |  Top left bounding box corner coordinate
left | float |  Top left bounding box corner coordinate
right | float |  Bottom right bounding box corner coordinate
bottom | float |  Bottom right bounding box corner coordinate

## RAYPACK Demographics Detection

> The call below requests the analysis of the image given in file and returns a JSON:  
Here is an example:  
<img src="/images/ki.jpg">

```shell
curl -X POST -F "apikey= " -F "threshold=0.4"
-F "file=ki.jpg"
-F "model=5" -F "lang=de" "https://api.raypack.ai/recog"

```

> The above call returns JSON structured like this:

```json
{
  "name":"Raypack_AI_Filecontainer",
  "version":"1.0",
  "license":"commercial",
  "results":
  {
    "stats":
    {
      "modelname":"Raypack_Demographics",
      "modelid":"5",
      "originalfile":"ki.jpg",
      "starttime":1544680153203,
      "endtime":1544680154600,
      "duration":1.397
    },
    "tags":
    [
      {
        "age":"46",
        "gender":"masculine",
        "culture":"white",
        "faceregion":
        {
          "top_row":0.22344437,
          "left_col":0.2502877,
          "bottom_row":0.6817542,
          "right_col":0.50777674
        },
        "value":"0.57789720"
      }
    ]
  }
}
```

RAYPACK Demographics detects faces and adds demographic information.


### HTTP Request

POST `https://apiv3.raypack.ai/recog`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | - | Sets the threshold of detection certainty required to return an object as detected.
file | - | Lets you specify your input file.
url | - | Lets you upload your file from the internet without saving it on your system.
model | - | Indicates which model you want to use. Multi-Object `model=1`, Food `model=2`, Celebrity US `model=3`, Face AI `model=4`, Demographics `model=5`
lang | - | Language of the output. You can choose between English `lang=en` or German `lang=de`.

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
tags | dict |  Contains Name and confidence of the detected celebrity as well as the location on the image

## RAYPACK Fashion Detection

> The call below requests the analysis of the image given in file and returns a JSON:  
Here is an example:  
<img src="/images/fashion.jpg">

```shell
curl -X POST -F "apikey= " -F "threshold=0.4"
-F "file=fashion.jpg"
-F "model=6" -F "lang=de" "https://api.raypack.ai/recog"

```

> The above call returns JSON structured like this:

```json
{
  "name":"Raypack_AI_Filecontainer",
  "version":"1.0",
  "license":"commercial",
  "results":
  {
    "stats":
    {
      "modelname":"Raypack_Clothes",
      "modelid":"6",
      "originalfile":"fashion.jpg",
      "starttime":1545042059125,
      "endtime":154504206115,
      "duration":2.034
    },
    "tags":
    [
      {"name":"Fur Coat","value":"0.79121980"},
      {"name":"Cardigan","value":"0.62127545"},
      {"name":"Turtleneck","value":"0.50549158"},
    ]
  }
}
```

RAYPACK Demographics detects clothing items in images.


### HTTP Request

POST `https://apiv3.raypack.ai/recog`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | - | Sets the threshold of detection certainty required to return an object as detected.
file | - | Lets you specify your input file.
url | - | Lets you upload your file from the internet without saving it on your system.
model | - | Indicates which model you want to use. Multi-Object `model=1`, Food `model=2`, Celebrity US `model=3`, Face AI `model=4`, Demographics `model=5`
lang | - | Language of the output. You can choose between English `lang=en` or German `lang=de`.

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
tags | dict |  Contains Name and confidence of the detected clothing item as well as the location on the image
