# API Documentation

## Address Routes

### 1. Update/Create Address

#### URL

`POST /address`

#### Description

This endpoint allows an authenticated user to create or update their address. If the user does not have an existing address, a new address will be created. If the user already has an address, it will be updated with the provided data.

#### Request Headers

- **Authorization**: Bearer token for authenticated user.
- **Cookie**: Contains the access token.

#### Request Body

The request body must be in JSON format and include the following fields:

- **primaryAddress** (object, required): The primary address of the user.
- **secondaryAddress** (object, optional): The secondary address of the user.
- **other address fields as required**.

#### Request Example

```json
{
  "primaryAddress": {
    "street": "123 Main St",
    "city": "Anytown",
    "state": "Anystate",
    "zip": "12345"
  },
  "secondaryAddress": {
    "street": "456 Side St",
    "city": "Othertown",
    "state": "Otherstate",
    "zip": "67890"
  }
}
```

#### Response

##### Success (200 OK)

If the address is created or updated successfully, the server responds with a JSON object containing the success status and the address data.

###### Response Example

```json
{
  "success": true,
  "data": {
    "_id": "60d9c6b0f1b4d72a8c8b4567",
    "primaryAddress": {
      "street": "123 Main St",
      "city": "Anytown",
      "state": "Anystate",
      "zip": "12345"
    },
    "secondaryAddress": {
      "street": "456 Side St",
      "city": "Othertown",
      "state": "Otherstate",
      "zip": "67890"
    }
  }
}
```

##### Client Error (400 Bad Request)

If there are validation errors in the provided address data, the server responds with an error message.

###### Response Example

```json
{
  "success": false,
  "message": "Validation errors",
  "errors": ["Invalid address format"]
}
```

##### Client Error (401 Unauthorized)

If the authentication token is not found, the server responds with an unauthorized error message.

###### Response Example

```json
{
  "success": false,
  "message": "Authentication token not found"
}
```

##### Client Error (404 Not Found)

If the user is not found, the server responds with a not found error message.

###### Response Example

```json
{
  "success": false,
  "message": "User not found"
}
```

##### Server Error (500 Internal Server Error)

If there is an internal server error, the server responds with an error message.

###### Response Example

```json
{
  "success": false,
  "message": "Internal Server Error"
}
```

### 2. Get Address by ID

#### URL

`GET /address/:id`

#### Description

This endpoint allows an authenticated user to retrieve an address by its ID.

#### Request Headers

- **Authorization**: Bearer token for authenticated user.

#### Request Parameters

- **id** (string, required): The ID of the address to be retrieved.

#### Request Example

```
GET /address/60d9c6b0f1b4d72a8c8b4567
```

#### Response

##### Success (200 OK)

If the address is retrieved successfully, the server responds with a JSON object containing the success status and the address data.

###### Response Example

```json
{
  "success": true,
  "data": {
    "_id": "60d9c6b0f1b4d72a8c8b4567",
    "primaryAddress": {
      "street": "123 Main St",
      "city": "Anytown",
      "state": "Anystate",
      "zip": "12345"
    },
    "secondaryAddress": {
      "street": "456 Side St",
      "city": "Othertown",
      "state": "Otherstate",
      "zip": "67890"
    }
  }
}
```

##### Client Error (404 Not Found)

If the address with the specified ID is not found, the server responds with a not found error message.

###### Response Example

```json
{
  "success": false,
  "message": "Address not found"
}
```

##### Server Error (500 Internal Server Error)

If there is an internal server error, the server responds with an error message.

###### Response Example

```json
{
  "success": false,
  "message": "Internal Server Error"
}
```

### 3. Delete Address by ID

#### URL

`DELETE /address/:id`

#### Description

This endpoint allows an authenticated user to delete an address by its ID.

#### Request Headers

- **Authorization**: Bearer token for authenticated user.

#### Request Parameters

- **id** (string, required): The ID of the address to be deleted.

#### Request Example

```
DELETE /address/60d9c6b0f1b4d72a8c8b4567
```

#### Response

##### Success (200 OK)

If the address is deleted successfully, the server responds with a JSON object containing the success status and a success message.

###### Response Example

```json
{
  "success": true,
  "message": "Address deleted successfully"
}
```

##### Client Error (404 Not Found)

If the address with the specified ID is not found, the server responds with a not found error message.

###### Response Example

```json
{
  "success": false,
  "message": "Address not found"
}
```

##### Server Error (500 Internal Server Error)

If there is an internal server error, the server responds with an error message.

###### Response Example

```json
{
  "success": false,
  "message": "Internal Server Error"
}
```

## Middleware

- **isAuthenticatedUser**: Ensures the user is authenticated.
- **authorizeRoles**: (Used for roles authorization in other routes if needed).

## Controller Functions

The `handleAddressUpdate`, `handleAddressGet`, and `handleAddressDelete` functions handle the address operations and perform the necessary validations and operations as described above.