---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Api Archivizer
# Authentication
## Introduction

ApiArchivizer uses JWT Authorization.
ApiArchivizer expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Bearer meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

## Sign in
```shell
curl -X POST \
  http://example.com/users/sign_in \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{"auth": {"email": "admin@example.com", "password": "admin"}}'
```

> The above command returns JSON structured like this:

```json
{
  "jwt": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY1ODk5MTMsInN1YiI6MX0.xp_Z8zU-5IJKZhCdg_q-AKPB9K8kGK-n6-rOQe4V2Yo"
}
```


For sign in need send to API email and password.
Аfter successful requests will receive a token for a JWT authorization

### HTTP Request

`POST http://example.com/users/sign_in`

### Query Parameters

Parameter | Description
--------- | -----------
email | The User's email.
password | The User's passwords.


## Sign up
```shell
curl -X POST \
  http://localhost:3000/users/sign_up \
  -H 'authorization: Basic eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY1OTA4MTMsInN1YiI6MX0.VkPN_SMD_kL1x3UCdFh17aeRWnOQJ86_wQPB-bwnbn8' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{"user": {"email": "user@example.com", "password": "12341234", "name": "User"}}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "data": {
    "id": 2,
    "name": "User",
    "email": "user@example.com",
    "surname": null,
    "deleted_at": null,
    "created_at": "2017-09-27T09:27:22.516Z",
    "updated_at": "2017-09-27T09:27:22.516Z"
  }
}
```


Only authorization users can registrate users.
### HTTP Request

`POST http://example.com/users/sign_up`

### Query Parameters

Parameter | Description
--------- | -----------
name      | The User's name.
email     | The User's email.
password  | The User's passwords.

## Update the user's data
```shell
curl -X PATCH \
  http://localhost:3000/users/current \
  -H 'authorization: Basic eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY1OTA4MTMsInN1YiI6MX0.VkPN_SMD_kL1x3UCdFh17aeRWnOQJ86_wQPB-bwnbn8' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{"user": { "name": "NewUser"}}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "data": {
    "id": 1,
    "name": "NewUser",
    "email": "admin@example.com",
    "surname": null,
    "deleted_at": null,
    "created_at": "2017-09-26T13:33:03.519Z",
    "updated_at": "2017-09-27T09:42:02.896Z"
  }
}
```

For update self info, user must authorization. User can update name, email, password, surname

### HTTP Request

`PATH http://example.com/users/current`

### Query Parameters

Parameter | Description
--------- | -----------
email     | The User's email.
password  | The User's passwords.
name      | The User's name
surname   | The User's surname

## Destroy current user
```shell
curl -X DELETE \
  http://localhost:3000/users/current \
  -H 'authorization: Basic eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY1OTIzNTcsInN1YiI6Mn0.YIeTTV7Ar_Mga1Dg18-8ivO2gCCfXDSsm77pzO0MjgI' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "message": "was destroed"
}
```

This endpoint destroy current user.

### HTTP Request

`DELETE http://example.com/users/current`

## Forgot password
```shell
curl -X POST \
  http://localhost:3000/users/forgot_password \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{"email": "admin@example.com"}'
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

For restore password need to do  this request, if request return succes: true, than system send email with reset token.

### HTTP Request

`POST http://example.com/users/forgot_password`

### Query Parameters

Parameter | Description
--------- | -----------
email     | The User's email.

## Restore password
```shell
curl -X POST \
  http://localhost:3000/users/password \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{"password": "321321321", "password_confirmation": "321321321", "token": "8b446cdc63ce97a20602"}'
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

This endpoint restore password. This request must to do after [forgot password](#forgot-password)
### HTTP Request

`POST http://example.com/users/password`

### Query Parameters

Parameter | Description
--------- | -----------
token     | Token, what received by email.
password  | New password for user
password_confirmation | Confirmation password. password and password_confirmation must match

# Users

In this section for each request user shoul authorize and have permissions for to do action.

## Get users

```shell
curl -X GET \
  http://localhost:3000/users \
  -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY2NzY2NzUsInN1YiI6MX0.XXpyCXXTDBPOMGjGtzBOX0-SuNBx6cqCK66IeWrx8vM' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \

  curl -X GET \
    http://localhost:3000/users \
    -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY2NzY2NzUsInN1YiI6MX0.XXpyCXXTDBPOMGjGtzBOX0-SuNBx6cqCK66IeWrx8vM' \
    -H 'cache-control: no-cache' \
    -H 'content-type: application/json' \
    -d '{"search": { "eq": {"name":"admin"}}}'
```

> The above command returns JSON structured like this:

```json
{
  "data": [
      {
        "id": 1,
        "name": "admin",
        "surname": null,
        "created_at": "2017-09-28T08:18:47.616Z",
        "updated_at": "2017-09-28T08:18:47.616Z",
        "email": "admin@example.com"
      }
  ],
  "meta": {
      "total": 1
  }
}
```
This endpoint for Get and search users. For search need send params with keq 'search'. This key can include eq, lt, gt. And on this keyes need set field and value.

### HTTP Request

`GET http://example.com/users` .

<aside class="success">
Remember — a user must is an authenticated and have permissions!
</aside>

## Create User

```shell
curl -X POST \
  http://localhost:3000/users \
  -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY2NzY2NzUsInN1YiI6MX0.XXpyCXXTDBPOMGjGtzBOX0-SuNBx6cqCK66IeWrx8vM' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{"user": { "email": "test2@example.com", "name": "Test2", "surname": "Testovich", "password":"12341234"}}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "data": {
    "id": 2,
    "name": "Test2",
    "surname": "Testovich",
    "created_at": "2017-09-28T09:38:23.480Z",
    "updated_at": "2017-09-28T09:38:23.480Z",
    "email": "test2@example.com"
  }
}
```


Only authorization and with permissions users can create users.
### HTTP Request

`POST http://example.com/users`

### Query Parameters

Parameter | Description
--------- | -----------
name      | The User's name.
email     | The User's email.
password  | The User's passwords.
surname   | User's surname

## Update User

```shell
curl -X PUT \
  http://localhost:3000/users/2 \
  -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY2NzY2NzUsInN1YiI6MX0.XXpyCXXTDBPOMGjGtzBOX0-SuNBx6cqCK66IeWrx8vM' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{"user": { "name": "Super Test2", "surname": "STestovich"}}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "data": {
    "id": 2,
    "name": "Super Test2",
    "surname": "STestovich",
    "created_at": "2017-09-28T09:38:23.480Z",
    "updated_at": "2017-09-28T09:47:37.133Z",
    "email": "test2@example.com"
  }
}
```

For update self info, user must authorization and have permission. User can update name, email, password, surname

### HTTP Request

`PUT http://example.com/users/:user_id`

### Query Parameters

Parameter | Description
--------- | -----------
email     | The User's email.
password  | The User's passwords.
name      | The User's name
surname   | The User's surname

## Show User

```shell
curl -X GET \
  http://localhost:3000/users/2 \
  -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY2NzY2NzUsInN1YiI6MX0.XXpyCXXTDBPOMGjGtzBOX0-SuNBx6cqCK66IeWrx8vM' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": 2,
    "name": "Super Test2",
    "surname": "STestovich",
    "created_at": "2017-09-28T09:38:23.480Z",
    "updated_at": "2017-09-28T09:47:37.133Z",
    "email": "test2@example.com"
  }
}
```

This endpoint for get user info.

### HTTP Request

`Get http://example.com/users/:user_id`

## User destroy
```shell
curl -X DELETE \
  http://localhost:3000/users/2 \
  -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY2NzY2NzUsInN1YiI6MX0.XXpyCXXTDBPOMGjGtzBOX0-SuNBx6cqCK66IeWrx8vM' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "message": "was destroed"
}
```

This endpoint for destroy user.

### HTTP Request

`DELETE http://example.com/users/:user_id`

# Role

In this section for each request user shoul authorize and have permissions for to do action.

## Index roles

```shell
curl -X GET \
  http://localhost:3000/roles \
  -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY2NzY2NzUsInN1YiI6MX0.XXpyCXXTDBPOMGjGtzBOX0-SuNBx6cqCK66IeWrx8vM' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": 1,
      "name": "admin",
      "surname": null,
      "created_at": "2017-09-28T08:18:47.616Z",
      "updated_at": "2017-09-28T08:18:47.616Z",
      "email": "admin@example.com"
    }
  ],
  "meta": {
      "total": 1
  }
}
```
This endpoint for Get and search roles. For search need send params with keq 'search'. This key can include eq, lt, gt. And on this keyes need set field and value.

### HTTP Request

`GET http://example.com/roles` .

<aside class="success">
Remember — a user must is an authenticated and have permissions!
</aside>

## Create role

```shell
curl -X POST \
  http://localhost:3000/roles \
  -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY2NzY2NzUsInN1YiI6MX0.XXpyCXXTDBPOMGjGtzBOX0-SuNBx6cqCK66IeWrx8vM' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{"role": { "name": "developer"}}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "data": {
    "id": 2,
    "name": "developer",
    "deleted_at": null,
    "permissions_count": null,
    "users_count": null,
    "created_at": "2017-09-28T10:12:42.996Z",
    "updated_at": "2017-09-28T10:12:42.996Z"
  }
}
```


Only authorization and with permissions users can create roles.
### HTTP Request

`POST http://example.com/roles`

### Query Parameters

Parameter | Description
--------- | -----------
name      | Role's name.

## Show role

```shell
curl -X GET \
  http://localhost:3000/roles/1 \
  -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY2NzY2NzUsInN1YiI6MX0.XXpyCXXTDBPOMGjGtzBOX0-SuNBx6cqCK66IeWrx8vM' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{"role": { "name": "manager"}}'
```

> The above command returns JSON structured like this:

```json
{
    "data": {
      "id": 1,
      "name": "admin",
      "permissions": [
        {
            "id": 1,
            "action": "roles_create",
            "description": null,
            "frontend": null,
            "self": null
        },
        {
            "id": 2,
            "action": "roles_index",
            "description": null,
            "frontend": null,
            "self": null
        },
        {
            "id": 3,
            "action": "roles_show",
            "description": null,
            "frontend": null,
            "self": null
        }
      ]
  }
}
```

This endpoint for get role info.

### HTTP Request

`Get http://example.com/roles/:role_id`

## Destroy Role

```shell
curl -X DELETE \
  http://localhost:3000/roles/2 \
  -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY2NzY2NzUsInN1YiI6MX0.XXpyCXXTDBPOMGjGtzBOX0-SuNBx6cqCK66IeWrx8vM' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "message": "was destroed"
}
```

This endpoint for destroy role.

### HTTP Request

`DELETE http://example.com/roles/:role_id`

## Assign role

```shell
curl -X POST \
  http://localhost:3000/roles/assign \
  -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY2NzY2NzUsInN1YiI6MX0.XXpyCXXTDBPOMGjGtzBOX0-SuNBx6cqCK66IeWrx8vM' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{"user_id": 1, "id": 2}'
```

> The above command returns JSON structured like this:

```json
{
    "success": true
}
```


Only authorization and with permissions users can assign roles. This endpoint for assign role to user.
### HTTP Request

`POST http://example.com/roles/assign`

### Query Parameters

Parameter | Description
--------- | -----------
user_id   | ID of the user assigned to the role.
id        | Id of the role assigne to the user.

## Remove role

```shell
curl -X POST \
  http://localhost:3000/roles/remove \
  -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY2NzY2NzUsInN1YiI6MX0.XXpyCXXTDBPOMGjGtzBOX0-SuNBx6cqCK66IeWrx8vM' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{"user_id": 1, "id": 2}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "message": "was destroed"
}
```


Only authorization and with permissions users can remove roles. This endpoint for remove role from user.
### HTTP Request

`POST http://example.com/roles/remove`

### Query Parameters

Parameter | Description
--------- | -----------
user_id   | ID of the user assigned to the role.
id        | Id of the role assigne to the user.

## Remove permission from role

```shell
curl -X DELETE \
  http://localhost:3000/roles/1/remove_permission \
  -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY2NzY2NzUsInN1YiI6MX0.XXpyCXXTDBPOMGjGtzBOX0-SuNBx6cqCK66IeWrx8vM' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{"permission_id": 20}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "message": "was destroed"
}
```


Only authorization and with permissions users can remove permissions from roles. This endpoint for permission from role.
### HTTP Request

`DELETE http://example.com/roles/:role_id/remove_permission`

### Query Parameters

Parameter | Description
--------- | -----------
permission_id   | ID of the perrmission.

# Permissions

## Create permission

```shell
curl -X POST \
  http://localhost:3000/permissions \
  -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY2NzY2NzUsInN1YiI6MX0.XXpyCXXTDBPOMGjGtzBOX0-SuNBx6cqCK66IeWrx8vM' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{"role_id": 2, "permission": {"action": "posts_destroy", "description": "Allow access to destroy posts"}}'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "data": {
    "id": 21,
    "action": "posts_destroy",
    "description": "Allow access to destroy posts",
    "deleted_at": null,
    "frontend": null,
    "self": null,
    "roles_count": 1,
    "created_at": "2017-09-28T12:09:22.837Z",
    "updated_at": "2017-09-28T12:09:22.837Z"
  }
}
```


Only authorization and with permissions "permissions_create" users can create permissions.
### HTTP Request

`POST http://example.com/permissions`

### Query Parameters

Parameter   | Description
---------   | -----------
role_id     | ID of the role to which the permission are added.
action      | Action to which the user get access. Format: "#{controller_name}_#{action_name}"
description | Description for permission
frontend    | Boolean value. Permission used on client part
self        | Boolean value. Allows the action only on his (user_id == id) record

## Index permissions

```shell
curl -X GET \
  http://localhost:3000/permissions \
  -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY2NzY2NzUsInN1YiI6MX0.XXpyCXXTDBPOMGjGtzBOX0-SuNBx6cqCK66IeWrx8vM' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json'
```

> The above command returns JSON structured like this:

```json
{
    "data": [
        {
            "id": 1,
            "action": "roles_create",
            "description": null,
            "deleted_at": null,
            "frontend": null,
            "self": null,
            "roles_count": 1,
            "created_at": "2017-09-28T08:18:47.698Z",
            "updated_at": "2017-09-28T08:18:47.698Z"
        },
        {
            "id": 2,
            "action": "roles_index",
            "description": null,
            "deleted_at": null,
            "frontend": null,
            "self": null,
            "roles_count": 1,
            "created_at": "2017-09-28T08:18:47.711Z",
            "updated_at": "2017-09-28T08:18:47.711Z"
        },
        {
            "id": 3,
            "action": "roles_show",
            "description": null,
            "deleted_at": null,
            "frontend": null,
            "self": null,
            "roles_count": 1,
            "created_at": "2017-09-28T08:18:47.718Z",
            "updated_at": "2017-09-28T08:18:47.718Z"
        }
    ],
    "meta": {
        "total": 21
    }
}
```
This endpoint for Get and search permission. For search need send params with key 'search'. This key can include eq, lt, gt. And on this keyes need set field and value.

### HTTP Request

`GET http://example.com/permissions` .

### Query Parameters

Parameter   | Description
---------   | -----------
role_id     | For get all permissions for this role.
page        | For pagination. Get current page
per_page    | For pagination. Set count objects on request

## Show permission

```shell
curl -X GET \
  http://localhost:3000/permissions/2 \
  -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY2NzY2NzUsInN1YiI6MX0.XXpyCXXTDBPOMGjGtzBOX0-SuNBx6cqCK66IeWrx8vM' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json' \
  -d '{"role_id": 2, "permission": {"action": "posts_destroy", "description": "Allow access to destroy posts"}}'
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": 2,
    "action": "roles_index",
    "description": null,
    "frontend": null,
    "self": null
  }
}
```

This endpoint for get permission info.

### HTTP Request

`Get http://example.com/permission/:permission_id`

## Destroy permission

```shell
curl -X DELETE \
  http://localhost:3000/permissions/2 \
  -H 'authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE1MDY2NzY2NzUsInN1YiI6MX0.XXpyCXXTDBPOMGjGtzBOX0-SuNBx6cqCK66IeWrx8vM' \
  -H 'cache-control: no-cache' \
  -H 'content-type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "status": "success",
  "message": "was destroed"
}
```

This endpoint for destroy permission.

### HTTP Request

`DELETE http://example.com/permissions/:permission_id`
