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

```javascript
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

# Kittens

## Get All Kittens

```javascript
  {
    x-auth-token: token
  }
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

