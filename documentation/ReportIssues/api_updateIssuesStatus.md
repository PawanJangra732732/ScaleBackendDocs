# API Documentation

## Endpoint: Update Issue Status

### URL

`PUT /report-issue/:id/status`

### Description

This endpoint allows a superadmin to update the status of a specific report issue. The response includes the updated report issue with the new status.

### Authentication

This endpoint requires the user to be authenticated.

### Authorization

Only users with the role of `superadmin` are authorized to use this endpoint.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Request Parameters

- **id** (string, required): The ID of the report issue to be updated.

### Request Body

The request body must be in JSON format and include the following field:

- **status** (string, required): The new status for the report issue. Valid statuses are `submitted`, `accepted`, `resolved`, `analyzed`, and `Closed`.

### Request Example

```json
{
  "status": "resolved"
}
```

### Response

#### Success (200 OK)

If the issue status is updated successfully, the server responds with a JSON object containing the success status, a success message, and the updated issue.

##### Response Example

```json
{
  "success": true,
  "message": "Issue status updated to resolved",
  "issue": {
    "_id": "60d9c6b0f1b4d72a8c8b4567",
    "userId": "60d9c6b0f1b4d72a8c8b4568",
    "entityId": "60d9c6b0f1b4d72a8c8b4569",
    "title": "Issue with the service",
    "description": "I encountered an issue with the service.",
    "priority": "high",
    "status": "resolved",
    "createdAt": "2024-07-10T12:34:56.789Z",
    "updatedAt": "2024-07-10T12:34:56.789Z"
  }
}
```

#### Client Error (400 Bad Request)

If the provided status is invalid, the server responds with a bad request error message.

##### Response Example

```json
{
  "success": false,
  "message": "Invalid status"
}
```

#### Client Error (403 Forbidden)

If the user is not a superadmin, the server responds with a forbidden error message.

##### Response Example

```json
{
  "success": false,
  "message": "Only superadmin can update the issue status"
}
```

#### Client Error (404 Not Found)

If the report issue with the specified ID is not found, the server responds with a not found error message.

##### Response Example

```json
{
  "success": false,
  "message": "Issue not found"
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

- **400**: Invalid status.
- **403**: Only superadmin can update the issue status.
- **404**: Issue not found.
- **500**: Internal server error.

### Controller Function

The `updateIssueStatus` function handles the updating of a report issue's status for a superadmin. It performs the necessary validations and operations as described above.