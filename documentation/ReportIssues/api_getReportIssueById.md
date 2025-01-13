# API Documentation

## Endpoint: Get Report Issue by ID

### URL

`GET /report-issue/:id`

### Description

This endpoint allows authenticated users to retrieve a specific report issue entry by its ID. Only the user who created the report or an admin can access it.

### Authentication

This endpoint requires the user to be authenticated.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Request Parameters

- **id** (string, required): The ID of the report issue to be retrieved.

### Request Example

```
GET /report-issue/60d9c6b0f1b4d72a8c8b4567
```

### Response

#### Success (200 OK)

If the report issue is retrieved successfully, the server responds with a JSON object containing the success status and the report issue data.

##### Response Example

```json
{
  "success": true,
  "issue": {
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

#### Client Error (403 Forbidden)

If a user attempts to access a report issue that they did not create, the server responds with a forbidden error message.

##### Response Example

```json
{
  "success": false,
  "message": "You cannot access this feedback"
}
```

#### Client Error (404 Not Found)

If the report issue with the specified ID is not found, the server responds with a not found error message.

##### Response Example

```json
{
  "success": false,
  "message": "Reported Issue not found"
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

- **403**: You cannot access this feedback.
- **404**: Reported Issue not found.
- **500**: Internal server error.

### Controller Function

The `getReportIssueById` function handles the retrieval of a report issue entry by its ID and performs the necessary validations and operations as described above. Only the user who created the report or an admin can access it.