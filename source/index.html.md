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
  "shipping_YN":0,
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
    "DEBUG": "DELETE order delted",
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


## Update Order Status

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

## Delete an Order Status


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


## GET Categories list


<!---
======================================================================================================================================
-->


# Uploads


<!---
======================================================================================================================================
-->


## CREATE S3 Signed URL 


<!---
======================================================================================================================================
-->


# Feeds


<!---
======================================================================================================================================
-->


## GET Feed list


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


# Payments


<!---
======================================================================================================================================
-->
