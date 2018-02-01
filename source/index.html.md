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

# Database Architecture



<aside class="warning">Make sure you read this section carefully!</aside>

The API handles the interaction between 2 databases:

- <code>InsurerData</code>: Contains all the data for the insurer's and the products they offer
- <code>basicUserData</code>: Contains all the data that does not come from other apps (e.g. Username, password, email, address, etc.)
- <code>rawUserData</code>: Contains all the data that comes from other apps and/or sensors (e.g. Walking distance, house temperature, etc.)

The following two tables list the acceptable format for each of these database.

## InsurerData Database

> An example of one row of the "insurerData" DB is provided below:

```json
{
  'insurer_name': "Desjardins",
  'insurer_id': "JWWoMSHXRvD",
  'products': [
                {
                  'product_name': 'Vision Death Insurance',
                  'product_id': "LJcswDRkZPHZWCk8Q",
                  'pricing_method': "linearRegression",
                  'pricing_method_id': "swDRkZPHZWCk",
                  'pricing_method_data': ["is_smoker", "birthday", ...]
                  'monetary_attr': [
                                      {
                                        'attribute_name': "Medical Payments",
                                        'attribute_id': "NJtNRargNcXCx",
                                      }
                                   ]
                  'qualitative_attr': [
                                        {
                                          'attribute_name': "Critical Illness Insurance",
                                          'attribute_id': "gb6ZFZpyGilDd",
                                        }
                                      ],
                }
              ]
}
```

Field | Value| Description
--------- | ------- | -----------
insurer_name | varchar(254) | Insurer's name
insurer_id | varchar(254) | Insurer's unique id
products | JSON | List of all the products for the insurer
product_name | varchar(254) | Product's name
product_id | varchar(254) | Product's id
pricing_method | varchar(254) | Name of the algorithm for the product's pricing
pricing_method_id | varchar(254) | id of the pricing method
pricing_method_data | JSON | List of the variables used for the pricing
monetary_attr | JSON | List of the monetary attributes for this product
qualitative_attr | JSON | List of the qualitative attributes for this product
attribute_name | varchar(50) | Name of the attribute for the product
attribute_id | varchar(50) | id of the attribute


## basicUserData Database

> An example of one row of the "basic data" DB is provided below:

```json
{
  'id': "Ie78jke1ldf9QJ73Cdf23",
  'username': "john@example.com",
  'password': "2Q/pGLJcswuo0JWWoMSHXRvD1",
  'first_name': "John",
  'middle_name': None,
  'last_name': "Doe",
  'birthday': 665350493000,
  'gender': "M",
  'country': "CA",
  'province': "QC",
  'city': "montreal",
  'postal_code': "H1M 3K5",
  'street_name': "example street",
  'house_number': 235,
  'geolocation': None,
  'currency': "CAD",
  'quotes': None,
  'relationships': [
                      {'friend_id': "E7tHV8wSfv7tmczQZ"}
                   ],
  'products': [
                {
                  'product_name': "Vision Death Insurance",
                  'product_id': "LJcswDRkZPHZWCk8Q",
                  'insurer_name': "Desjardins",
                  'insurer_id': "JWWoMSHXRvD",
                  'price': 345.32,
                  'payment_frequency': "monthly",
                  'insureds': [
                                        {
                                          'first_name': "Jr.",
                                          'last_name': "Doe"
                                          'email': "jr@example.com"
                                        }
                                     ],
                  'monetary_attr': [
                                      {
                                        'attribute_name': "Medical Payments",
                                        'attribute_id': "NJtNRargNcXCx",
                                        'covered_amount': 2000.00,
                                      }
                                   ],
                  'qualitative_attr': [
                                        {
                                          'attribute_name': "Critical Illness Insurance",
                                          'attribute_id': "gb6ZFZpyGilDd",
                                          'covered': True
                                        }
                                      ]

                }
              ]
}
```



Field | Value| Description
--------- | ------- | -----------
id | varchar(254) | User's unique id
username | varchar(254) | User's email
password | varchar(254) | User's hashed password
first_name | varchar(50) | User's first name
middle_name | varchar(50) | User's middle name
last_name | varchar(50) | User's last name
birthday | varchar(254) | milliseconds UNIX timestamp
gender | varchar(1) | M or F
country | varchar(2) | Country abbreviation
province | varchar(2) | Province abbreviation
city | varchar(50) | City
postal_code | varchar(50) | Postal code
street_name | varchar(50) | Street name
house_number | varchar(50) | House number
geolocation | varchar(100) | Google Map's geolocation
currency | varchar(10) | Currency used by the user
relationships | JSON | ids of the user's friend using the app
products | JSON | List of all the user's products characteristics
quotes | JSON | List of all the user's quotes characteristics
product_name | varchar(50) | Name of the insurance product
product_id | varchar(50) | id of the insurance product
insurer_name | varchar(50) | Name of the insurer
insurer_id | varchar(50) | id of the insurer
price | real | Price of the product/quote
payment_frequency | varchar(25) | Weekly, monthly, etc.
insureds | JSON | List of the insureds for the product/quote
monetary_attr | JSON | List of the monetary attributes for the product/quote
qualitative_attr | JSON | List of the qualitative attributes for the product/quote


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

# API Endpoints

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

url = 'https:/localhost:5000/api/v1.0/getBasicData/'
payload = {"username":"myUsername", "password":"myPassword",
           "fields": ["field 1", ..., "field n"]}
headers = {'content-type': 'application/json'}

r = requests.get(url, data=json.dumps(payload), headers=headers)
```

```swift

```

```javascript

```

> The above command returns JSON structured like this:

```json
{
    "success": Boolean,
    "data": [
        "field 1": 'value 1',
                ...,
        "field n": 'value n'
    ]
}
```

This endpoint retrieves specific user information in the "basic data" database.

### HTTP Request

`GET https:/localhost:5000/api/v1.0/getBasicData/`

### URL Parameters

Parameter | Description
--------- | -----------
username | Username of the user
password | Password of the user
fields   | Fields of the value you wish to retrieve





## Update Basic User Data

```shell
curl -H "Content-Type: application/json" -X POST -d
  '{"username":"myUsername", "password":"myPassword",
  "fields": ["field 1", "field 2"],
  "values": ["value 1", "value 2"]}'
  http://localhost:5000/api/v1.0/updateBasicData/
```

```python
import requests, json

url = 'https:/localhost:5000/api/v1.0/updateBasicData/'
payload = {"username":"myUsername", "password":"myPassword",
           "fields": ["field 1", ..., "field n"],
           "values": ["value 1", ..., "value n"]}
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
    "success": Boolean,
}
```

This endpoint updates specific user information in the "basic data" database.

### HTTP Request

`POST https:/localhost:5000/api/v1.0/updateBasicData/`

### URL Parameters

Parameter | Description
--------- | -----------
username | Username of the user
password | Password of the user
fields   | Fields of the value you wish to update
values   | Values of the fields





## Update Raw User Data

```shell
curl -H "Content-Type: application/json" -X POST -d
  '{"username":"myUsername", "password":"myPassword",
  "fields": ["field 1", "field 2"],
  "values": ["value 1", "value 2"]}'
  http://localhost:5000/api/v1.0/updateRawData/
```

```python
import requests, json

url = 'https:/localhost:5000/api/v1.0/updateBasicData/'
payload = {"username":"myUsername", "password":"myPassword",
           "fields": ["field 1", ..., "field n"],
           "values": ["value 1", ..., "value n"]}
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
    "success": Boolean,
}
```

This endpoint updates specific user information in the "raw data" database.

### HTTP Request

`POST https:/localhost:5000/api/v1.0/updateRawData/`

### URL Parameters

Parameter | Description
--------- | -----------
username | Username of the user
password | Password of the user
fields   | Fields of the value you wish to update
values   | Values of the fields

