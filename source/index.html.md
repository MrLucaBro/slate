---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

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
curl -X POST -F "apikey=RF00ff22e31"
-F "threshold=0.9" -F "imagef=https://cvdazzle.com/assets/img/look5r-md.jpg" 
-F "mode=json" -F "facemode=default" -F "hex=00ff00" "http://otc.raypack.ai:5000/raypackfacev3"

```


> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint lets you use FACE AI.

### HTTP Request

`http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```


> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

