
# Eazychop Api Documentation

The api contains resources, and each resource has serval actions that can be performed on it.

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

`400` User Exists (code: "USER_EXISTS")

`400` Bad Request (code: "BAD_REQUEST")

`500` Internal Server Error | Something went wrong while creating the user
