# API Documentation

## Endpoint: Get Details of Entity Profile

### URL

`GET /entity/details`

### Description

This endpoint allows authenticated users to retrieve the details of their own entity profile based on the authentication token.

### Authentication

This endpoint requires the user to be authenticated.

### Request Headers

- **Authorization**: Bearer token for authenticated user.
- **Cookie**: Contains the access token.

### Request Example

```
GET /entity/details
```

### Response

#### Success (200 OK)

If the entity details are retrieved successfully, the server responds with a JSON object containing the success status and the entity data.

##### Response Example

```json
{
  "success": true,
  "data": {
    "_id": "60d9c6b0f1b4d72a8c8b4567",
    "entityName": "Example Entity",
    "createdAt": "2024-07-10T12:34:56.789Z",
    "updatedAt": "2024-07-10T12:34:56.789Z"
  }
}
```

#### Client Error (401 Unauthorized)

If the authentication token is not found, the server responds with an unauthorized error message.

##### Response Example

```json
{
  "success": false,
  "message": "Authentication token not found"
}
```

#### Client Error (404 Not Found)

If the entity associated with the authenticated user is not found, the server responds with a not found error message.

##### Response Example

```json
{
  "success": false,
  "message": "Entity not found"
}
```

#### Server Error (500 Internal Server Error)

If there is an internal server error, the server responds with an error message.

##### Response Example

```json
{
  "success": false,
  "message": "Internal Server Error"
}
```

### Errors

- **401**: Authentication token not found.
- **404**: Entity not found.
- **500**: Internal server error.

### Controller Function

The `handleGetDetailsOfEntityProfile` function handles the retrieval of the authenticated user's entity profile based on the authentication token and performs the necessary validations and operations as described above.