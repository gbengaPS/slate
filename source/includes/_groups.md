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
    "groupId": 1,
    "groupName": "test group name",
    "groupDescription": "test group description"
  }

```
 This endpoint creates a new group

`POST http://postit-gbenga.herokuapp.com/api/group`

### URL Parameters

Parameter | Description
--------- | -----------
groupName | The unique name of the group
groupDescription | The description of the group


## Get user groups
This endpoint gets the group a user belongs to

`GET http://postit-gbenga.herokuapp.com/api/group/user`

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

`GET http://postit-gbenga.herokuapp.com/api/group/:groupId/users`

> Response

```json
{
    "users": [
        {
            "id": 1,
            "username": "test23",
            "fullName": "Mr test",
            "email": "test23@gmail.com",
            "phoneNumber": "23480641406954",
            "groupMembers": {
                "userId": 1,
                "addedBy": 1,
                "groupId": 1,
                "createdAt": "2017-09-06T16:35:02.731Z",
                "updatedAt": "2017-09-06T16:35:02.731Z"
            }
        },
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

### URL Parameter

Parameter | Description
--------- | -----------
userId   | The id of the user to be added

## Leave group
This endpoint removes the user from the group

`DELETE http://postit-gbenga.herokuapp.com/api/group/:groupId/leave`

>Response

```json
  {
    "message": "User left group"
  }
```
## Post message
This endpoint sends a message to a group

`POST http://postit-gbenga.herokuapp.com/api/group/:groupId/message`

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

