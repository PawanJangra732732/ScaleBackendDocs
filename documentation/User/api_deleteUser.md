# API Documentation for `handleDeleteUser`

## Description

The `handleDeleteUser` endpoint allows an authenticated admin or superadmin to delete a user from the system. This operation also deletes associated personal information and address records. The endpoint ensures that only superadmins can delete other superadmins and that admins can only delete users within their own entity.

## Endpoint

```
DELETE /api/v1/admin/user
```

## Request Headers

- `Content-Type: application/json`
- `Authorization: Bearer <JWT_TOKEN>` (JWT token for authentication)

## Request Body

The request body must be in JSON format and include the following field:

| Field   | Type   | Description                   |
|---------|--------|-------------------------------|
| `userId`| String | The ID of the user to delete. |

### Example Request

```json
{
  "userId": "60d21b4667d0d8992e610c85"
}
```

## Response

### Success Response

- **Status Code:** `200 OK`
- **Body:**

```json
{
  "success": true,
  "message": "User 60d21b4667d0d8992e610c85 deleted successfully"
}
```

### Error Responses

- **Status Code:** `401 Unauthorized`
  - **Body:** If the authentication token is missing or invalid.
  
  ```json
  {
    "success": false,
    "message": "Authentication token not found"
  }
  ```

- **Status Code:** `403 Forbidden`
  - **Body:** If the admin and user do not belong to the same entity, or if a non-superadmin tries to delete a superadmin.
  
  ```json
  {
    "success": false,
    "message": "Not allowed: Admin and user must belong to the same entity"
  }
  ```

  - **Body:** If a non-superadmin tries to delete a superadmin.
  
  ```json
  {
    "success": false,
    "message": "Not allowed: Only superadmins can delete other superadmins"
  }
  ```

- **Status Code:** `404 Not Found`
  - **Body:** If the admin user or the user to be deleted is not found.
  
  ```json
  {
    "success": false,
    "message": "Admin user not found"
  }
  ```

  - **Body:** If the user to be deleted is not found.
  
  ```json
  {
    "success": false,
    "message": "User not found"
  }
  ```

- **Status Code:** `500 Internal Server Error`
  - **Body:** If there is an internal server error.
  
  ```json
  {
    "success": false,
    "message": "Internal Server Error"
  }
  ```

## Notes

- This endpoint requires admin or superadmin privileges.
- Ensure the JWT token is provided in the `Authorization` header to authenticate the request.
- The endpoint uses MongoDB transactions to ensure atomicity in deleting user and related records.

---

This API endpoint is part of the admin functionalities, allowing admins and superadmins to manage user accounts by enabling them to delete users securely while maintaining data integrity with transaction handling.