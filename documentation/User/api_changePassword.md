# API Documentation for `handleChangePassword`

## Description

The `handleChangePassword` endpoint allows authenticated users to change their current password to a new password. The endpoint ensures that the current password is correct, the new password meets the required strength criteria, and that the new password and confirm password match. If the password change is successful, the user is logged out.

## Endpoint

```
POST /api/v1/auth/change-password
```

## Request Headers

- `Content-Type: application/json`
- `Cookie: accessToken=<JWT_TOKEN>` (JWT token for authentication)

## Request Body

The request body must be in JSON format and include the following fields:

| Field                | Type   | Description                                       |
|----------------------|--------|---------------------------------------------------|
| `current_password`   | String | The current password of the user.                 |
| `new_password`       | String | The new password the user wants to set.           |
| `confirm_new_password`| String | Confirmation of the new password.                 |

### Example Request

```json
{
  "current_password": "CurrentPassword123!",
  "new_password": "NewPassword123!",
  "confirm_new_password": "NewPassword123!"
}
```

## Response

### Success Response

- **Status Code:** `200 OK`
- **Body:**

```json
{
  "success": true,
  "message": "Password reset successfully. User has been logged out"
}
```

### Error Responses

- **Status Code:** `400 Bad Request`
  - **Body:** If any required field is missing.
  
  ```json
  {
    "error": "All fields are required."
  }
  ```

  - **Body:** If the new password is the same as the current password.
  
  ```json
  {
    "success": false,
    "field": "new_password",
    "error": "new password cannot be same as the current password"
  }
  ```

  - **Body:** If the new password does not meet strength criteria.
  
  ```json
  {
    "success": false,
    "field": "new_password",
    "error": "The new password should have at least one uppercase letter, one lowercase letter, one number and one special character"
  }
  ```

  - **Body:** If the new password and confirm password do not match.
  
  ```json
  {
    "success": false,
    "field": "confirm_new_password",
    "error": "New password and confirm password do not match."
  }
  ```

- **Status Code:** `401 Unauthorized`
  - **Body:** If the token is missing or invalid.
  
  ```json
  {
    "error": "Unauthorized. Token missing."
  }
  ```

  - **Body:** If the current password is incorrect.
  
  ```json
  {
    "success": false,
    "field": "current_password",
    "error": "Incorrect current password."
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

- The endpoint requires authentication. The user's JWT token should be included in the request cookies.
- The new password must meet the following strength criteria: 
  - At least one uppercase letter
  - At least one lowercase letter
  - At least one number
  - At least one special character
  - Minimum length of 8 characters

---

This API endpoint is part of a secure authentication system, ensuring that users can change their passwords securely while adhering to best practices for password complexity and validation.