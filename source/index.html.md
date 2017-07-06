---
title: Bucketlist API

language_tabs:
  - shell: cURL

toc_footers:
  - <a href='#'>Github</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

According to Merriam-Webster Dictionary, a Bucket List is a list of things that one has not done before but wants to do before dying.

This API application will serve to enable registered users to post bucket lists, bucket list 
items and keep track of them. A registered user can:

1. Post bucket lists.
2. Delete bucket lists.
3. View all bucketlists with their items.
3. Edit the bucket list names.
4. Add bucketlist items to individual bucketlists.
5. Edit the bucketlist items.
5. Update the ites as 'done' when the user accomplishes them.
    

# Registration

To use the Bucketlist API application, users are required to register with the service.

Registration details required are:

1. **user_email** : The user's email address. It must be made up of a local-part, an @ symbol, 
then a 
case-insensitive domain. Version 2 of will include validation for the domain.
2. **user_password**: This is a string that must be at least 8 digits long, must include an 
uppercase 
letter, lowercase letter and a digit.
3. **confirm_password**: This is a string that must be equal to the **user_password** string.

> The json request is formatted thus:

```shell
curl "/api/v1/auth/register/"
```
```json
[
  {
  "user_email": "dan@gmail.com",
  "user_password": "Qwerty123",
  "confirm_password": "Qwerty123"
  }
]
```
```shell
curl "/api/v1/auth/register/"
```
> On successful registration, the user will receive such a message:

```json
[
  {
    "user_email": "dan@gmail.com",
    "date_registered": "2017-07-06T17:12:53.104342+00:00",
    "id": 1,
    "message": "Registration successful, welcome to Bucketlist"
  }
]
```

If there are any anomalies with the registration, the API request, the returned json will have 
all the details of the error.

For example:

> When a user is already registered, the json response will be:

```json
[
  {
    "message": "Registration Failure. User dan@gmail.com already registered"
  }
]
```

# User Login

This endpoint is for registered users to log into the service, and be able to access their own 
bucketlists(if any) and post new bucketlists and bucketlist items. The required parameters are a 
registered user email and a matching password. 

> The request is formatted as below

```shell
 curl "/api/v1/auth/login/"
```
```json
[
  {
  "user_email": "dan@gmail.com",
  "user_password": "Qwerty123"
  }
]
```

> The above command returns JSON structured like this:

```json
[
{
    "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE0OTkzNTQ2MzAsImlhdCI6MTQ5OTM1MTYzMCwic3ViIjo4fQ.9neRwXsHZP6D0XnAlrpGgFpvbLuyveSqT9kCZCuHa-8",
    "message": "Login successful"
}
]
```

The `access_token` value will be used in subsequent request headers for token authentication 
purposes.


> When the email provided is not registered, the API will return a JSON with the appropriate error 
message and status_code.

```json
[
    {
        "message": "User dans@gmail.com does not exist. Register to access the service"
    }
]
```
# Bucketlist manipulations
 
This endpoint is for a logged in user to post, and view existing bucketlists.

## POST
`POST http://127.0.0.1:5000/api/v1/bucketlists/`

This operation enables a user to post a new bucketlist

### Post Parameters
Parameter | Default | Description
--------- | ------- | -----------
name | None | Name of the bucketlist.

> The request JSON is formatted as below

```json
[
{
  "name": "Travel The World",
  "Authorization": "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE0OTkzNTQ2MzAsImlhdCI6MTQ5OTM1MTYzMCwic3ViIjo4fQ.9neRwXsHZP6D0XnAlrpGgFpvbLuyveSqT9kCZCuHa-8",

}
]
```

> The return JSON is as below:

 ```json
[
{
    "date_created": "2017-06-25 10:26:29",
    "date_modified": "2017-06-28 07:45:02",
    "id": 1,
    "name": "Travel the world",
    "owner_id": 8
}
]
```

## GET

`GET http://127.0.0.1:5000/api/v1/bucketlists/?q=free&limit=40`

This command will get a users buckelists

### Get Parameters


### Post Parameters
Parameter | Default | Description
--------- | ------- | -----------
q | '' | Query string.
limit | 20 | Pagination limit of results per page

> A GET operation without any parameters is shwon below

`GET http://127.0.0.1:5000/api/v1/bucketlists`

> The response JSON will be the list of all bucketlists belonging to the user.

```json
[
    {
        "date_created": "2017-07-06 18:47:34",
        "date_modified": "2017-07-06 18:47:34",
        "id": 1,
        "items": [],
        "name": "Travel the world",
        "owner_id": 8
    }
]
```

> A search parameter that has no hits will return the JSON below

`GET http://127.0.0.1:5000/api/v1/bucketlists/?q=food`

```json
[
{
    "message": "No bucketlists with provided search parameter"
}
]
```
## Single Bucketlist Operations

### GET
### PUT
### DELETE

## Bucketlist Items Manipulation
### POST

## Bucketlist Item Operations
### PUT
### DELETE

