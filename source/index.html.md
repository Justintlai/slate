---
title: Minto API Reference

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

Welcome to the Minto API! You can use our API to access Minto API endpoints, which can get information on various data sets in our database.

We have language bindings in JavaScript only! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```json
//Header
  {
    "x-auth-token": "token"
  }
```

> Make sure to replace `token` with your uniquely generated token.

Minto uses Passport's `facebook-token` and email and password as part of the authentication process.

Once a user is verified by the Facebook Login process a `x-auth-token` is using JWT is generated and sent.

Here after, the token should be included in the header of each request to gain access to secured routes.

This should look something like this:

`x-auth-token: EAAZAKwmZC5Ki4BAD0fCZAZCyVQZ...`

<aside class="notice">
You must replace <code>token</code> with your personal token.
</aside>


## Manual Email login

> REQUEST: 

```json
{
	"username": "johndoe",
	"email":"john.doe@hotmail.co.uk",
	"password":"password"
}
```

> RESPONSE:

```json
{
    "user": {
        "id": 2,
        "first_name": "John",
        "last_name": "Doe",
        "username": "johndoe",
        "email": "johndoe@hotmail.co.uk",
        "profile_URL": "https://demos.subinsb.com/isl-profile-pic/image/person.png",
        "national_id_URL": null,
        "bank_sort_code": null,
        "bank_account_number": null,
        "story": null,
        "email_verified_YN": false,
        "admin_YN": false,
        "seller_YN": false
    },
    "message": "Success: Login successful",
    "success": true
}
```

This endpoint will log an existing user into the application. The user can login with either email or username.

### HTTP Request

`POST api/v1/auth/login`

### URL Parameters

* *No parameters required*

### SCOPES

* *This endpoint requires Facebook Login to Authenticate*

<!---
======================================================================================================================================
-->


## Facebook login

> REQUEST: 
// Header
```json
{
	"Authorization": "Beaer EALCNsjwwwLNSWisikwFal..."
}
```

> RESPONSE:

```json
{
    "user": {
        "id": 9,
        "first_name": "Justin",
        "last_name": "Lai",
        "email": "just_in_88@hotmail.com",
        "profile_URL": "https://graph.facebook.com/v2.6/10156690772858296/picture?type=large",
        "email_verified_YN": false,
        "admin_YN": false,
        "seller_YN": false
    },
    "message": "Success: Login successful",
    "success": true
}
```

This endpoint will log a Facebook user automatically based on their Facebook Login Credentials

### HTTP Request

`POST api/v1/auth/facebook`

### URL Parameters

* *No parameters required*

### SCOPES

* *This endpoint requires Facebook Login to Authenticate*

<!---
======================================================================================================================================
-->


# Users

<!---
======================================================================================================================================
-->
## CREATE a new user

> REQUEST: 

```json
{
  "first_name": "John",
  "last_name": "Doe",
  "username": "johndoe",
  "email": "johndoe@hotmail.co.uk",
  "password": "password",
  "profile_URL":"https://demos.subinsb.com/isl-profile-pic/image/person.png"
}
```

> RESPONSE:

```json
{
    "user": {
        "id": 10,
        "first_name": "John",
        "last_name": "Doe",
        "username": "johndoe",
        "email": "johndoe@hotmail.co.uk",
        "profile_URL": "https://demos.subinsb.com/isl-profile-pic/image/person.png",
        "national_id_URL": null,
        "bank_sort_code": null,
        "bank_account_number": null,
        "story": null,
        "email_verified_YN": false,
        "admin_YN": false,
        "seller_YN": false
    },
    "message": "Success: Login successful",
    "email": true,
    "success": true
}
```

This endpoint will execute the following events:
    - Create a new user
    - Send an email verification email.
    - Automatically login the user (Auth token is sent)

### HTTP Request

`POST api/v1/users`

### URL Parameters

* *No parameters required*

### SCOPES

* *This endpoint requires Facebook Login to Authenticate*

<!---
======================================================================================================================================
-->

## READ a Specific User


> RESPONSE:

```json
{
    "user": {
        "id": 4,
        "first_name": "John",
        "last_name": "Doe",
        "username": "johndoe",
        "profile_URL": "https://demos.subinsb.com/isl-profile-pic/image/person.png",
        "story": null,
        "total_followers": 240,
        "total_following": 256,
        "total_products": 155,
        "addresses": []
    },
    "message": "Success: User successfully created",
    "success": true
}
```

This endpoint retrieves a specific user. 

It will return a users profile along with the number of followers, likes and profile picture.

### HTTP Request

`GET api/v1/users/:user_id`

Example: [GET User Id 1](https://api-dev.minto.app/api/v1/users/1)

### URL Parameters

Parameter | Description
--------- | -----------
user_id | The id of the user to retrieve

### SCOPES

* *No permission required*


<!---
======================================================================================================================================
-->
## READ a list of all users


> RESPONSE:

```json
{
    "users": [
        {
            "id": 1,
            "first_name": "Anna",
            "last_name": "Doe",
            "username": "annadoe",
            "profile_URL": "https://demos.subinsb.com/isl-profile-pic/image/person.png",
            "story": null,
            "total_followers": 23,
            "total_following": 51,
            "total_products": 66,
            "addresses": []
        },
        {
            "id": 2,
            "first_name": "John",
            "last_name": "Doe",
            "username": "johndoe",
            "profile_URL": "https://demos.subinsb.com/isl-profile-pic/image/person.png",
            "story": null,
            "total_followers": 36,
            "total_following": 77,
            "total_products": 6,
            "addresses": []
        }
    ]
}
```

This endpoint retrieves a list of all users. 

You can optionally add parameters to further define your output but defaults are applied if nothing is supplied.

### HTTP Request

`GET api/v1/users/`

Example: [GET User All](https://jwl-be-staging.herokuapp.com/api/v1/users)

`GET api/v1/users?page=1&limit=20`

Example: [GET User All](https://jwl-be-staging.herokuapp.com/api/v1/users?page=1&limit=20)

<aside class="notice">
This is an <strong>ADMIN</strong> Route. You must have administrator rights to perform this action.
</aside>

### URL Query

Parameter | Description | required?
--------- | ----------- | ------------
page | set the page number to retrieve | optional (default to 1)
limit | set the size of the page limit | optional (default to 15)

### SCOPES

* This endpoint requires an admin authorisation token to access.

### FIELDS

These fields are available to be updated:

Field | Description
--------- | -----------
first_name | First name extracted from a users facebook account
last_name | Last name extracted from a users facebook account
username | User selected username depending on availability (unqiue)
email | The email address linked to their facebook account
password | The user's password details
profile_URL | By default from a user's facebook account
national_id_URL | Uploaded by a user to become an approved seller
email_verified_YN | Determined email verification
seller_YN | Determine whether a user is a seller
disabled_YN | Determine whether an account is disabled/suspended
admin_YN | Determine whether a user has admin rights
total_followers | The number of followers a user has
total_following | The number of people following this user
total_products | The number of products a user has uploaded

<!---
======================================================================================================================================
-->


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
  "first_name": "Bob",
  "last_name": "Builder"
}
```

> RESPONSE:

```json
{
    "user": {
        "id": 2,
        "first_name": "Bob",
        "last_name": "Builder",
        "username": "johndoe",
        "email": "johndoe@hotmail.co.uk",
        "profile_URL": "https://demos.subinsb.com/isl-profile-pic/image/person.png",
        "national_id_URL": null,
        "bank_sort_code": null,
        "bank_account_number": null,
        "story": null,
        "email_verified_YN": false,
        "admin_YN": false,
        "seller_YN": false
    },
    "message": "Success: User successfully updated",
    "success": true
}
```

This endpoint updates a user's personal details. It can also be used to update a user's password.
However, it will not update protected parameters such as `seller_YN` unless you have ADMIN rights.

### HTTP Request

`UPDATE api/v1/users/`

### URL Parameters

* *No parameters required*

### SCOPES

* This endpoint requires an authentication token to access.

### FIELDS

These fields are available to be updated:

Field | Description | Permission
--------- | ----------- | ---------
first_name | First name extracted from a users facebook account | loggedIn
last_name | Last name extracted from a users facebook account |  loggedIn
username | User selected username depending on availability (unqiue) | loggedIn
profile_URL | By default from a user's facebook account | loggedIn
national_id_URL | Uploaded by a user to become an approved seller | loggedIn
email_verified_YN | Determined email verification | admin
seller_YN | Determine whether a user is a seller | admin
disabled_YN | Determine whether an account is disabled/suspended | admin
admin_YN | Determine whether a user has admin rights | admin 


<!---
======================================================================================================================================
-->


## DELETE a user

> REQUEST: 

```json
// --------
// HEADER
// --------
{
  "x-auth-token":"token"
}
```

> RESPONSE:

```json
{
    "user": {
        "id": 3,
        "first_name": "John",
        "last_name": "Doe",
        "username": "johndoe",
        "email": "johndoe@hotmail.co.uk",
        "password": "$2a$08$nx1pby98iZ//Vj.jpSoj.urj1w5k/rmjQKxuzfLINSPjgwkHq7Wu2",
        "bank_sort_code": null,
        "bank_account_number": null,
        "story": null,
        "fb_id": null,
        "fb_token": null,
        "email_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImJiYkBob3RtYWlsLmNvLnVrIiwiaWF0IjoxNTM5ODU5OTYyLCJleHAiOjE1Mzk5NDYzNjJ9.-_dOJFufpvIlMA9ahvXiLs-e8aawg5siNyqnNUkZoL8",
        "stripe_customer_id": null,
        "profile_URL": "https://demos.subinsb.com/isl-profile-pic/image/person.png",
        "national_id_URL": null,
        "email_verified_YN": false,
        "seller_YN": false,
        "disabled_YN": false,
        "admin_YN": true,
        "deleted_YN": false,
        "created_at": "2018-10-18T10:52:42.000Z",
        "updated_at": "2018-10-18T10:52:42.000Z"
    },
    "message": "Success: User successfully updated",
    "success": true
}
```

This endpoint deletes a user completely from the database. 
It should remove any trace of a user.


### HTTP Request

`DELETE api/v1/users/`

<aside class="notice">
This is an <strong>ADMIN</strong> Route. You must have administrator rights to perform this action.
</aside>

### URL Parameters

* *No parameters required*

### SCOPES

* This endpoint requires an authentication token to access.

<!---
======================================================================================================================================
-->


## CHECK username


> RESPONSE:

```json
{
    "available": true,
    "message": "Success: Username is available",
    "success": true
}
```

This endpoint will verify username availability.

### HTTP Request

`GET api/v1/users/username_availability/:username`

Example: [GET User Id 1](https://api-dev.minto.app/api/v1/users/username_availability/isthisavailable)

### URL Parameters

Parameter | Description
--------- | -----------
username | The username to be checked

### SCOPES

* *No permission required*


<!---
======================================================================================================================================
-->


## RESEND email


> RESPONSE:

```json
{
    "email": true,
    "success": true
}
```

This endpoint will resend an email to a user to enable them to verify their account.

### HTTP Request

`GET api/v1/users/resend_verify_email/:token`

Example: [GET User Id 1](https://api-dev.minto.app/api/v1/users/resend_verify_email/token)

### URL Parameters

Parameter | Description
--------- | -----------
token | This should receive a `JWT` token to enable verification of the user's email.

### SCOPES

* *No permission required*


<!---
======================================================================================================================================
-->


## VERIFY email


> RESPONSE:

```json
{
    "verified": true,
    "success": true
}
```

This endpoint will verify a user's email via the token submitted.

### HTTP Request

`GET api/v1/users/verify_email/:token`

### URL Parameters

Parameter | Description
--------- | -----------
token | This should receive a `JWT` token to enable verification of the user's email.

### SCOPES

* *No permission required*


<!---
======================================================================================================================================
-->


## READ current

> REQUEST: 

```json
// --------
// HEADER
// --------
{
  "x-auth-token":"token"
}
```

> RESPONSE:

```json
{
    "user": {
        "id": 8,
        "first_name": "John",
        "last_name": "Doe",
        "username": "johndoe",
        "profile_URL": "https://demos.subinsb.com/isl-profile-pic/image/person.png",
        "story": null,
        "total_followers": 0,
        "total_following": 0,
        "total_products": 0,
        "addresses": []
    },
    "message": "Success: User successfully created",
    "success": true
}
```

This endpoint will get the current logged in user's profile information

### HTTP Request

`GET api/v1/users/current`

### URL Parameters

Parameter | Description
--------- | -----------
token | This should receive a `JWT` token to enable verification of the user's email.

### SCOPES

* *No permission required*


<!---
======================================================================================================================================
-->

# Followers

<!---
======================================================================================================================================
-->
## CREATE a new follower

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
  "following_id": 6,
}
```

> RESPONSE:

```json
{
    "follow": {
        "id": 5,
        "follower_id": 10,
        "following_id": 6,
        "follow_date": "2018-10-19T08:29:02.000Z"
    },
    "message": "Success: Follower successfully created",
    "success": true
}
```

This endpoint creates a new follower for the user logged in.

### HTTP Request

`POST api/v1/follows`

### URL Parameters

* *No parameters required*

### SCOPES

* *This endpoint requires Facebook Login to Authenticate*

<!---
======================================================================================================================================
-->
## READ a list of following

> REQUEST: 

```json
// --------
// HEADER
// --------
{
  "x-auth-token":"token"
}
```

> RESPONSE:

```json
{
    "following": {
        "count": 2,
        "rows": [
            {
                "id": 3,
                "follower_id": 8,
                "following_id": 7,
                "follow_date": "2018-10-19T07:59:56.000Z",
                "following": {
                    "id": 7,
                    "first_name": "John",
                    "last_name": "Doe",
                    "username": "johndoe",
                    "profile_URL": "https://demos.subinsb.com/isl-profile-pic/image/person.png",
                    "story": null
                }
            },
            {
                "id": 2,
                "follower_id": 8,
                "following_id": 6,
                "follow_date": "2018-10-19T07:59:52.000Z",
                "following": {
                    "id": 6,
                    "first_name": "Anna",
                    "last_name": "Doe",
                    "username": "annadoe",
                    "profile_URL": "https://demos.subinsb.com/isl-profile-pic/image/person.png",
                    "story": null
                }
            }
        ]
    },
    "message": "Success: Followers successfully retrieved",
    "success": true
}
```

This endpoint retrieves a the logged in users's following list. A list of who they are following

It will return a users profile along with the number of following and profile picture.

### HTTP Request

`GET api/v1/follows/following`

`GET api/v1/follows/following?page=1&limit=20`

### URL Query

Parameter | Description | required?
--------- | ----------- | ------------
page | set the page number to retrieve | optional (default to 1)
limit | set the size of the page limit | optional (default to 15)

### SCOPES

* *This endpoint requires Facebook Login to Authenticate*


<!---
======================================================================================================================================
-->
## READ a list of followers

> REQUEST: 

```json
// --------
// HEADER
// --------
{
  "x-auth-token":"token"
}
```

> RESPONSE:

```json
{
    "following": {
        "count": 1,
        "rows": [
            {
                "id": 4,
                "follower_id": 10,
                "following_id": 8,
                "follow_date": "2018-10-19T08:02:21.000Z",
                "follower": {
                    "id": 10,
                    "first_name": "Bob",
                    "last_name": "Builder",
                    "username": "bobthebuilder",
                    "profile_URL": "https://demos.subinsb.com/isl-profile-pic/image/person.png",
                    "story": null
                }
            }
        ]
    },
    "message": "Success: Followers successfully retrieved",
    "success": true
}
```

This endpoint retrieves a list of all follower for the user logged in. 

You can optionally add parameters to further define your output but defaults are applied if nothing is supplied.

### HTTP Request

`GET api/v1/follows/followers`

`GET api/v1/follows/followers?page=1&limit=20`

### URL Query

Parameter | Description | required?
--------- | ----------- | ------------
page | set the page number to retrieve | optional (default to 1)
limit | set the size of the page limit | optional (default to 15)

### SCOPES

* *This endpoint requires Facebook Login to Authenticate*


<!---
======================================================================================================================================
-->

## DELETE a follower

> REQUEST: 

```json
// --------
// HEADER
// --------
{
  "x-auth-token":"token"
}
```

> RESPONSE:

```json
{
    "follow": {
        "id": 4,
        "follower_id": 10,
        "following_id": 8,
        "follow_date": "2018-10-19T08:02:21.000Z",
        "created_at": "2018-10-19T08:02:21.000Z",
        "updated_at": "2018-10-19T08:02:21.000Z",
        "user_id": null
    },
    "message": "Success: Follower successfully deleted",
    "success": true
}
```

This endpoint deletes a follower from the logged in user's follower list. 

### HTTP Request

`DELETE api/v1/follows/:following_id`

### URL Parameters

Parameter | Description
--------- | -----------
following_id | The id of the user to unfollow

### SCOPES

* *This endpoint requires Facebook Login to Authenticate*



<!---
======================================================================================================================================
-->


# Addresses

<!---
======================================================================================================================================
-->


## CREATE an Address

> REQUEST: 

```json
{
    "address_type": "delivery",    (delivery or billing ONLY)
    "address_name": "Shoreditch Home",
    "address1": "Flat 5",
    "address2": "176 Shoreditch High Street",
    "city": "London",
    "postcode": "E1 6AX",
    "country": "United Kingdom",
    "country_code": "UK",
    "primary_YN": true
}
```

> RESPONSE:

```json
{
    "address": {
        "id": 1,
        "user_id": 10,
        "address_type": "delivery",
        "address_name": "Shoreditch Home",
        "address1": "Flat 5",
        "address2": "176 Shoreditch High Street",
        "city": "London",
        "postcode": "E1 6AX",
        "country": "United Kingdom",
        "country_code": "GB",
        "primary_YN": true
    },
    "message": "Success: Address successfully created",
    "success": true
}
```

This endpoint creates a new address.

### HTTP Request

`POST api/v1/addresses`

### URL Parameters

* *No parameters required*

### SCOPES

* *This endpoint requires an authentication token to access.*


<!---
======================================================================================================================================
-->


## GET an Address for an User

> RESPONSE:

```json
{
    "address": {
        "id": 1,
        "user_id": 10,
        "address_type": "delivery",
        "address_name": "Shoreditch Home",
        "address1": "Flat 5",
        "address2": "176 Shoreditch High Street",
        "address3": null,
        "address4": null,
        "city": "London",
        "county": null,
        "postcode": "E1 6AX",
        "country": "United Kingdom",
        "country_code": "GB",
        "primary_YN": true,
        "created_at": "2018-10-19T09:29:40.000Z",
        "updated_at": "2018-10-19T09:29:40.000Z"
    },
    "message": "Success: Address successfully retrieved",
    "success": true
}
```

This endpoint retrieves a list of addresses for user specified. 

### HTTP Request

`GET api/v1/addresses/:user_id`

### URL Parameters

Parameter | Description
--------- | -----------
user_id | The id of the user's address to retrieve

### SCOPES

* *This endpoint requires an authentication token to access.*

<!---
======================================================================================================================================
-->

## GET Address list

> REQUEST: 

```json
// --------
// HEADER
// --------
{
  "x-auth-token":"token"
}
```

> RESPONSE:

```json
{
    "address": {
        "count": 2,
        "rows": [
            {
                "id": 1,
                "user_id": 10,
                "address_type": "delivery",
                "address_name": "Shoreditch Home",
                "address1": "Flat 5",
                "address2": "176 Shoreditch High Street",
                "address3": null,
                "address4": null,
                "city": "London",
                "county": null,
                "postcode": "E1 6AX",
                "country": "United Kingdom",
                "country_code": "GB",
                "primary_YN": true,
                "created_at": "2018-10-19T09:29:40.000Z",
                "updated_at": "2018-10-19T09:29:40.000Z"
            },
            {
                "id": 2,
                "user_id": 10,
                "address_type": "billing",
                "address_name": "Shoreditch Home",
                "address1": "Flat 5",
                "address2": "176 Shoreditch High Street",
                "address3": null,
                "address4": null,
                "city": "London",
                "county": null,
                "postcode": "E1 6AX",
                "country": "United Kingdom",
                "country_code": "GB",
                "primary_YN": true,
                "created_at": "2018-10-19T09:30:09.000Z",
                "updated_at": "2018-10-19T09:30:09.000Z"
            }
        ]
    },
    "message": "Success: Address successfully retrieved",
    "success": true
}
```

This endpoint retrieves a list of all addresses for the logged in user. 

### HTTP Request

`GET api/v1/addresses`

`GET api/v1/addresses/?page=1&limit=20`

### URL Query

Parameter | Description | required?
--------- | ----------- | ------------
page | set the page number to retrieve | optional (default to 1)
limit | set the size of the page limit | optional (default to 15)

### SCOPES

* *You must be logged in to access this endpoint*


<!---
======================================================================================================================================
-->

## UPDATE an Address

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
    "address_type": "delivery",
    "address_name": "Shoreditch Home",
    "address1": "Flat 5",
    "address2": "176 Shoreditch High Street",
    "city": "London",
    "postcode": "E1 6AX",
    "country": "United Kingdom",
    "country_code": "GB",
    "primary_YN": true,
}
```

> RESPONSE:

```json
{
    "address": {
        "id": 2,
        "user_id": 10,
        "address_type": "billing",
        "address_name": "New Name",
        "address1": "Flat 5",
        "address2": "176 Shoreditch High Street",
        "address3": null,
        "address4": null,
        "city": "London",
        "county": null,
        "postcode": "E1 6AX",
        "country": "United Kingdom",
        "country_code": "GB",
        "primary_YN": true
    },
    "message": "Success: Address successfully updated",
    "success": true
}
```

This endpoint update an address.

For country codes see: https://www.nationsonline.org/oneworld/country_code_list.htm

### HTTP Request

`UPDATE api/v1/addresses/:address_id`

### URL Parameters

Parameter | Description
--------- | -----------
address_id | The id of the address to be deleted

### SCOPES

* This endpoint requires an authentication token to access.

### FIELDS

These fields are available to be updated:

Field | Description | Permission
--------- | ----------- | ---------
address_type | billing or delivery | loggedIn
address_name | the name of the address given by user |  loggedIn
address1 | first line of address | loggedIn
address2 |  second line of address | loggedIn
address3 | third line of address | loggedIn
address4 | fourth line of address | loggedIn
city | city |  loggedIn
county | county see above list of names of countries | loggedIn
postcode |  postcode area | loggedIn
country |  name of the country | loggedIn
country_code | country code - 2 characters (see above for list) | loggedIn
primary_YN | description of the product |  loggedIn

<!---
======================================================================================================================================
-->

## DELETE an Address


> REQUEST: 

```json
// --------
// HEADER
// --------
{
  "x-auth-token":"token"
}

```

> RESPONSE:

```json
{
    "address": {
        "id": 2,
        "user_id": 10,
        "address_type": "billing",
        "address_name": "New Name",
        "address1": "Flat 5",
        "address2": "176 Shoreditch High Street",
        "address3": null,
        "address4": null,
        "city": "London",
        "county": null,
        "postcode": "E1 6AX",
        "country": "United Kingdom",
        "country_code": "GB",
        "primary_YN": true,
        "created_at": "2018-10-19T09:30:09.000Z",
        "updated_at": "2018-10-19T09:31:56.000Z"
    },
    "message": "Success: Address successfully deleted",
    "success": true
}
```

This endpoint deletes an address. 

### HTTP Request

`DELETE api/v1/adresses/:address_id`


### URL Parameters

Parameter | Description
--------- | -----------
address_id | The id of the address to be deleted

### SCOPES

* This endpoint requires an authentication token to access.



<!---
======================================================================================================================================
-->


# Products

<!---
======================================================================================================================================
-->


## CREATE a Product

> REQUEST: 

```json
{
  "category_id":2,
  "description":"Kate Spade New Flying Colours Pave Dash Earrings",
  "price": 45,
  "currency_id": "GBP",
  "images": [{
    "image_URL": "https://twicely.shop/pub/media/wysiwyg/jewellery-9.jpg",
     "image_description": "This is the image"
  },{
    "image_URL": "https://another image.jpg",
     "image_description": "This is the image 2"
  }]
}
```

> RESPONSE:

```json
{
    "product": {
        "id": 15,
        "category_id": 2,
        "user_id": 10,
        "entry_date": "2018-10-19T14:03:19.000Z",
        "description": "Kate Spade New Flying Colours Pave Dash Earrings",
        "price": 45,
        "currency_id": "GBP",
        "User": {
            "id": 10,
            "first_name": "John",
            "last_name": "Doe",
            "username": "johndoe",
            "profile_URL": "https://demos.subinsb.com/isl-profile-pic/image/person.png",
            "story": null
        },
        "images": [
            {
                "id": 29,
                "image_URL": "https://twicely.shop/pub/media/wysiwyg/jewellery-9.jpg",
                "image_description": "This is the image",
                "image_date": "2018-10-19T14:03:19.000Z"
            },
            {
                "id": 30,
                "image_URL": "https://another image.jpg",
                "image_description": "This is the image 2",
                "image_date": "2018-10-19T14:03:19.000Z"
            }
        ]
    },
    "message": "Success: Product successfully created",
    "success": true
}
```

This endpoint creates a new product.

### HTTP Request

`POST api/v1/products`

### URL Parameters

* *No parameters required*

### SCOPES

* *This endpoint requires an authentication token to access.*

### FIELDS

These fields are available to use:

Field | Description | Permission
--------- | ----------- | ---------
category_id | the type of product | loggedIn
description | describe the product |  loggedIn
price | cost for the product | loggedIn
currency_id |  currency of the product | loggedIn
images_URL | the URL of the AWS S3 image (Array) | loggedIn
image_description | a short description of the product (Array) | loggedIn


<!---
======================================================================================================================================
-->


## GET a Specific Product

> RESPONSE:

```json
{
    "product": [
        {
            "id": 15,
            "category_id": 2,
            "user_id": 10,
            "entry_date": "2018-10-19T14:03:19.000Z",
            "description": "Kate Spade New Flying Colours Pave Dash Earrings",
            "price": 45,
            "currency_id": "GBP",
            "User": {
                "id": 10,
                "first_name": "John",
                "last_name": "Doe",
                "username": "johndoe",
                "profile_URL": "https://demos.subinsb.com/isl-profile-pic/image/person.png",
                "story": null
            },
            "images": [
                {
                    "id": 29,
                    "image_URL": "https://twicely.shop/pub/media/wysiwyg/jewellery-9.jpg",
                    "image_description": "This is the image",
                    "image_date": "2018-10-19T14:03:19.000Z"
                },
                {
                    "id": 30,
                    "image_URL": "https://another image.jpg",
                    "image_description": "This is the image 2",
                    "image_date": "2018-10-19T14:03:19.000Z"
                }
            ],
            "Order": null,
            "Like": null
        }
    ],
    "info": "Success: Product successfully retrieved",
    "success": true
}
```

This endpoint retrieves a specific product. 

### HTTP Request

`GET api/v1/products/:product_id`


### URL Parameters

Parameter | Description
--------- | -----------
product_id | The id of the product to retrieve

### SCOPES

* *No permission required*

<!---
======================================================================================================================================
-->

## GET Product list

> REQUEST: 

```json
// --------
// HEADER
// --------
{
  "x-auth-token":"token"
}
```

> RESPONSE:

```json
{
    "product": {
        "count": 14,
        "rows": [
            {
                "id": 20,
                "category_id": 2,
                "user_id": 10,
                "entry_date": "2018-10-19T14:14:35.000Z",
                "description": "Kate Spade New Flying Colours Pave Dash Earrings",
                "price": 45,
                "currency_id": "GBP",
                "User": {
                    "id": 10,
                    "first_name": "John",
                    "last_name": "Doe",
                    "username": "johndoe",
                    "profile_URL": "https://demos.subinsb.com/isl-profile-pic/image/person.png",
                    "story": null
                },
                "images": [
                    {
                        "id": 39,
                        "image_URL": "https://twicely.shop/pub/media/wysiwyg/jewellery-9.jpg",
                        "image_description": "This is the image",
                        "image_date": "2018-10-19T14:14:35.000Z"
                    },
                    {
                        "id": 40,
                        "image_URL": "https://another image.jpg",
                        "image_description": "This is the image 2",
                        "image_date": "2018-10-19T14:14:35.000Z"
                    }
                ]
            }
        ]
    },
    "message": "Success: Product successfully retrieved",
    "success": true
}
```

This endpoint retrieves a list of all products for the logged in user. 

### HTTP Request

`GET api/v1/products`

`GET api/v1/products?page=1&limit=20`

### URL Query

Parameter | Description | required?
--------- | ----------- | ------------
page | set the page number to retrieve | optional (default to 1)
limit | set the size of the page limit | optional (default to 15)

### SCOPES

* *You must be logged in to access this endpoint*


<!---
======================================================================================================================================
-->

## UPDATE a Product

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
  "category_id":1,
  "description":"update descr",
  "price": 123,
  "currency_id": "GBP"
}
```

> RESPONSE:

```json
{
    "product": {
        "id": 15,
        "category_id": 1,
        "user_id": 10,
        "entry_date": "2018-10-19T14:03:19.000Z",
        "description": "update descr",
        "price": 123,
        "currency_id": "GBP",
        "images": [
            {
                "id": 29,
                "image_URL": "https://twicely.shop/pub/media/wysiwyg/jewellery-9.jpg",
                "image_description": "This is the image",
                "image_date": "2018-10-19T14:03:19.000Z"
            },
            {
                "id": 30,
                "image_URL": "https://another image.jpg",
                "image_description": "This is the image 2",
                "image_date": "2018-10-19T14:03:19.000Z"
            }
        ]
    },
    "message": "Success: Product successfully updated",
    "success": true
}
```

This endpoint updates a specific product.

### HTTP Request

`UPDATE api/v1/products`

### URL Parameters

* *No parameters required*

### SCOPES

* This endpoint requires an authentication token to access.

### FIELDS

These fields are available to be updated:

Field | Description | Permission
--------- | ----------- | ---------
category_id | category of the product | loggedIn
description | description of the product |  loggedIn
price | price of the product | loggedIn
currency_id | currency of the product | loggedIn


<!---
======================================================================================================================================
-->

## DELETE a Product


> REQUEST: 

```json
// --------
// HEADER
// --------
{
  "x-auth-token":"token"
}

```

> RESPONSE:

```json
{
    "product": {
        "id": 15,
        "category_id": 1,
        "user_id": 10,
        "entry_date": "2018-10-19T14:03:19.000Z",
        "description": "update descr",
        "price": 123,
        "currency_id": "GBP",
        "shipping_YN": true,
        "meet_in_person_YN": false,
        "created_at": "2018-10-19T14:03:19.000Z",
        "updated_at": "2018-10-19T14:26:31.000Z"
    },
    "message": "Success: Product successfully deleted",
    "success": true
}
```

This endpoint deletes a product. 

### HTTP Request

`DELETE api/v1/products/:product_id`


### URL Parameters

Parameter | Description
--------- | -----------
product_id | The id of the product to be deleted

### SCOPES

* This endpoint requires an authentication token to access.



<!---
======================================================================================================================================
-->


# Orders


<!---
======================================================================================================================================
-->


## CREATE a Order

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
  //Product
  "product_id":11,
  "delivery_method": "shipping"
}
```

> RESPONSE:

```json
{
    "DEBUG": "POST create new order",
    "status": 200,
    "message": "Success: Order successfully created",
    "data": {
        "order_id": 47,
        "order_date": "2018-07-14T19:59:04.000Z",
        "delivery_method": "shipping",
        "Product": {
            "id": 15,
            "category_id": 1,
            "user_id": 11,
            "entry_date": "2017-12-28T00:00:00.000Z",
            "description": "PRE-OWNED 18CT YELLOW GOLD FANCY BAND RING",
            "shipping_YN": true,
            "meet_in_person_YN": false,
            "created_at": "2018-07-13T12:16:20.000Z",
            "updated_at": "2018-07-13T12:16:20.000Z",
            "product_id": null,
            "Prices": [
                {
                    "price": 331.2
                }
            ]
        },
        "OrderStatus": {
            "description": "OPEN"
        }
    }
}
```

This endpoint creates a new order.

### HTTP Request

`POST api/v1/orders`

### URL Parameters

* *No parameters required*

### SCOPES

* *This endpoint requires an authentication token to access.*

<!---
======================================================================================================================================
-->


## GET a Specific Order


> REQUEST: 

```json
// --------
// HEADER
// --------
{
  "x-auth-token":"token"
}
```

> RESPONSE:

```json
{
    "DEBUG": "GET order",
    "status": 200,
    "message": "Success: Order successfully found",
    "data": {
        "order_id": 41,
        "order_date": "2018-07-14T14:13:51.000Z",
        "delivery_method": "shipping",
        "Product": {
            "id": 11,
            "category_id": 1,
            "user_id": 11,
            "entry_date": "2017-11-14T00:00:00.000Z",
            "description": "PRE OWNED 9CT YELLOW GOLD 7 BAR GATE BRACELET",
            "shipping_YN": false,
            "meet_in_person_YN": true,
            "created_at": "2018-07-13T12:16:20.000Z",
            "updated_at": "2018-07-13T12:16:20.000Z",
            "product_id": null,
            "Prices": [
                {
                    "price": 106.8
                }
            ]
        },
        "OrderStatus": {
            "description": "OPEN"
        }
    }
}
```

This endpoint retrieves a specific order. 

### HTTP Request

`GET api/v1/orders/:order_id`

Example: [GET order Id 1](https://jwl-be-staging.herokuapp.com/api/v1/orders/1)

### URL Parameters

Parameter | Description
--------- | -----------
order_id | The id of the order to retrieve

### SCOPES

* *This endpoint requires an authentication token to access.*



<!---
======================================================================================================================================
-->


## GET Order list


> REQUEST: 

```json
// --------
// HEADER
// --------
{
  "x-auth-token":"token"
}
```

> RESPONSE:

```json
{
    "DEBUG": "GET All orders for current logged in user",
    "status": 200,
    "message": "Success: Orders successfully found",
    "data": [
        {
            "order_id": 41,
            "order_date": "2018-07-14T14:13:51.000Z",
            "delivery_method": "shipping",
            "Product": {
                "id": 11,
                "category_id": 1,
                "user_id": 11,
                "entry_date": "2017-11-14T00:00:00.000Z",
                "description": "PRE OWNED 9CT YELLOW GOLD 7 BAR GATE BRACELET",
                "shipping_YN": false,
                "meet_in_person_YN": true,
                "created_at": "2018-07-13T12:16:20.000Z",
                "updated_at": "2018-07-13T12:16:20.000Z",
                "product_id": null,
                "Prices": [
                    {
                        "price": 106.8
                    }
                ]
            },
            "OrderStatus": {
                "description": "OPEN"
            }
        },
    ]
}
```

This endpoint retrieves a list of all orders for the logged in user. 

### HTTP Request

`GET api/v1/orders`

Example: [GET User All](https://jwl-be-staging.herokuapp.com/api/v1/orders)

`GET api/v1/orders?page=1&limit=20`

Example: [GET Orders All](https://jwl-be-staging.herokuapp.com/api/v1/orders?page=1&limit=20)

### URL Query

Parameter | Description | required?
--------- | ----------- | ------------
page | set the page number to retrieve | optional (default to 1)
limit | set the size of the page limit | optional (default to 15)

### SCOPES

* *You must be logged in to access this endpoint*




<!---
======================================================================================================================================
-->


## UPDATE a Order


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
  "category_id":8,
  "description":"test description 23",
  "shipping_YN":0,
  "price": 999,
  "product_id":100
}
```

> RESPONSE:

```json
{
    "DEBUG": "PUT user: 16's order",
    "status": 200,
    "message": "Success: Order successfully updated",
    "data": {
        "user": {
            "user_id": 16,
            "first_name": "Jon",
            "last_name": "Snow",
            "username": "JonSnow"
        },
        "category_id": 8,
        "entry_date": "2018-07-13T12:17:39.000Z",
        "description": "test description 23",
        "shipping_YN": true,
        "meet_in_person_YN": true,
        "Price": {
            "price": 999,
            "entry_date": "2018-07-13T13:38:35.000Z",
            "active_YN": true
        }
    }
}
```

This endpoint update a order.

### HTTP Request

`UPDATE api/v1/orders`

### URL Parameters

* *No parameters required*

### SCOPES

* This endpoint requires an authentication token to access.

### FIELDS

These fields are available to be updated:

Field | Description | Permission
--------- | ----------- | ---------
delivery_method | The method chosen by the buyer to receive the goods | loggedIn

<!---
======================================================================================================================================
-->


## DELETE a Order

> REQUEST: 

```json
// --------
// HEADER
// --------
{
  "x-auth-token":"token"
}

```

> RESPONSE:

```json
{
    "DEBUG": "DELETE order deleted",
    "status": 200,
    "message": "Success: Order successfully deleted",
    "data": {
        "id": 48,
        "user_id": 16,
        "product_id": 15,
        "order_date": "2018-07-14T20:03:34.000Z",
        "order_status_id": 5,
        "delivery_method": "shipping",
        "created_at": "2018-07-14T20:03:34.000Z",
        "updated_at": "2018-07-14T20:03:34.000Z"
    }
}
```

This endpoint deletes a order. 

### HTTP Request

`DELETE api/v1/orders/:order_id`

<aside class="notice">
This is an <strong>ADMIN</strong> Route. You must have administrator rights to perform this action.
</aside>


### URL Parameters

Parameter | Description
--------- | -----------
order_id | The id of the product to be deleted

### SCOPES

* This endpoint requires an authentication token to access.

<!---
======================================================================================================================================
-->


# Order Statuses

<!---
======================================================================================================================================
-->

## CREATE Order Status

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
  //Order Status
  "id":11,
  "description": "Another Order Status"
}
```

> RESPONSE:

```json
{
    "DEBUG": "GET orderStatus",
    "status": 200,
    "message": "Success: orderStatus data successfully created",
    "data": {
        "id": 11,
        "description": "Another Order Status"
    }
}
```

This endpoint creates a new order status.

### HTTP Request

`POST api/v1/orderstatuses`

### URL Parameters

* *No parameters required*

### SCOPES

* *This endpoint requires an authentication token to access.*

<!---
======================================================================================================================================
-->


## GET Order Status list


> REQUEST: 

```json
// --------
// HEADER
// --------
{
  "x-auth-token":"token"
}
```

> RESPONSE:

```json
{
    "DEBUG": "GET orderStatus",
    "status": 200,
    "message": "Success: OrderStatus data successfully retrieved",
    "data": [
        {
            "orderstatus_id": 5,
            "description": "OPEN"
        },
        {
            "orderstatus_id": 10,
            "description": "CLOSED"
        },
        {
            "orderstatus_id": 99,
            "description": "CANCELLED"
        }
    ]
}
```

This endpoint retrieves a list of all order statuses. 

### HTTP Request

`GET api/v1/ordersstatuses`

Example: [GET Order Statuses All](https://jwl-be-staging.herokuapp.com/api/v1/orderstatuses)

### URL Parameters

* *No parameters required*

### SCOPES

* *You must be logged in to access this endpoint*


## UPDATE Order Status

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
  "description":"updated a description"
}
```

> RESPONSE:

```json
{
    "DEBUG": "Update a specific orderStatus",
    "status": 200,
    "message": "Success: orderStatus data successfully updated",
    "data": {
        "id": 5,
        "description": "I CHANGED THIS"
    }
}
```

This endpoint update an order status.

### HTTP Request

`UPDATE api/v1/ordersstatuses`

### URL Parameters

* *No parameters required*

### SCOPES

* This endpoint requires an authentication token to access.

### FIELDS

These fields are available to be updated:

Field | Description | Permission
--------- | ----------- | ---------
description | The description of an order status | loggedIn

## DELETE an Order Status


> REQUEST: 

```json
// --------
// HEADER
// --------
{
  "x-auth-token":"token"
}

```

> RESPONSE:

```json
{
    "DEBUG": "DELETE an orderStatus",
    "status": 200,
    "message": "Success: Order Status successfully deleted",
    "data": {
        "id": 21,
        "description": "some description",
        "created_at": "2018-07-16T13:55:35.000Z",
        "updated_at": "2018-07-16T13:55:35.000Z"
    }
}
```

This endpoint deletes an order status. 

### HTTP Request

`DELETE api/v1/orderstatuses/:orderstatus_id`


### URL Parameters

Parameter | Description
--------- | -----------
orderstatus_id | The id of the order status to be deleted

### SCOPES

* This endpoint requires an authentication token to access.

<!---
======================================================================================================================================
-->

# Categories


<!---
======================================================================================================================================
-->

## CREATE a category

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
  "product_type": "Back",
  "description": "Jerwellery for your back",
  "active_YN": 1
}
```

> RESPONSE:

```json
{
    "DEBUG": "CREATE a new category",
    "status": 200,
    "message": "Success: Category data successfully created",
    "data": {
        "product_type": "Back",
        "description": "Jerwellery for your back"
    }
}
```

This endpoint creates a new category.

### HTTP Request

`POST api/v1/categories`

<aside class="notice">
This is an <strong>ADMIN</strong> Route. You must have administrator rights to perform this action.
</aside>

### URL Parameters

* *No parameters required*

### SCOPES

* *This endpoint requires **ADMIN** token to access.*

<!---
======================================================================================================================================
-->

## GET Categories list


> REQUEST: 

```json
// --------
// HEADER
// --------
{
  "x-auth-token":"token"
}
```

> RESPONSE:

```json
{
    "DEBUG": "GET category",
    "status": 200,
    "message": "Success: Category data successfully retrieved",
    "data": [
        {
            "category_id": 1,
            "product_type": "Hair and head ornaments",
            "description": "Jewellery for your hair and head"
        },
        {
            "category_id": 2,
            "product_type": "Neck",
            "description": "Anything that goes on your neck"
        },
        {
            "category_id": 3,
            "product_type": "Arms",
            "description": "Jewellery for your arms"
        },
        {
            "category_id": 4,
            "product_type": "Hands",
            "description": "Jewellery for your hands like rings"
        },
        {
            "category_id": 5,
            "product_type": "Body",
            "description": "Anything that goes on your body"
        },
        {
            "category_id": 6,
            "product_type": "Feet",
            "description": "Jewellery for your feet"
        },
        {
            "category_id": 7,
            "product_type": "Back",
            "description": "Jerwellery for your back"
        }
    ]
}
```

This endpoint retrieves a list of all categories. 

### HTTP Request

`GET api/v1/categories`

Example: [GET Categories All](https://jwl-be-staging.herokuapp.com/api/v1/categories)

### URL Query

* *No parameters required*

### SCOPES

* *You must be logged in to access this endpoint*


<!---
======================================================================================================================================
-->


## GET a Specific Category


> REQUEST: 

```json
// --------
// HEADER
// --------
{
  "x-auth-token":"token"
}
```

> RESPONSE:

```json
{
    "DEBUG": "GET a specific category",
    "status": 200,
    "message": "Success: Category data successfully retrieved",
    "data": {
        "id": 1,
        "product_type": "Hair and head ornaments",
        "description": "Jewellery for your hair and head",
        "active_YN": true,
        "created_at": "2018-08-05T09:34:14.000Z",
        "updated_at": "2018-08-05T09:34:14.000Z"
    }
}
```

This endpoint retrieves a specific order. 

### HTTP Request

`GET api/v1/categories/:category_id`

Example: [GET a specific category Id 1](https://jwl-be-staging.herokuapp.com/api/v1/category/1)

### URL Parameters

Parameter | Description
--------- | -----------
category_id | The id of the category to retrieve

### SCOPES

* *This endpoint requires an authentication token to access.*

<!---
======================================================================================================================================
-->



## UPDATE a Category


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
  "product_type": "Updated Category",
  "description":"This is definitely not a category",
  "active_YN": 1
}
```

> RESPONSE:

```json
{
    "DEBUG": "UPDATE a category",
    "status": 200,
    "message": "Success: Category data successfully created",
    "data": {
        "product_type": "Updated Category",
        "description": "This is definitely not a category",
        "active_YN": true
    }
}
```

This endpoint will update a specific category.

### HTTP Request

`UPDATE api/v1/categories`

<aside class="notice">
This is an <strong>ADMIN</strong> Route. You must have administrator rights to perform this action.
</aside>

### URL Parameters

* *No parameters required*

### SCOPES

* This endpoint requires an ADMIN authentication token to access.

### FIELDS

These fields are available to be updated:

Field | Description | Permission
--------- | ----------- | ---------
product_type | category product name | ADMIN
description | description of the category | ADMIN
active_YN | determine if category is used | ADMIN

<!---
======================================================================================================================================
-->



## DELETE a cateogry

> REQUEST: 

```json
// --------
// HEADER
// --------
{
  "x-auth-token":"token"
}
```

> RESPONSE:

```json
{
    "DEBUG": "DELETE category",
    "status": 200,
    "message": "Success: categories 6 data successfully deleted!",
    "data": [
        {
            "fieldCount": 0,
            "affectedRows": 1,
            "insertId": 0,
            "info": "",
            "serverStatus": 2,
            "warningStatus": 0
        },
        {
            "fieldCount": 0,
            "affectedRows": 1,
            "insertId": 0,
            "info": "",
            "serverStatus": 2,
            "warningStatus": 0
        }
    ]
}
```

This endpoint deletes a specific category.


### HTTP Request

`DELETE api/v1/categories/:category_id`

<aside class="notice">
This is an <strong>ADMIN</strong> Route. You must have administrator rights to perform this action.
</aside>

### URL Parameters

* *No parameters required*

### SCOPES

* This endpoint requires an authentication token to access.



<!---
======================================================================================================================================
-->



# Uploads


<!---
======================================================================================================================================
-->



## CREATE S3 Upload URL
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
  "upload_type":"documents",
  "document_type":"national_id",
  "images":["nationalid.png", "cat.png", "dob.png"]
}
```

> RESPONSE:

```json
[
    {
        "imageName": "nationalid.png",
        "key": "16/documents/national_id/69dbd320-998e-11e8-8796-272fbb9ba1a5.png",
        "url": "https://jwl-public.s3.eu-west-2.amazonaws.com/16/documents/national_id/69dbd320-998e-11e8-8796-272fbb9ba1a5.png?Content-Type=image%2Fpng&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIKFT6IEBSN7KHXRQ%2F20180806%2Feu-west-2%2Fs3%2Faws4_request&X-Amz-Date=20180806T153557Z&X-Amz-Expires=900&X-Amz-Signature=1ea36e60a940f1d02ab1b674219066cd1f5f2d2b7c17d7a93bf5fb18cdc4944c&X-Amz-SignedHeaders=host"
    },
    {
        "imageName": "cat.png",
        "key": "16/documents/national_id/69dc4850-998e-11e8-8796-272fbb9ba1a5.png",
        "url": "https://jwl-public.s3.eu-west-2.amazonaws.com/16/documents/national_id/69dc4850-998e-11e8-8796-272fbb9ba1a5.png?Content-Type=image%2Fpng&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIKFT6IEBSN7KHXRQ%2F20180806%2Feu-west-2%2Fs3%2Faws4_request&X-Amz-Date=20180806T153557Z&X-Amz-Expires=900&X-Amz-Signature=515ffece8e866981f24f13b0226fa5b6188451ae7a48dd8522014e51f2f27eaa&X-Amz-SignedHeaders=host"
    },
    {
        "imageName": "dob.png",
        "key": "16/documents/national_id/69dc4851-998e-11e8-8796-272fbb9ba1a5.png",
        "url": "https://jwl-public.s3.eu-west-2.amazonaws.com/16/documents/national_id/69dc4851-998e-11e8-8796-272fbb9ba1a5.png?Content-Type=image%2Fpng&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAIKFT6IEBSN7KHXRQ%2F20180806%2Feu-west-2%2Fs3%2Faws4_request&X-Amz-Date=20180806T153557Z&X-Amz-Expires=900&X-Amz-Signature=4b1d6a96ff1e7855d97cfb72a2da16dabba70fbd62cfcfaea1c68cbd4cc5ec92&X-Amz-SignedHeaders=host"
    }
]
```

This endpoint will generate unique URLS to enable the front end client to upload pictures to AWS S3s

### HTTP Request

`POST api/v1/upload`


### URL Parameters

* *No parameters required*

### SCOPES

* *This endpoint requires a user to be  **Logged In** to access.*


<!---
======================================================================================================================================
-->


# Feeds


<!---
======================================================================================================================================
-->



## GET a Feed List


> RESPONSE:

```json
{
    "DEBUG": "GET  Feed",
    "status": 200,
    "message": "Success: Feed data successfully retrieved",
    "data": [
        {
            "product_id": 32,
            "category_id": 4,
            "entry_date": "2018-01-20T00:00:00.000Z",
            "description": "PRE OWNED 9CT YELLOW GOLD JUG CHARM",
            "shipping_YN": false,
            "meet_in_person_YN": true,
            "User": {
                "user_id": 9,
                "first_name": "Bat",
                "last_name": "Man",
                "username": "BatMan",
                "profile_URL": "https://source.unsplash.com/collection/888146/300x300"
            },
            "Images": [
                {
                    "image_URL": "https://picsum.photos/200/300",
                    "image_description": "Bacon ipsum dolor amet shankle porchetta brisket beef alcatra, tongue venison.",
                    "image_date": "2017-11-28T00:00:00.000Z"
                }
            ],
            "Prices": [
                {
                    "price": 549.6
                }
            ]
        }
    ]
}...
```

This endpoint retrieves a feed list.

### HTTP Request

`GET api/v1/feeds?page=1&limit=15`

Example: [GET Feed](https://jwl-be-staging.herokuapp.com/api/v1/feeds?page=1&limit=15)

Filter by options:

`GET api/v1/feeds?page=1&limit=15&max_price=500&user_id=1`

Example: [GET Feed Filtered by Max Price and User ID](https://jwl-be-staging.herokuapp.com/api/v1/feeds?page=1&limit=15&max_price=500&user_id=1)

### URL Query

Parameter | Description | required?
--------- | ----------- | ------------
page | set the page number to retrieve | optional (default to 1)
limit | set the size of the page limit | optional (default to 15)
user_id | the user id that is to be filtered by | optional
category_id | the category id that is to be filtered by  | optional
description | the description that is to be filtered by | optional
max_price | filter by the maximum price amount | optional
min_price | filter by the minimum price amount | optional


### SCOPES

* *You must be logged in to access this endpoint*


<!---
======================================================================================================================================
-->


# Payments (STRIPE)


<!---
======================================================================================================================================
-->



## CREATE a Payment Charge

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
  "stripeToken":"stripeToken",
  "product_id": 2
}
```

> RESPONSE:

```json

// ---------
// SUCCESS
// ---------
{
    "DEBUG": "POST create a payment against a product",
    "status": 200,
    "message": "Success: Payment successfully made",
    "data": {
        "data": {
            "order_id": 41,
            "order_date": "2018-08-31T12:11:57.000Z",
            "delivery_method": null,
            "Product": {
                "id": 2,
                "category_id": 3,
                "user_id": 13,
                "entry_date": "2017-11-26T00:00:00.000Z",
                "description": "PRE-OWNED 1982 HALF SOVEREIGN COIN PENDANT",
                "shipping_YN": true,
                "meet_in_person_YN": false,
                "created_at": "2018-08-30T18:15:41.000Z",
                "updated_at": "2018-08-30T18:15:41.000Z",
                "product_id": null,
                "Prices": [
                    {
                        "price": 590.4
                    }
                ]
            },
            "OrderStatus": {
                "description": "OPEN"
            }
        },
        "info": "Success: Order successfully created"
    }
}

// --------
// ERROR
// --------

{
    "status": 400,
    "message": "Server Error!",
    "err": "Product already sold",
    "redirect": "/"
}
```

This endpoint will create a charge for a product. If successful it will generate an order.


### HTTP Request

`POST api/v1/payments/stripe/charge`

### URL Parameters

* *No parameters required*

### SCOPES

* This endpoint requires an authentication token to access.



<!---
======================================================================================================================================
-->



# Images


<!---
======================================================================================================================================
-->


## GET Images list


<!---
======================================================================================================================================
-->

