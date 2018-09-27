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

Welcome to the Minto API! You can use our API to access Minto API endpoints, which can get information on various products in our database.

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

Minto uses Passport's `facebook-token` and pure email and password as part of the authentication process.

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
	"first_name": "john",
	"last_name":"doe",
	"username": "johndoe",
	"email":"john.doe@hotmail.co.uk",
	"password":"password"
}
```

> RESPONSE:

```json
{
  "data": {
    "id": 32,
    "first_name": "justin",
    "last_name": "lai",
    "username": "justintlai",
    "email": "justin.t.lai@hotmail.co.uk",
    "password": null,
    "fb_id": null,
    "fb_token": null,
    "stripe_customer_id": null,
    "profile_URL": null,
    "national_id_URL": null,
    "email_verified_YN": false,
    "seller_YN": false,
    "disabled_YN": false,
    "admin_YN": false,
    "deleted_YN": false,
    "created_at": "2018-09-09T19:56:41.000Z",
    "updated_at": "2018-09-09T19:56:41.000Z",
    "user_id": null
  },
  "info": "Success: User Found"
}
```

This endpoint will create a new user or login an existing user.

### HTTP Request

`POST api/v1/auth/login`

### URL Parameters

* *No parameters required*

### SCOPES

* *This endpoint requires Facebook Login to Authenticate*



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
    "profile_URL":"https://demos.subinsb.com/isl-profile-pic/image/person.png",
    "national_id_URL":"https://demos.subinsb.com/isl-profile-pic/image/person.png"
}
```

This endpoint creates a new user.

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


<!---
======================================================================================================================================
-->
## READ a list of all users


> RESPONSE:

```json
{
    "DEBUG": "GET All users",
    "status": 200,
    "message": "Success: User successfully retrieved",
    "data": [
        {
            "user_id": 1,
            "first_name": "Mark",
            "last_name": "Robins",
            "username": "MarkRobins",
            "email": "MarkRobins@gmail.com",
            "profile_URL": "https://source.unsplash.com/collection/888146/300x300",
            "national_id_URL": null,
            "email_verified_YN": 0,
            "seller_YN": 0,
            "disabled_YN": 0,
            "admin_YN": 0,
            "total_followers": 12,
            "total_following": 1,
            "total_products": 6
        }...
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

This endpoint deletes a user. 
Currently, this will not completely delete all user actions in the database. It will only delete the user from the user table.


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
```

> REQUEST: 

```json
{
  "folloing_id": 1,
}
```

> RESPONSE:

```json
{
    "data": {
        "id": 2,
        "follower_id": 17,
        "following_id": 4,
        "follow_date": "2018-09-26T05:24:08.000Z"
    },
    "info": "Success: Follower data successfully created"
}
```

This endpoint creates a new follower for the user logged in.

### HTTP Request

`POST api/v1/followers`

### URL Parameters

* *No parameters required*

### SCOPES

* *This endpoint requires Facebook Login to Authenticate*

<!---
======================================================================================================================================
-->
## READ a Specific User's Follower List

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
  "data": {
      "count": 2,
      "rows": [
          {
              "id": 1,
              "follower_id": 1,
              "following_id": 2,
              "follow_date": "2017-12-01T00:00:00.000Z",
              "created_at": "2018-08-30T08:30:33.000Z",
              "updated_at": "2018-08-30T08:30:33.000Z"
          },
          {
              "id": 2,
              "follower_id": 1,
              "following_id": 3,
              "follow_date": "2017-12-03T00:00:00.000Z",
              "created_at": "2018-08-30T08:30:33.000Z",
              "updated_at": "2018-08-30T08:30:33.000Z"
          }
      ]
  },
  "info": "Success: Follower data successfully retrieved"
}
```

This endpoint retrieves a specific user. 

It will return a users profile along with the number of followers, likes and profile picture.

### HTTP Request

`GET api/v1/followers/:user_id`

### URL Parameters

Parameter | Description
--------- | -----------
user_id | The id of the user to retrieve

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
  "data": {
      "count": 2,
      "rows": [
          {
              "id": 1,
              "follower_id": 1,
              "following_id": 2,
              "follow_date": "2017-12-01T00:00:00.000Z",
              "created_at": "2018-08-30T08:30:33.000Z",
              "updated_at": "2018-08-30T08:30:33.000Z"
          },
          {
              "id": 2,
              "follower_id": 1,
              "following_id": 3,
              "follow_date": "2017-12-03T00:00:00.000Z",
              "created_at": "2018-08-30T08:30:33.000Z",
              "updated_at": "2018-08-30T08:30:33.000Z"
          }
      ]
  },
  "info": "Success: Follower data successfully retrieved"
}
```

This endpoint retrieves a list of all follower for the user logged in. 

You can optionally add parameters to further define your output but defaults are applied if nothing is supplied.

### HTTP Request

`GET api/v1/followers/`

`GET api/v1/followers?page=1&limit=20`

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
    "data": {
        "id": 40,
        "follower_id": 17,
        "following_id": 6,
        "follow_date": "2018-09-26T11:30:53.000Z",
        "created_at": "2018-09-26T11:30:53.000Z",
        "updated_at": "2018-09-26T11:30:53.000Z"
    },
    "info": "Success: User id 17 has unfollowed user id 6"
}
```

This endpoint deletes a follower from the logged in user's follower list. 

### HTTP Request

`DELETE api/v1/followers/:follower_id`

### URL Parameters

Parameter | Description
--------- | -----------
follower_id | The id of the user to unfollow

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
  "data": {
      "user_id": 17,
      "address_type": "delivery", 
      "address_name": "Shoreditch Home",
      "address1": "Flat 5",
      "address2": "176 Shoreditch High Street",
      "city": "London",
      "postcode": "E1 6AX",
      "country": "United Kingdom",
      "country_code": "UK",
      "primary_YN": true
  },
  "info": "Success: Address data successfully created"
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
    "data": {
        "count": 1,
        "rows": [
            {
                "id": 1,
                "user_id": 17,
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
                "country_code": "UK",
                "primary_YN": false,
                "created_at": "2018-09-26T07:42:56.000Z",
                "updated_at": "2018-09-26T07:54:59.000Z"
            }
        ]
    },
    "info": "Success: Address data successfully retrieved"
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
    "data": {
        "count": 1,
        "rows": [
            {
                "id": 1,
                "user_id": 17,
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
                "country_code": "UK",
                "primary_YN": false,
                "created_at": "2018-09-26T07:42:56.000Z",
                "updated_at": "2018-09-26T07:54:59.000Z"
            }
        ]
    },
    "info": "Success: Address data successfully retrieved"
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
    "data": {
        "user_id": 17,
        "address_type": "delivery",
        "address_name": "New Name",
        "address1": "Flat 5",
        "address2": "176 Shoreditch High Street",
        "address3": null,
        "address4": null,
        "city": "London",
        "county": null,
        "postcode": "E1 6AX",
        "country": "United Kingdom",
        "country_code": "UK",
        "primary_YN": false
    },
    "info": "Success: Address data successfully updated"
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
    "data": {
        "id": 5,
        "user_id": 17,
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
        "country_code": "UK",
        "primary_YN": false,
        "created_at": "2018-09-26T07:55:22.000Z",
        "updated_at": "2018-09-26T07:58:35.000Z"
    },
    "info": "Success: Addresses 5 data successfully deleted!"
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
  //Product Category
  "category_id":11,
  "description":"test description",
  //Price
  "price":"100",
  "currency_id":"GBP",
  "shipping_YN":1,
  "meet_in_person_YN":1,
  //Image Information
  "images": [
    {
      "image_URL": "image1.com",
      "image_description": "test image description",
      "image_date": ""
    },
    {
      "image_URL": "image2.com",
      "image_description": "test 2 image description",
      "image_date": ""
    }
  ]
}
```

> RESPONSE:

```json
{
    "DEBUG": "POST create new product",
    "status": 200,
    "message": "Success: Product successfully created",
    "data": {
        "user_id": 16,
        "first_name": "Jon",
        "last_name": "Snow",
        "username": "JonSnow",
        "product_id": 110,
        "category_id": 11,
        "entry_date": "2018-07-13T12:32:10.000Z",
        "description": "King of the North",
        "shipping_YN": true,
        "meet_in_person_YN": true,
        "images": [
            {
                "image_id": 120,
                "image_URL": "Wolves.com",
                "image_description": "My Wolves",
                "image_date": "2018-07-13T12:32:10.000Z",
                "primary_YN": false
            },
            {
                "image_id": 121,
                "image_URL": "Selfie.com",
                "image_description": "Jon snow",
                "image_date": "2018-07-13T12:32:10.000Z",
                "primary_YN": true
            }
        ],
        "price": "100",
        "active_YN": true,
        "currency_id": "GBP"
    }
}
```

This endpoint creates a new product.

### HTTP Request

`POST api/v1/products`

### URL Parameters

* *No parameters required*

### SCOPES

* *This endpoint requires an authentication token to access.*


<!---
======================================================================================================================================
-->


## GET a Specific Product

> RESPONSE:

```json
{
    "DEBUG": "GET product by ProductID",
    "status": 200,
    "message": "Success: Product data successfully retrieved",
    "data": [
        {
            "product_id": 1,
            "category_id": 6,
            "entry_date": "2017-11-15T00:00:00.000Z",
            "description": "PRE-OWNED 9CT YELLOW GOLD FULL KRUGERRAND MOUNT PENDANT",
            "shipping_YN": false,
            "meet_in_person_YN": false,
            "User": {
                "user_id": 13,
                "first_name": "Rachel",
                "last_name": "Green",
                "username": "RachelGreen"
            },
            "Images": [
                {
                    "image_URL": "https://picsum.photos/200/300",
                    "image_description": "Bacon ipsum dolor amet shankle porchetta brisket beef alcatra, tongue venison.",
                    "image_date": "2017-11-01T00:00:00.000Z"
                }
            ],
            "Prices": [
                {
                    "price": 538.8
                }
            ]
        }
    ]
}
```

This endpoint retrieves a specific product. 

### HTTP Request

`GET api/v1/products/:product_id`

Example: [GET Product Id 1](https://jwl-be-staging.herokuapp.com/api/v1/product/1)

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
    "DEBUG": "GET  user: 1's product",
    "status": 200,
    "message": "Success: Product data successfully retrieved",
    "data": [
        {
            "product_id": 28,
            "category_id": 1,
            "entry_date": "2018-01-07T00:00:00.000Z",
            "description": "PRE-OWNED 9CT YELLOW GOLD ONYX SIGNET RING",
            "shipping_YN": true,
            "meet_in_person_YN": true,
            "User": {
                "user_id": 1,
                "first_name": "Mark",
                "last_name": "Robins",
                "username": "MarkRobins"
            },
            "Images": [
                {
                    "image_URL": "https://picsum.photos/200/300",
                    "image_description": "Bacon ipsum dolor amet shankle porchetta brisket beef alcatra, tongue venison.",
                    "image_date": "2017-12-29T00:00:00.000Z"
                }
            ],
            "Prices": [
                {
                    "price": 583.2
                }
            ]
        }
    ]
}
```

This endpoint retrieves a list of all products for the logged in user. 

### HTTP Request

`GET api/v1/products`

Example: [GET User All](https://jwl-be-staging.herokuapp.com/api/v1/products)

`GET api/v1/products?page=1&limit=20`

Example: [GET Products All](https://jwl-be-staging.herokuapp.com/api/v1/products?page=1&limit=20)

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
  "category_id":8,
  "description":"test description 23",
  "shipping_YN":false,
  "price": 999,
  "product_id":100
}
```

> RESPONSE:

```json
{
    "DEBUG": "PUT  user: 16's product",
    "status": 200,
    "message": "Success: Product successfully updated",
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

This endpoint update a product.

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
shipping_YN | seller allowing shipping conditions | loggedIn
meet_in_person_YN |  seller will meet in person to exchange goods | loggedIn
price | update the price of the product | loggedIn

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
    "DEBUG": "DELETE  productId: 103",
    "status": 200,
    "message": "Success: Product successfully deleted",
    "data": [
        {
            "id": 103,
            "category_id": 11,
            "user_id": 16,
            "entry_date": "2018-07-13T12:22:17.000Z",
            "description": "test description",
            "shipping_YN": true,
            "meet_in_person_YN": true,
            "created_at": "2018-07-13T12:22:17.000Z",
            "updated_at": "2018-07-13T12:22:17.000Z",
            "product_id": null
        },
        {
            "id": 103,
            "currency_id": "GBP",
            "product_id": 103,
            "price": 100,
            "entry_date": "2018-07-13T12:22:17.000Z",
            "active_YN": true,
            "created_at": "2018-07-13T12:22:17.000Z",
            "updated_at": "2018-07-13T12:22:17.000Z"
        },
        {
            "id": 106,
            "product_id": 103,
            "image_URL": "image1.com",
            "image_description": "test image description",
            "image_date": "2018-07-13T12:22:17.000Z",
            "primary_YN": false,
            "created_at": "2018-07-13T12:22:17.000Z",
            "updated_at": "2018-07-13T12:22:17.000Z"
        }
    ]
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

