---
title: POSTIT API DOCUMENTATION

language_tabs: # must be one of https://git.io/vQNgJ
  - json: JSON

toc_footers:
  - <p><a href='https://travis-ci.org/gbengaPS/postit'> <img src='https://travis-ci.org/gbengaPS/postit.svg?branch=develop'/> </a></p>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - groups

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

### Query Parameters
<aside class="warning">All fields are required </aside>
Parameter| Description
--------- | -----------
fullName |  Full name of the user.
username|  Username (no special characters aside from an underscore _).
email | User email
phoneNumber | User phone number
password | User password (not less than 6 characters)

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

### URL Parameters

Parameter | Description
--------- | -----------
username | Username or email of the user
password | User password

## Search users

 This endpoint returns users that match the search query

`GET http://postit-gbenga.herokuapp.com/api/user/search?query=query`

Sample query URL

http://postit-gbenga.herokuapp.com/api/user/search?query=s&offset=0&limit=3

> Response

```json
 {
    "pageCount": 3,
    "count": 9,
    "users": [
        {
            "id": 1,
            "username": "test23",
            "fullName": "Mr test",
            "email": "test23@gmail.com",
            "phoneNumber": "23480641406954"
        },
        {
            "id": 80,
            "username": "test_user",
            "fullName": "test user",
            "email": "test.user@gmail.com",
            "phoneNumber": "09025615565"
        },
        {
            "id": 6,
            "username": "Jason",
            "fullName": "Jason Nelson",
            "email": "jason@gmail.com",
            "phoneNumber": "080641406954"
        }
    ]
}
```

## Password Reset
 This endpoint allows a user request a password reset

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
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6NTUsImZ1bGxOYW1lIjoic2FtIGFkZXllbWkiLCJlbWFpbCI6ImlveWV0YWRlQGdtYWlsLmNvbSIsInBob25lTnVtYmVyIjoiOTExIiwiaWF0IjoxNTExMzUwNDMxLCJleHAiOjE1NDI4ODY0MzF9.vseweDoDgOMjL_PWA6oEf1rZTsIgrFYdyRFffd97Ul4"
}
```

### URL Parameters

  Prameter  | Description
  --------- | ----------
  password  | New user password

