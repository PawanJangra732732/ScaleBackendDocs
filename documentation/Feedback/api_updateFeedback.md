# API Documentation: Update Feedback

## Endpoint: `/feedback/:id`

### Method: `PUT`

### Description:
This endpoint allows authenticated users to update feedback. Users can only update their own feedback, while admins can update any feedback.

### Request Headers:
- `Authorization`: `Bearer <token>` (JWT token for authentication)
- `Content-Type`: `application/json`

### Request Parameters:
- `id`: `string` (Feedback ID)

### Request Body:
- Any fields from the `FeedbackSchema` that need to be updated.

### Response:
#### Success (200 OK):
- **Content-Type**: `application/json`

```json
{
  "success": true,
  "feedback": {
    "_id": "string",
    "userId": "string",
    "comment": "string",
    "rating": "number",
    // Include other feedback fields as necessary
  }
}
```

#### Error (403 Forbidden):
- **Content-Type**: `application/json`

```json
{
  "success": false,
  "message": "You cannot update this feedback"
}
```

#### Error (404 Not Found):
- **Content-Type**: `application/json`

```json
{
  "success": false,
  "message": "Feedback not found"
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
- **403 Forbidden**: Returned if a user tries to update feedback that does not belong to them.
- **404 Not Found**: Returned if the feedback with the provided ID is not found.
- **500 Internal Server Error**: Returned if there is a server error or an unknown error occurs.

### Implementation Details:
- The function retrieves the feedback ID from the request parameters.
- It checks if the feedback exists in the database.
- If the requesting user is a regular user, it verifies that the feedback belongs to them.
- It updates the feedback with the new data provided in the request body.
- If successful, it returns a 200 OK response with the updated feedback details.
- If any validation fails or an error occurs, it returns an appropriate error response.

### Example Request:
```bash
curl -X PUT https://yourapi.com/feedback/60d0fe4f5311236168a109ca \
-H "Authorization: Bearer your_jwt_token" \
-H "Content-Type: application/json" \
-d '{"comment":"Updated feedback comment", "rating":5}'
```

### Example Success Response:
```json
{
  "success": true,
  "feedback": {
    "_id": "60d0fe4f5311236168a109ca",
    "userId": "60d0fe4f5311236168a109cb",
    "comment": "Updated feedback comment",
    "rating": 5
    // Include other feedback fields as necessary
  }
}
```

### Example Error Responses:
#### User Cannot Update This Feedback:
```json
{
  "success": false,
  "message": "You cannot update this feedback"
}
```

#### Feedback Not Found:
```json
{
  "success": false,
  "message": "Feedback not found"
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
- Ensure the requesting user's role and ownership of the feedback are validated.
- Use HTTPS to transmit sensitive information.
- Implement proper error handling to avoid exposing sensitive information.
- Log actions for auditing purposes, especially changes made by users and admins.