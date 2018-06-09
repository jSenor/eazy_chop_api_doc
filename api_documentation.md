
# Eazychop Api Documentation

The api contains resources, and each resource has serval actions that can be performed on it.

## Resources
* [User](#user)

## User

### User Schema

The representation of a valid user is given below

```json
    {
        "phone": Number,
        "firstname": String,
        "lastname": String,
        "password": String,
        "wallet": Number
    }
```

### User creation

`POST` /users

`REQUEST-BODY` phone, firstname, lastname, password

Example 

```javascript
    fetch(/users, {
        method: POST
    })
```

