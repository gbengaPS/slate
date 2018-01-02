# Groups
<aside class="warning">
  Every request needs the `x-access-token` header.
  The header contains the user token
</aside>

## Create group
> Sample request

```json
  {
    "groupName": "test group name",
    "groupDescription": "test group description",
  }
```
> The above returns

```json
  {
    "group": {
        "groupId": 1,
        "groupName": "test group name",
        "groupDescription": "test group description"
    },
    "message": "Group created successfully"
  }

```
 This endpoint creates a new group

`POST http://postit-gbenga.herokuapp.com/api/group`

### Body Parameters

Parameter | Description
--------- | -----------
groupName | The unique name of the group
groupDescription | The description of the group

### Response
* Status code `201: created`
* Body `(application/json)`

## Get user groups
This endpoint gets the group a user belongs to

`GET http://postit-gbenga.herokuapp.com/api/group/user`

### Response
* Status code `200: OK`
* Body `(application/json)`

>Response

```json
{
    "id": 80,
    "username": "test_user",
    "fullName": "test user",
    "email": "test.user@gmail.com",
    "phoneNumber": "09025615565",
    "groups": [
        {
            "id": 75,
            "groupName": "test group name",
            "groupDescription": "test group description",
            "createdBy": 80,
            "createdAt": "2017-11-22T10:09:18.446Z",
            "updatedAt": "2017-11-22T10:09:18.446Z",
            "messages": []
        },
        {
            "id": 1,
            "groupName": "Postit Default",
            "groupDescription": "Default group for postit users",
            "createdBy": 3,
            "createdAt": "2017-09-10T14:40:30.122Z",
            "updatedAt": "2017-09-10T14:40:30.122Z",
            "messages": [
                {
                    "id": 133,
                    "messageBody": "here\n",
                    "messagePriority": "Normal",
                    "groupId": 1,
                    "userId": 4,
                    "createdAt": "2017-11-20T10:53:03.132Z",
                    "updatedAt": "2017-11-20T10:53:03.132Z"
                }
            ]
        }
    ]
}
```
## Get group members
This endpoint gets the group members from a group provider
current user belongs to the group

### Path Parameter

Parameter | Description
--------- | -----------
groupId | The id of the group to fetch from

`GET http://postit-gbenga.herokuapp.com/api/group/:groupId/users`

### Response
* Status code `200: OK`
* Body `(application/json)`

> Response

```json
{
    "members": [
        {
            "id": 6,
            "username": "python",
            "fullName": "Ade Man",
            "email": "ade@we.com",
            "phoneNumber": "08077567485",
            "groupMembers": {
                "userId": 6,
                "addedBy": 1,
                "groupId": 1,
                "createdAt": "2017-12-11T23:44:42.686Z",
                "updatedAt": "2017-12-11T23:44:42.686Z"
            }
        },
        {
            "id": 7,
            "username": "aliveli",
            "fullName": "ali veli",
            "email": "aliveli@gmail.com",
            "phoneNumber": "905533558787",
            "groupMembers": {
                "userId": 7,
                "addedBy": 1,
                "groupId": 1,
                "createdAt": "2017-12-17T12:28:14.263Z",
                "updatedAt": "2017-12-17T12:28:14.263Z"
            }
        },
        {
            "id": 9,
            "username": "topeooo",
            "fullName": "Temitope Joloko",
            "email": "temitope@gmail.com",
            "phoneNumber": "2348064140695",
            "groupMembers": {
                "userId": 9,
                "addedBy": 1,
                "groupId": 1,
                "createdAt": "2017-12-18T07:59:15.127Z",
                "updatedAt": "2017-12-18T07:59:15.127Z"
            }
        }
    ]
}
```

## Add members
> Sample request

```json
 {
   "userId": 80,
 }
```
> Response

```json
{
    "member": {
        "groupId": 3,
        "userId": 80,
        "addedBy": 80,
        "updatedAt": "2017-11-22T12:23:03.328Z",
        "createdAt": "2017-11-22T12:23:03.328Z",
        "id": 172
    },
    "message": "User successfully added to group"
}
```
This endpoint adds a user to the group

`POST http://postit-gbenga.herokuapp.com/api/group/:groupId/user`

### Body Parameter

Parameter | Description
--------- | -----------
userId   | The id of the user to be added

### Path Parameter

Parameter | Description
--------- | -----------
groupId | The id of the group to add new user to

### Response
* Status code `201: created`
* Body `(application/json)`

## Leave group
This endpoint removes the user from the group

`DELETE http://postit-gbenga.herokuapp.com/api/group/:groupId/leave`

### Path Parameter

Parameter | Description
--------- | -----------
groupId | The id of the group user is to leave

### Response
* Status code `200: OK`
* Body `(application/json)`

>Response

```json
  {
    "message": "User left group"
  }
```
## Post message
This endpoint sends a message to a group

### Body Parameter

Parameter | Description
--------- | -----------
messageBody | The message to be sent
messagePriority | This could be Normal, Urgent or Critical

### Path Parameter

Parameter | Description
--------- | -----------
groupId | The id of the group to post message to

`POST http://postit-gbenga.herokuapp.com/api/group/:groupId/message`

### Response
* Status code `201: created`
* Body `(application/json)`

>Request

```json
{
  "messageBody": "test message",
  "messagePriorty": "Normal",
}
```
>Response

```json
  {
    "message": {
        "messageId": 138,
        "userId": 80,
        "groupId": 3,
        "messageBody": "test message",
        "messagePriority": "Normal"
    }
  }
```

## Get messages

This endpoint gets all the messages sent to a group

`GET http://postit-gbenga.herokuapp.com/api/group/:groupId/messages`

### Path Parameter

Parameter | Description
--------- | -----------
groupId | The id of the group to get messages from

### Response
* Status code `200: OK`
* Body `(application/json)`

>Response

```json
{
    "messages": [
        {
            "id": 139,
            "messageBody": "test message",
            "messagePriority": "Normal",
            "groupId": 75,
            "userId": 80,
            "user": {
                "id": 80,
                "username": "test_user",
                "fullName": "test user",
                "email": "test.user@gmail.com",
                "phoneNumber": "09025615565"
            }
        }
    ]
}
```

