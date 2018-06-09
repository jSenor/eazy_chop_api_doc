
# Eazychop Api Documentation

The api contains resources, and each resource has serval actions that can be performed on it.

A note on responses. Every response has a status code and a custom code.

The custom code is the machine friendly description of the error that you can use if your switch statements or if blocks. If not custom code is specified then the statusCode would be used

Below is a list of some of the response codes you might see

`200` For everything that went right

`400` The request you sent to us was invalid. Missing params, invalid params e.t.c

`403` The request you sent to us was good, but we could not fufill your request mostly because you are not authorized to do what you are asking

`500` Internal Server error something went wrong on the server when processing the request

## Resources
* [User](#user)

## User

### User Schema

The representation of a valid user is given below

```json
    {
        "phone": "Number",
        "firstname": "String",
        "lastname": "String",
        "password": "String",
        "wallet": "Number
    }
```

### Fetch All Users (Will not be released in production)

#### `GET` /users

#### `RESPONSE-PARAMS` users

Example

``` javascript
    fetch("/users") //Returns an promise that will resolve to an object with an array of users.
```

####
Response

`200` Fetched successfully

`500` Internal server error

### User creation

#### `POST` /users

#### `REQUEST-BODY` phone, firstname, lastname, password

Example 

```javascript

    fetch("/users", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
            phone: 0992839329,
            firstname: "Bob",
            lastname: "Alice",
            password: "closeyoureyes"
        })
    })

```

#### Response
`200` User created successfully

`400` Bad Request (code: "BAD_REQUEST") 

`403` User Exists (code: "USER_EXISTS")

`500` Internal Server Error | Something went wrong while creating the user


### User login

#### `POST` /users/login

#### `REQUEST-BODY` phone, password

#### `RESPONSE-PARAMS` token

You are required to store the token on the client, and attach it to future requests

Example

```javascript
    
    fetch("/users/login", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
            phone: 0992839329,
            password: "closeyoureyes"
        })
    })

```

#### Response

`200` User was logged in | Returns the user token

`400` Bad Request (Code: BAD_REQUEST)

`403` Authentication Failed (Code: AUTH_FAILED)

`500` Internal Server Error

### Fund Wallet

#### `POST` /users/fund

#### `REQUEST-BODY` token, amount

#### `RESPONE-PARAMS` currentAmount

Still need to take care of some security issues

Example

``` javascript
     fetch("/users/fund", {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify({
               token: "dfkjfhsfshkdhksdhdfd",
               amount: 500
           })
        })
```

#### Response

`200` Funded wallet successfully | Returns the current amount in the users wallet

`400` Token not found (Code: TOKEN_NOT_FOUND) // User sent a request without the token

`403` Token Expired (Code: TOKEN_EXPIRED)

`403` Token Invalid (Code: TOKEN_INVALID) // Someone tampered with the token

`403` User does not exist (Code: USER_DOES_NOT_EXIST) // Token was validated but the user generated doesn't exist

