# User Login API

API endpoint for user authentication and login.

## Endpoint

`POST /api/login`

## Description

This endpoint handles user authentication and login. It verifies the user's credentials (email and password), generates access and refresh tokens upon successful login, and sets cookies for token storage.

## Parameters

| Parameter | Type   | Description                    |
|-----------|--------|--------------------------------|
| email     | String | User's email address.          |
| password  | String | User's password.               |

## Returns

Upon successful login:
- `200 OK` along with `accessToken` and `refreshToken` cookies set in the response headers.
- JSON response body:
  ```json
  {
    "success": true,
    "data": {
      "message": "Logged in successfully"
    }
  }

## Error Responses

### Validation Errors

If validation fails due to missing or invalid parameters:

- `401 Unauthorized` with a JSON response indicating the specific validation error:
  
  ```json
  {
    "success": false,
    "field": "email",
    "error": "Please enter an email"
  }

or

```json
{
  "success": false,
  "field": "password",
  "error": "Please provide a password"
}

## Authentication Errors
if authentication fails due to incorrect credentials
```json
{
  "success": false,
  "field": "password",
  "error": "Email or password is invalid"
}

## Server Errors
If there's an unexpected server error:
```json
{
  "success": false,
  "message": "Internal Server Error"
}

Notes
- Cookies `accessToken` and `refreshToken` are HTTP-only and secure.
- `accessToken` expires based on `ACCESS_TOKEN_MAX_AGE` environment variable.
- `refreshToken` expires based on `REFRESH_TOKEN_MAX_AGE` environment variable.
