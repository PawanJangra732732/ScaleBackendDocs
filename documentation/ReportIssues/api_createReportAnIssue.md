# API Documentation

## Endpoint: Create Report Issue

### URL

`POST /report-issue`

### Description

This endpoint allows authenticated users to create a report issue entry. The report includes details such as the user ID, entity ID, and other relevant information.

### Authentication

This endpoint requires the user to be authenticated.

### Request Headers

- **Authorization**: Bearer token for authenticated user.
- **Cookie**: Contains the access token.

### Request Body

The request body must be in JSON format and include the necessary fields to report an issue. The fields will vary depending on the issue being reported but must pass validation.

### Request Example

```json
{
  "title": "Issue with the service",
  "description": "I encountered an issue with the service.",
  "priority": "high"
}
```

### Response

#### Success (201 Created)

If the report issue is created successfully, the server responds with a JSON object containing the success status and the report issue data.

##### Response Example

```json
{
  "success": true,
  "reportAnIssue": {
    "_id": "60d9c6b0f1b4d72a8c8b4567",
    "userId": "60d9c6b0f1b4d72a8c8b4568",
    "entityId": "60d9c6b0f1b4d72a8c8b4569",
    "title": "Issue with the service",
    "description": "I encountered an issue with the service.",
    "priority": "high",
    "createdAt": "2024-07-10T12:34:56.789Z",
    "updatedAt": "2024-07-10T12:34:56.789Z"
  }
}
```

#### Client Error (400 Bad Request)

If there are validation errors in the provided report issue data, the server responds with an error message.

##### Response Example

```json
{
  "success": false,
  "message": "Validation errors",
  "errors": ["Title is required", "Description is required"]
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

- **400**: Validation errors.
- **401**: Authentication token not found.
- **500**: Internal server error.

### Controller Function

The `createReportIssue` function handles the creation of a report issue entry for an authenticated user. It performs the necessary validations and operations as described above.