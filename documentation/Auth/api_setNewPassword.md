# API Documentation: Set New Password

## Endpoint: `/set-new-password`

### Method: `POST`

### Description:
This endpoint is used to set a new password for a user who has requested a password reset. The user provides the new password and a confirmation of the new password. The request must include a valid reset token.

### Request Headers:
- `Content-Type`: `application/json`

### Request Body:
```json
{
  "new_password": "string",
  "confirm_new_password": "string"
}
```

| Field                 | Type   | Description                                      |
| --------------------- | ------ | ------------------------------------------------ |
| new_password          | string | The new password for the user.                   |
| confirm_new_password  | string | Confirmation of the new password.                |

### Cookies:
- `token`: The reset password token stored in cookies.

### Response:
#### Success (200 OK):
- **Content-Type**: `application/json`

```json
{
  "success": true,
  "message": "Password reset successfully. User has been logged out."
}
```

#### Error (400 Bad Request):
- **Content-Type**: `application/json`

```json
{
  "success": false,
  "field": "new_password",
  "error": "The new password should have at least one uppercase letter, one lowercase letter, one number and one special character."
}
```

```json
{
  "success": false,
  "field": "confirm_new_password",
  "error": "New password and confirm password do not match."
}
```

```json
{
  "error": "All fields are required."
}
```

#### Error (401 Unauthorized):
- **Content-Type**: `application/json`

```json
{
  "error": "Unauthorized. Token missing."
}
```

```json
{
  "error": "Link Expired or has already been used."
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
- **400 Bad Request**: Returned if the new password or confirm password fields are missing, if the new password is not strong enough, or if the new password and confirm password do not match.
- **401 Unauthorized**: Returned if the token is missing or invalid, or if the reset link has expired or already been used.
- **500 Internal Server Error**: Returned if there is a server error or an unknown error occurs.

### Implementation Details:
- The function retrieves the new password and confirm password from the request body.
- It checks if both fields are present.
- It verifies the reset token from the cookies.
- It retrieves the user associated with the token from the database.
- It checks if the reset token matches the token stored in the user's document.
- It verifies the strength of the new password using a regular expression.
- It checks if the new password and confirm password match.
- It updates the user's password and clears the reset token.
- It logs out the user by clearing the token cookie.
- If successful, it returns a 200 OK response with a success message.
- If any validation fails or an error occurs, it returns an appropriate error response.

### Example Request:
```bash
curl -X POST https://yourapi.com/set-new-password \
-H "Content-Type: application/json" \
-d '{"new_password":"NewPassword123!", "confirm_new_password":"NewPassword123!"}' \
--cookie "token=your_reset_token"
```

### Example Success Response:
```json
{
  "success": true,
  "message": "Password reset successfully. User has been logged out."
}
```

### Example Error Responses:
#### All Fields Required:
```json
{
  "error": "All fields are required."
}
```

#### Token Missing:
```json
{
  "error": "Unauthorized. Token missing."
}
```

#### Link Expired or Used:
```json
{
  "error": "Link Expired or has already been used."
}
```

#### Password Strength:
```json
{
  "success": false,
  "field": "new_password",
  "error": "The new password should have at least one uppercase letter, one lowercase letter, one number and one special character."
}
```

#### Password Mismatch:
```json
{
  "success": false,
  "field": "confirm_new_password",
  "error": "New password and confirm password do not match."
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
- Ensure the reset password token is securely generated and stored.
- Use HTTPS to transmit sensitive information.
- Implement proper error handling to avoid exposing sensitive information.
- Ensure the reset password URL is valid for a limited time (e.g., 15 minutes) to mitigate risks.

### Additional Information:
- The reset password token is generated using `jwt.sign` and is stored in the user's document in the database.
- The `sendEmail` function is used to send the email with the reset password instructions.