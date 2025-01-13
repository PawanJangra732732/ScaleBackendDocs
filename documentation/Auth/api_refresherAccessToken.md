# API Documentation: Refresh Access Token

## Endpoint: `/refresh-token`

### Method: `POST`

### Description:
This endpoint is used to refresh the access token using a valid refresh token. The refresh token must be provided in the request body. Upon successful validation, new access and refresh tokens are generated and returned to the client.

### Request Headers:
- `Content-Type`: `application/json`

### Request Body:
```json
{
  "refreshToken": "string"
}
```

| Field         | Type   | Description                     |
| ------------- | ------ | ------------------------------- |
| refreshToken  | string | The refresh token for the user. |

### Response:
#### Success (200 OK):
- **Content-Type**: `application/json`
- **Set-Cookie**: 
  - `accessToken`: The new access token, HTTP only, secure.
  - `refreshToken`: The new refresh token, HTTP only, secure.

```json
{
  "success": true,
  "message": "Access token refreshed",
  "data": {
    "accessToken": "string",
    "refreshToken": "string"
  }
}
```

#### Error (401 Unauthorized):
- **Content-Type**: `application/json`

```json
{
  "success": false,
  "message": "Unauthorized request"
}
```

#### Error (401 Unauthorized - Invalid Token):
- **Content-Type**: `application/json`

```json
{
  "success": false,
  "message": "Refresh token invalid"
}
```

### Error Handling:
- **401 Unauthorized**: Returned if the refresh token is missing, expired, or invalid.
- **401 Unauthorized**: Returned if the refresh token does not match the stored token in the user object.

### Implementation Details:
- The function uses `jwt.verify` to validate the incoming refresh token.
- It retrieves the user associated with the decoded token ID from the database.
- It securely compares the incoming refresh token with the stored refresh token.
- It generates new access and refresh tokens using `generateAccessAndRefreshTokens`.
- It sets the new tokens in HTTP-only, secure cookies.
- If any validation fails, it returns a 401 Unauthorized error with an appropriate message.

### Example Request:
```bash
curl -X POST https://yourapi.com/refresh-token \
-H "Content-Type: application/json" \
-d '{"refreshToken":"your_refresh_token"}'
```

### Example Success Response:
```json
{
  "success": true,
  "message": "Access token refreshed",
  "data": {
    "accessToken": "new_access_token",
    "refreshToken": "new_refresh_token"
  }
}
```

### Example Error Response:
```json
{
  "success": false,
  "message": "Unauthorized request"
}
```

### Security Considerations:
- Ensure the refresh token is stored securely and transmitted over HTTPS.
- Use HTTP-only and secure flags for cookies to mitigate XSS attacks.
- Implement proper error handling to avoid exposing sensitive information.