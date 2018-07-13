---
title: JWL API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  # - <a href='#'>Sign Up for a Developer Keys</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the JWL API! You can use our API to access JWL API endpoints, which can get information on various products in our database.

We have language bindings in JavaScript only! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This example API documentation page was created with [Slate](https://github.com/lord/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Authentication

> To authorize, use this code:

```json
  {
    "x-auth-token": "token"
  }
```

> Make sure to replace `token` with your uniquely generated token.

JWL uses Passport's `facebook-token` authentication process.

Once a user is verified by the Facebook Login process a `x-auth-token` is using JWT is generated and sent.

Here after, the token should be included in the header of each request to gain access to secured routes.

This should look something like this:

`x-auth-token: EAAZAKwmZC5Ki4BAD0fCZAZCyVQZ...`

<aside class="notice">
You must replace <code>token</code> with your personal token.
</aside>

# Users

## GET a Specific User


> RESPONSE:

```json
{
    "DEBUG": "GET user",
    "status": 200,
    "message": "Success: User successfully retrieved",
    "data": {
        "user_id": 1,
        "first_name": "Mark",
        "last_name": "Robins",
        "username": "MarkRobins",
        "email": "MarkRobins@gmail.com",
        "profile_URL": "https://source.unsplash.com/collection/888146/300x300",
        "total_followers": 12,
        "total_following": 1,
        "total_products": 6
    }
}
```

This endpoint retrieves a specific user. 

It will return a users profile along with the number of followers, likes and profile picture.

### HTTP Request

`GET api/v1/users/:user_id`

Example: [GET User Id 1](https://jwl-be-staging.herokuapp.com/api/v1/users/1)

### URL Parameters

Parameter | Description
--------- | -----------
user_id | The id of the user to retrieve

### SCOPES

* *No permission required*


## CREATE a new user

> REQUEST: 

```json
// --------
// HEADER
// --------
{
  "x-auth-token":"token"
}
// --------
// BODY
// --------
{
  "first_name": "John",
  "last_name": "Doe",
  "username": "JohnDoe",
  "email": "JohnDoe@gmail.com",
  "profile_URL":"https://demos.subinsb.com/isl-profile-pic/image/person.png"
}
```

> RESPONSE:

```json
{
    "DEBUG": "POST create new user",
    "status": 200,
    "message": "Success: User successfully created",
    "data": {
    "first_name": "John",
    "last_name": "Doe",
    "username": "JohnDoe",
    "email": "JohnDoe@gmail.com",
    "profile_URL":"https://demos.subinsb.com/isl-profile-pic/image/person.png"
}
```

This endpoint creates a new user.

### HTTP Request

`GET api/v1/users/`

### URL Parameters

* *No parameters required*

### SCOPES

* This endpoint requires an authentication token to access.


## UDPATE a user

> REQUEST: 

```json
// --------
// HEADER
// --------
{
  "x-auth-token":"token"
}
// --------
// BODY
// --------
{
  "first_name": "Jon",
  "last_name": "Snow"
}
```

> RESPONSE:

```json
{
    "DEBUG": "PUT  user 18's header profile page",
    "status": 200,
    "message": "Success: User successfully updated",
    "data": {
        "first_name": "Jon",
        "last_name": "Snow",
        "username": "JonDoe",
        "email": "JohnDoe@gmail.com",
        "profile_URL": "https://demos.subinsb.com/isl-profile-pic/image/person.png"
    }
}
```

This endpoint creates a new user.

### HTTP Request

`GET api/v1/users/`

### URL Parameters

* *No parameters required*

### SCOPES

* This endpoint requires an authentication token to access.

### FIELDS

These fields are available to be updated:

Field | Description
--------- | -----------
first_name | A user's first name
last_name | A user's last name
username | A user's username depending on availability


# Products

## GET a Specific Product

## GET Product list

## CREATE a Product

## UPDATE a Product

## DELETE a Product

# Orders

## GET a Specific Order

## GET Order list

## CREATE a Order

## UPDATE a Order

## DELETE a Order

# Order Statuses

## GET Order Status list

# Categories

## GET Categories list

# Uploads

## CREATE S3 Signed URL 

# Feeds

## GET Feed list

# Images

## GET Images list

# Payments



# [Admin] Authentication

# [Admin] Users

# [Admin] Products

# [Admin] Orders

# [Admin] Order Statuses

# [Admin] Categories

# [Admin] Uploads

# [Admin] Feeds

# [Admin] Images

# [Admin] Payments

