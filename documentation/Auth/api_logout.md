# API Documentation: Logout User

## Endpoint: `/logout`

### Method: `POST`

### Description:
This endpoint is used to log out the user by clearing the refresh and access tokens stored in cookies. It invalidates the refresh token in the database and clears the cookies on the client side.

### Request Headers:
- `Content-Type`: `application/json`

### Request Body:
- None

### Cookies:
- `refreshToken`: The refresh token stored in cookies.

### Response:
#### Success (200 OK):
- **Content-Type**: `application/json`

```json
{
  "success": true,
  "message": "Logged out successfully."
}
```

#### Error (400 Bad Request):
- **Content-Type**: `application/json`

```json
{
  "success": false,
  "message": "No refresh token found in cookies."
}
```

#### Error (404 Not Found):
- **Content-Type**: `application/json`

```json
{
  "success": false,
  "message": "User not found."
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
- **400 Bad Request**: Returned if no refresh token is found in the cookies.
- **404 Not Found**: Returned if no user is found with the provided refresh token.
- **500 Internal Server Error**: Returned if there is a server error or an unknown error occurs.

### Implementation Details:
- The function retrieves the refresh token from the cookies.
- It checks if the refresh token is present in the cookies.
- It finds the user associated with the refresh token in the database.
- It invalidates the refresh token by setting it to null in the user object and saves the user.
- It clears the `accessToken` and `refreshToken` cookies on the client side.
- If any validation fails, it returns an appropriate error response.

### Example Request:
```bash
curl -X POST https://yourapi.com/logout \
-H "Content-Type: application/json" \
--cookie "refreshToken=your_refresh_token"
```

### Example Success Response:
```json
{
  "success": true,
  "message": "Logged out successfully."
}
```

### Example Error Responses:
#### No Refresh Token Found:
```json
{
  "success": false,
  "message": "No refresh token found in cookies."
}
```

#### User Not Found:
```json
{
  "success": false,
  "message": "User not found."
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
- Ensure the cookies are transmitted over HTTPS.
- Use HTTP-only and secure flags for cookies to mitigate XSS attacks.
- Implement proper error handling to avoid exposing sensitive information.