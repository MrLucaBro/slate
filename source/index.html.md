---
title: RAYPACK API Platform Documentation

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://raypack.ai/trial-api-key/'>Sign Up for a trial API-key</a>
  - <a>Documentation Version 1.1.0.</a>


includes:
  - errors

search: true
---

# Introduction

Welcome to the RAYPACK AI Platform. Our platform is a fully integrated solution enabling users to deploy and develop AI models. We offer ready-to-deploy as well as custom models to improve the efficiency of your business with AI. All our models are deployable as a service on our platform or can be conveniently embedded into existing systems on-premise. You can use our API to run AI models and receive their output as an image (.jpg) or as a JSON file. The main language used to access our API is Shell, but you can customize the code examples to any language you prefer. You can view code examples in the dark area to the right.



# Authentication

> To authorize, use your API-key in the blank space after 'apikey='in every request you send:


```shell
# With shell, you can just pass the correct parameter with each request.
curl -X POST -F "apikey=****" ...
```


Our platform uses API-keys to allow access to the API. You can register for a trial key at our [homepage](http://raypack.ai).

The server expects the API-key to be included in all API requests as a parameter, that looks like the following example:

-F "apikey:****"

<aside class="notice">
You must replace <code>****</code> with your personal API key.
</aside>

# RAYPACK AI Models
> The call below requests a list of available models and returns it as a JSON:

```shell
curl -X POST -F 'apikey=****' 'https://api.raypack.ai/getmodels'
```

```json
{
  "response":
  [
  {"name":"general","id":"1","desc":"Raypack Generall Modell","parameters":"model=Defines the modelID,language=defines the languages (currently de or en)","pricing":"0.02"},
  {"name":"food","id":"2","desc":"Raypack Food Modell. Returns JSON Back","parameters":"model=Defines the modelID,language=defines the languages (currently de or en)","pricing":"0.02"},
  {"name":"celeb_us","id":"3","desc":"Raypack Celeb US.","parameters":"model=Defines the modelID,language=defines the languages (currently de or en)","pricing":"0.02"},
  {"name":"raypackfacev3","id":"4","desc":"This is the Raypack Face Version 3 Model","parameters":"model=Defines the modelID,language=defines the languages (currently de or en)","pricing":"0.02"},
  {"name":"raypackfacev4","id":"41","desc":"This is the Raypack Face Version 4 Model (faster then Model 3)","parameters":"model=Defines the modelID,language=defines the languages (currently de or en)","pricing":"0.025"},
  {"name":"demographics","id":"5","desc":"This is the Raypack Demographics Model","parameters":"model=Defines the modelID,language=defines the languages (currently de or en)","pricing":"0.02"},
  {"name":"clothes","id":"6","desc":"This is the Raypack Clothes Model","parameters":"model=Defines the modelID,language=defines the languages (currently de or en)","pricing":"0.02"},
  {"name":"Vector 512","id":"7","desc":"This is the Raypack Vector Model. It can extract 512 or 2048 Vectors","parameters":"model=Defines the modelID,language=defines the languages (currently de or en)","pricing":"0.02"},
  {"name":"Vector 2048","id":"8","desc":"This is the Raypack Vector Model.","parameters":"model=Defines the modelID,language=defines the languages (currently de or en)","pricing":"0.02"},
  {"name":"Color","id":"9","desc":"This is the Raypack Color Model.","parameters":"model=Defines the modelID,language=defines the languages (currently de or en)","pricing":"0.02"},
  {"name":"Object","id":"10","desc":"This is the Raypack Object Model.","parameters":"model=Defines the modelID,language=defines the languages (currently de or en)","pricing":"0.02"}
  ]
}
```

The RAYPACK AI platform offers a number of ready-to-deploy models.
These models are:

1. RAYPACK Multi-Object Detection
2. RAYPACK Multi-Object Localization
3. RAYPACK Food Detection
4. RAYPACK Celebrity Detection US
5. RAYPACK Face AI
6. RAYPACK Face AI fast
7. RAYPACK Demographics Detection
8. RAYPACK Fashion Detection
9. RAYPACK Color Model

You can connect with the RAYPACK Platform API by sending http requests to our API server `https://api.raypack.ai`.
You can get an overview over all available models by sending the http request on the right to the endpoint `https://api.raypack.ai/getmodels`. The models themselves are available under the endpoint `https://api.raypack.ai/recog`. In this section, we will give detailed examples of how you can use each of our ready-to-deploy models.

## RAYPACK Multi-Object Detection

> The call below requests the analysis of the image given in file and returns a JSON:  
Here is an example:  
<img src="/images/rawpixel-645294-unsplash.jpg">

```shell
curl -X POST -F "apikey=****" -F "threshold=0.9" \
-F "file=@rawpixel-645294-unsplash.jpg" \
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
threshold | - | Sets the threshold of detection confidence required to return an object as detected.
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

## RAYPACK Multi-Object Localization
> The call below requests the analysis of the image given in file and returns a JSON:  
Here is an example:  
<img src="/images/rawpixel-645294-unsplash.jpg">

```shell
curl -X POST -F "apikey=****" -F "threshold=0.5" \
-F "file=@rawpixel-645294-unsplash.jpg" \
-F "model=10" -F "lang=de" "https://api.raypack.ai/recog"

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
      "modelname":"Raypack_Object",
      "modelid":"10",
      "originalfile":"rawpixel-645294-unsplash.jpg",
      "starttime":1548055347119,
      "endtime":1548055347589,
      "duration":0.47
    },
    "tags":
    [
      {
        "name":"Laptop",
        "score":0.8682193,
        "position":[{"x":0.680901,"y":0.321802},{"x":0.9990991,"y":0.321802},{"x":0.9990991,"y":0.96055114},{"x":0.680901,"y":0.96055114}]},
      {
        "name":"Computer keyboard",
        "score":0.6041973,
        "position":[{"x":0.680901,"y":0.321802},{"x":0.9990991,"y":0.321802},{"x":0.9990991,"y":0.96055114},{"x":0.680901,"y":0.96055114}]
      }
    ]
  }
}
```

The RAYPACK Multi-Object Localization model comes with all the advantages of the RAYPACK Multi-Object Detection model. In addition it provides precise localization of the detected objects within a picture, allowing users to track objects through consecutive frames or to define regions of interest.

<aside class="warning">Videos are not supported yet.</aside>

### HTTP Request

POST `https://api.raypack.ai/recog`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | - | Sets the threshold of detection confidence required to return an object as detected.
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
tags | dict |  Contains name and confidence score of the detected objects as well as their location.
position | list |  Contains x and y coordinates of top, bottom, left and right (in this order) corners of the bounding box containing the detected object.

## RAYPACK Food Detection

> The call below requests the analysis of the image given in file and returns a JSON:  
Here is an example:  
<img src="/images/burger.jpg">

```shell
curl -X POST -F "apikey=****" -F "threshold=0.9" \
-F "file=@burger.jpg" \
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
threshold | - | Sets the threshold of detection confidence required to return an object as detected.
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
curl -X POST -F "apikey=****" -F "threshold=0.9" \
-F "file=@Brad_Pitt_at_Incirlik2.jpg" \
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

RAYPACK Celebrity Detection US lets you automatically detect the identity of celebrities in videos and images. The model can be expanded with any desired celebrity or common person. It could be used to automate the analysis of archived videos or for processing of incoming footage in real time.

<aside class="warning">Videos are not supported yet.</aside>

### HTTP Request

POST `https://api.raypack.ai/recog`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | - | Sets the threshold of detection confidence required to return an object as detected.
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
tags | dict |  Contains name and confidence value of the detected celebrity as well as the location on the image

## RAYPACK Face AI

> The call below requests the analysis of the image in url and returns the results as a JSON or JPEG:

```shell
curl -X POST -F "apikey=****" \
-F "threshold=0.9" -F "url=https://cvdazzle.com/assets/img/look5r-md.jpg" -F "model=4" \
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
threshold | - | Sets the threshold of detection confidence required to return an object as detected.
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

## RAYPACK Face AI fast

> The call below requests the analysis of the image given in file and returns a JSON:  
Here is an example:  
<img src="/images/CVD_4.jpg">

```shell
curl -X POST -F "apikey=****" -F "threshold=0.5" \
-F "file=@CVD_4.jpg" \
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

RAYPACK Face AI fast is faster and more efficient than the standard Face AI. The increas in efficiency and speed don't decrease performance.


### HTTP Request

POST `https://api.raypack.ai/recog`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | - | Sets the threshold of detection confidence required to return an object as detected.
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
curl -X POST -F "apikey=****" -F "threshold=0.4" \
-F "file=@ki.jpg" \
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

RAYPACK Demographics Detection detects faces and adds demographic to each detected face information. It has a number of possible business applications. You could, for instance, use it to automatically derive demographic information about the customers in your store.


### HTTP Request

POST `https://api.raypack.ai/recog`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | - | Sets the threshold of detection confidence required to return an object as detected.
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
tags | dict |  Contains name and confidence of the detected characteristics as well as the position of the face in the image.
top_row | float |  Top left bounding box corner y-coordinate
left_col | float |  Top left bounding box corner x-coordinate
bottom_row | float |  Bottom right bounding box corner y-coordinate
right_col| float |  Bottom right bounding box corner x-coordinate

## RAYPACK Fashion Detection

> The call below requests the analysis of the image given in file and returns a JSON:  
Here is an example:  
<img src="/images/fashion.jpg">

```shell
curl -X POST -F "apikey=****" -F "threshold=0.4" \
-F "file=@fashion.jpg" \
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

RAYPACK Fashion Detection finds and categorizes clothing items in images. It gives you a comprehensive list of the clothing items in an image providing you with the opportunity to automate processes any process in relation fashion.


### HTTP Request

POST `https://api.raypack.ai/recog`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | - | Sets the threshold of detection confidence required to return an object as detected.
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
tags | dict |  Contains name and confidence of the detected clothing item

## RAYPACK Color Model

> The call below requests the analysis of the image given in file and returns a JSON:  
Here is an example:  

```shell
curl -X POST -F "apikey=****" -F "threshold=0.4" \
-F "file=@fashion.jpg" \
-F "model=9" -F "lang=de" "https://api.raypack.ai/recog"

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
      "modelname":"RaypackVector",
      "modelid":"9",
      "originalfile":"fashion.jpg",
      "starttime":1547194952158,
      "endtime":1547194953348,
      "duration":1.19
    },
    "colors":
    {
      "hex":
      [
        "#834c3d","#05050b","#b9765e","#dbc1b5","#2a1c1e","#a2604c","#5d352b","#cb937e","#6c7e99","#3b4058"
      ],
      "names":
      [
        "sienna","black","indianred","silver","black","sienna","saddlebrown","rosybrown","slategrey","darkslategray"
      ],
      "percent":
      [
        9.91,40.02,10.68,3.27,6.55,13.26,6.37,6.63,1.03,2.28
      ]
    }
  }
}
```

The RAYPACK Color Model analyses the colors that make up an image and returns a hexadecimal value, name and percentage for each. When combined with other models, such as RAYPACK Fashion Detection, it is able to generate insights about the color of detected objects and increases the flexibility and value of your inference.

### HTTP Request

POST `https://api.raypack.ai/recog`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | - | Sets the threshold of detection confidence required to return an object as detected.
file | - | Lets you specify your input file.
url | - | Lets you upload your file from the internet without saving it on your system.
model | - | Indicates which model you want to use. Multi-Object `model=1`, Food `model=2`, Celebrity US `model=3`, Face AI `model=4`, Demographics `model=5` etc.
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
colors | dict |  Contains model results
hex | list | Contains hexadecimal values as strings
names | list | Contains the names of the colors within the image as strings
percent | list | Contains contribution percentage for each color as floats


# RAYPACK Vector-based Embedding

RAYPACK Vector Embedding employs one shot learning logic to rethink the way images are processed with neural networks. Instead of training a network on huge datasets for each  classification purpose we simply compare stored vector representations to each other.
This workflow makes retraining of the model obsolete, because new images can be simply added to the database in which the representations are stored.

Imagine you would want to create an AI model that recognizes sports stars in an vast archive of video material. With traditional models you would have to create large annotated datasets for each star and even retrain the model if you want to add an additional star. With RAYPACK Vector Embedding however you could simply create a database of vector representations and classify new images based on the difference between their representations and the ones stored in your database. This method greatly increases the efficiency of classifications, while still saving money and time. A typical workflow of detecting the identity of a sports star could look like so:

1. Extract the regions of the image containing faces with RAYPACK Face AI.
2. Convert these regions into vector representations using our RAYPACK Vector Embedding.
3. Compare the resulting representations with the representations stored in the database using our vector comparisons.
4. Use the results for your classification needs (i.e. Who is in the image?).

The workflow can be used for almost any classification purpose and is easily scalable. All the calls needed can be found in this documentation. You can use our existing object database or start building your own.

Currently two versions are available:

* 512 Vector Embedding
* 2048 Vector Embedding

## RAYPACK 512 Vector Embedding

> The call below requests the vectorization of the image given in file and returns a JSON.  
Here is an example:  

```shell
curl -X POST -F "apikey=****" -F "threshold=0.4" \
-F "file=@fashion.jpg" \
-F "model=7" -F "lang=de" "https://api.raypack.ai/recog"

```

> The above call returns JSON structured containing the 512 element vector
representation produced by the model.

```json
{
  "name":"Raypack_AI_Filecontainer",
  "version":"1.0",
  "license":"commercial",
  "results":
  {
    "stats":
    {
      "modelname":"RaypackVector",
      "modelid":"7",
      "originalfile":"fashion.jpg",
      "starttime":1546872010419,
      "endtime":1546872010656,
      "duration":0.237
    },
    "vector":
    [
      0.6352465748786926,2.296454429626465,0.3659933805465698,0.09472954273223877,0.20474199950695038,1.5770865678787231,0.31255221366882324,0.9102488160133362,2.3947975635528564, ..., 0.6517073512077332
    ]
  }
}

```
The RAYPACK 512 Vector Embedding returns a vector representation of a given image that can be stored in databases. It reduces the memory space needed to store the images and facilitates operations such as image comparisons. The 512 Vector embedding trades off some detail in the representation for less memory usage compared to the more detailed 2048 Vector Embedding model. However, even a less detailed representations enable highly accurate and fast performance.

### HTTP Request

POST `https://api.raypack.ai/recog`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | - | Sets the threshold of detection confidence required to return an object as detected.
file | - | Lets you specify your input file.
url | - | Lets you upload your file from the internet without saving it on your system.
model | - | Indicates which model you want to use. Multi-Object `model=1`, Food `model=2`, Celebrity US `model=3`, Face AI `model=4`, Demographics `model=5` etc.
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
vector| list |  Contains vector representation of the processed image

## RAYPACK 2048 Vector Embedding

> The call below requests the vectorization of the image given in file and returns a JSON.  
The process is very similar to the 512 Vector Embedding:  

```shell
curl -X POST -F "apikey=****" -F "threshold=0.4" \
-F "file=@fashion.jpg" \
-F "model=8" -F "lang=de" "https://api.raypack.ai/recog"

```
> The above call returns JSON structured containing the 2048 element vector
representation produced by the model.

```json
{
  "name":"Raypack_AI_Filecontainer",
  "version":"1.0",
  "license":"commercial",
  "results":
  {
    "stats":
    {
      "modelname":"RaypackVector",
      "modelid":"8",
      "originalfile":"fashion.jpg",
      "starttime":1546872690402,
      "endtime":1546872691363,
      "duration":0.961
    },
    "vector":
    [
      0.3076409101486206,1.4681082963943481,0.5565540790557861,0.3580729067325592,0.3559722602367401,0.3806714713573456,0.8307628035545349,3.998251438140869,0.17733852565288544, ..., 0.050893161445856094
    ]
  }
}

```
The RAYPACK 2048 Vector Embedding returns a more detailed representation of the given image, compared to the 512 Vector Embedding. It enables highly accurate and fast image operations, while still being more memory efficient than image storage. These aspects make 2048 vector encoding especially interesting for face recognition in large databases and archives.

### HTTP Request

POST `https://api.raypack.ai/recog`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
threshold | - | Sets the threshold of detection confidence required to return an object as detected.
file | - | Lets you specify your input file.
url | - | Lets you upload your file from the internet without saving it on your system.
model | - | Indicates which model you want to use. Multi-Object `model=1`, Food `model=2`, Celebrity US `model=3`, Face AI `model=4`, Demographics `model=5` etc.
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
vector| list |  Contains vector representation of the processed image
