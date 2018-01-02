---
title: POSTIT API DOCUMENTATION

language_tabs: # must be one of https://git.io/vQNgJ
  - json: JSON

toc_footers:
  - <p><a href='https://travis-ci.org/gbengaPS/postit'> <img src='https://travis-ci.org/gbengaPS/postit.svg?branch=develop'/> </a></p>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - groups
  - errors

search: true
---

# Introduction

Welcome to the PostIt API! . PostIt is a group messaging application. It allows you create groups,
add users, and send prioritzed messages to these groups.

Our API allows you do the above mentioned and more.


# Users

## User Signup
> Sample user details:

```json
 {
   "fullName": "test",
   "username": "test_user",
   "email": "test.user@gmail.com",
   "phoneNumber": "09025615565",
   "password": "password"
 }
```

> The above command returns JSON structured like this:

```json
{
    "user": {
        "id": 80,
        "fullName": "test user",
        "username": "test_user",
        "email": "test.user@gmail.com",
        "phoneNumber": "09025615565",
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6ODAsImZ1bGxOYW1lIjoidGVzdCB1c2VyIiwiZW1haWwiOiJ0ZXN0LnVzZXJAZ21haWwuY29tIiwicGhvbmVOdW1iZXIiOiIwOTAyNTYxNTU2NSIsImlhdCI6MTUxMTM0MDg1MSwiZXhwIjoxNTQyODc2ODUxfQ.6L3AIXfU307YRfPkZG4wnYDBZvUWDBWxOrdfkWUtf_o"
    },
    "message": "User test_user was created successfully"
}
```

This endpoint creates a new user account.

`POST http://postit-gbenga.herokuapp.com/api/user/signup`

### HTTP Request

### Body Parameters
<aside class="warning">All fields are required </aside>
Parameter| Description
--------- | -----------
fullName |  Full name of the user.
username|  Username (no special characters aside from an underscore _).
email | User email
phoneNumber | User phone number
password | User password (not less than 6 characters)

### Response
* Status code `201: Created`
* Body `(application/json)`

## User Signin
> Sample registered user details:

```json
  {
    "username":"test_user",
    "password": "password"
  }
```

> The above command returns JSON structured like this:

```json
{
    "user": {
        "id": 80,
        "fullName": "test user",
        "username": "test_user",
        "email": "test.user@gmail.com",
        "phoneNumber": "09025615565",
        "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6ODAsImZ1bGxOYW1lIjoidGVzdCB1c2VyIiwiZW1haWwiOiJ0ZXN0LnVzZXJAZ21haWwuY29tIiwicGhvbmVOdW1iZXIiOiIwOTAyNTYxNTU2NSIsImlhdCI6MTUxMTM0MTM4OCwiZXhwIjoxNTQyODc3Mzg4fQ.uaXCpn4ztgvSxuNvRbj5ZaY2Kaipe2_lah5lQOwk57U"
    }
}
```

This endpoint signs in a registered user.

### HTTP Request

`POST http://postit-gbenga.herokuapp.com/api/user/signin`

### Body Parameters

Parameter | Description
--------- | -----------
username | Username or email of the user
password | User password

### Response
* Status code `200: OK`
* Body `(application/json)`

## Search users

 This endpoint returns users that match the search query

<aside class="warning">
  The `x-access-token` header is needed to access this endpoint
</aside>
`GET http://postit-gbenga.herokuapp.com/api/user/search`

### Query Parameter

Parameter | Description
--------- | -----------
query | The search query
offset | Determines the result offset (integer value)
limit | The number of results per page (default is 10)

Sample query

`http://postit-gbenga.herokuapp.com/api/user/search?query=ade&offset=0&limit=3`

### Response
* Status code `200: OK`
* Body `(application/json)`

> Response

```json
{
    "pageCount": 1,
    "count": 3,
    "users": [
        {
            "id": 4,
            "username": "gbenga_ps",
            "fullName": "Gbenga Elijah Oyetade",
            "email": "ioyetade@gmail.com",
            "phoneNumber": "09025615564"
        },
        {
            "id": 6,
            "username": "python",
            "fullName": "Ade Man",
            "email": "ade@we.com",
            "phoneNumber": "08077567485"
        },
        {
            "id": 16,
            "username": "adebisi",
            "fullName": "Adebisi Gbadebo",
            "email": "gbadebo_adebisi@gmail.com",
            "phoneNumber": "2348064130196"
        }
    ]
}
```

## Password Reset
 This endpoint helps a user update his password

  `POST http://postit-gbenga.herokuapp.com/api/user/password/reset`

>Sample request

```json
{
  "email": "test.user@gmail.com",
}
```
> Response

```json
 {
    "message": "Mail sent successfully"
 }
```

### URL Parameters

  Prameter  | Description
  --------- | ----------
  email     | User email address

### Response
* Status code `200: OK`
* Body `(application/json)`

## Password Update
 This endpoint helps a user update his password

 `POST http://postit-gbenga.herokuapp.com/api/user/password/update?token=usertoken`

 >Sample request

```json
{
  "password": "password",
}
```
> Response

```json
 {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NTUsImZ1bGxOYW1lIjoic2FtIGFkZXllbWkiLCJlbWFpbCI6ImlveWV0YWRlQGdtYWlsLmNvbSIsInBob25lTnVtYmVyIjoiOTExIiwiaWF0IjoxNTExMzUwNDMxLCJleHAiOjE1NDI4ODY0MzF9.vseweDoDgOMjL_PWA6oEf1rZTsIgrFYdyRFffd97Ul4",
    "message": "Password updated successfully"
}
```

### Body Parameters

  Prameter  | Description
  --------- | ----------
  password  | New user password

### Query Parameters

  Prameter  | Description
  --------- | ----------
  token  | token sent to the user's email

### Response
* Status code `200: OK`
* Body `(application/json)`