---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - swift
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Koïos Smart Insurance API! You can use our API to access the smart insurance app API endpoints, which
provides information about our users and let's you push data to our servers.

We have language bindings in Shell, Python, Swift and Javascript! You can view code examples in the dark area to the right, and you
can switch the programming language of the examples with the tabs in the top right.


# Authentication

> Each requests to the server needs to be authenticated by the username and password of the user:

```shell
curl -H "Content-Type: application/json" -X POST
  -d '{"username":"myUsername", "password":"myPassword"}'
  http://localhost:5000/api/v1.0/verifyUser/
```

```python
import requests, json

url = 'https:/localhost:5000/api/v1.0/verifyUser/'
payload = {'username': 'myUsername', 'password': 'myPassword'}
headers = {'content-type': 'application/json'}

r = requests.post(url, data=json.dumps(payload), headers=headers)
```

```swift

```

```javascript

```

> Make sure to replace `username` and `password` with the user's credentials.

This API uses the <code>username</code> and <code>password</code> to authenticate each requests to the server.

Each requests are expected to contain a JSON body with the user's credentials that looks like this:

`{'username': 'myUsername', 'password': 'myPassword'}`

<aside class="notice">
Make sure to include the <code>username</code> and <code>password</code> in the JSON body of all your requests to the server.
</aside>

# Basic Data

## Create New User

```shell
curl -H "Content-Type: application/json" -X POST -d
  '{"username":"myUsername", "password":"myPassword"}'
  http://localhost:5000/api/v1.0/newUser/
```

```python
import requests, json

url = 'https:/localhost:5000/api/v1.0/newUser/'
payload = {"username":"myUsername", "password":"myPassword"}
headers = {'content-type': 'application/json'}

r = requests.post(url, data=json.dumps(payload), headers=headers)
```

```swift

```

```javascript

```

> The above command returns JSON structured like this:

```json
{
  "success": Boolean
}
```

This endpoint creates a new user.

### HTTP Request

`POST https:/localhost:5000/api/v1.0/newUser/`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
username | None | Username of the user to create
password | None | Password of the user to create

<aside class="warning">
The username and the password must respect the database guidelines.
</aside>

## Get Basic User Data

```shell
curl -H "Content-Type: application/json" -X GET -d
  '{"username":"myUsername", "password":"myPassword",
  "fields": ["field 1", "field 2"]}'
  http://localhost:5000/api/v1.0/getBasicData/
```

```python
import requests, json

url = 'https:/localhost:5000/api/v1.0/newUser/'
payload = {"username":"myUsername", "password":"myPassword"}
headers = {'content-type': 'application/json'}

r = requests.post(url, data=json.dumps(payload), headers=headers)
```

```swift

```

```javascript

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

<aside class="success">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

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

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
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


