# API Documentation: Update User Role

## Endpoint: `/update-user-role`

### Method: `PUT`

### Description:
This endpoint allows a super-admin to update the role of a user. Only super-admins have the permission to perform this action.

### Request Headers:
- `Authorization`: `Bearer <token>` (JWT token for authentication)
- `Content-Type`: `application/json`

### Request Body:
```json
{
  "userId": "string",
  "newRole": "string"
}
```

| Field   | Type   | Description                      |
| ------- | ------ | -------------------------------- |
| userId  | string | The ID of the user to be updated.|
| newRole | string | The new role to be assigned.     |

### Response:
#### Success (200 OK):
- **Content-Type**: `application/json`

```json
{
  "success": true,
  "message": "User role updated successfully",
  "user": {
    "_id": "string",
    "firstName": "string",
    "lastName": "string",
    "email": "string",
    "mobileNum": "string",
    "role": "string",
    "dateOfBirth": "string",
    "addressId": "string",
    "personalInfoId": "string",
    "entityId": "string"
  }
}
```

#### Error (403 Forbidden):
- **Content-Type**: `application/json`

```json
{
  "success": false,
  "message": "Only super-admins can update user roles"
}
```

#### Error (404 Not Found):
- **Content-Type**: `application/json`

```json
{
  "success": false,
  "message": "User not found"
}
```

#### Error (500 Internal Server Error):
- **Content-Type**: `application/json`

```json
{
  "success": false,
  "message": "Internal Server Error"
}
```

### Error Handling:
- **403 Forbidden**: Returned if the requesting user is not a super-admin.
- **404 Not Found**: Returned if the user with the provided ID is not found.
- **500 Internal Server Error**: Returned if there is a server error or an unknown error occurs.

### Implementation Details:
- The function checks if the requesting user is a super-admin.
- It extracts the `userId` and `newRole` from the request body.
- It queries the database to find the user by their ID.
- If the user is found, it updates the user's role and saves the changes.
- If successful, it returns a 200 OK response with a success message and the updated user details.
- If any validation fails or an error occurs, it returns an appropriate error response.

### Example Request:
```bash
curl -X PUT https://yourapi.com/update-user-role \
-H "Authorization: Bearer your_jwt_token" \
-H "Content-Type: application/json" \
-d '{"userId":"60d0fe4f5311236168a109ca", "newRole":"admin"}'
```

### Example Success Response:
```json
{
  "success": true,
  "message": "User role updated successfully",
  "user": {
    "_id": "60d0fe4f5311236168a109ca",
    "firstName": "John",
    "lastName": "Doe",
    "email": "john.doe@example.com",
    "mobileNum": "1234567890",
    "role": "admin",
    "dateOfBirth": "1990-01-01",
    "addressId": "60d0fe4f5311236168a109cb",
    "personalInfoId": "60d0fe4f5311236168a109cc",
    "entityId": "60d0fe4f5311236168a109cd"
  }
}
```

### Example Error Responses:
#### Only Super-Admins Can Update Roles:
```json
{
  "success": false,
  "message": "Only super-admins can update user roles"
}
```

#### User Not Found:
```json
{
  "success": false,
  "message": "User not found"
}
```

#### Internal Server Error:
```json
{
  "success": false,
  "message": "Internal Server Error"
}
```

### Security Considerations:
- Ensure the requesting user's role is validated to confirm they are a super-admin.
- Use HTTPS to transmit sensitive information.
- Implement proper error handling to avoid exposing sensitive information.
- Log actions for auditing purposes, especially changes made by super-admins.