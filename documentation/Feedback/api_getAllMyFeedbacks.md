# API Documentation

## Endpoint: Get All My Feedbacks

### URL

`GET /my-feedbacks`

### Description

This endpoint allows authenticated users to retrieve all their own feedback entries with pagination and search functionality. The response includes paginated feedback entries and additional pagination details.

### Authentication

This endpoint requires the user to be authenticated.

### Request Headers

- **Authorization**: Bearer token for authenticated user.

### Query Parameters

- **page** (integer, optional): The page number to retrieve. Defaults to 1.
- **pageSize** (integer, optional): The number of feedback entries per page. Defaults to 10.
- **q** (string, optional): A search term to filter feedback entries by their name or email.

### Request Example

```
GET /my-feedbacks?page=1&pageSize=10&q=john
```

### Response

#### Success (200 OK)

If the feedback entries are retrieved successfully, the server responds with a JSON object containing the success status, paginated feedback entries, and pagination details.

##### Response Example

```json
{
  "success": true,
  "data": [
    {
      "_id": "60d9c6b0f1b4d72a8c8b4567",
      "name": "John Doe",
      "email": "johndoe@example.com",
      "rating": 5,
      "feedback": "Great service!",
      "createdAt": "2024-07-10T12:34:56.789Z",
      "updatedAt": "2024-07-10T12:34:56.789Z"
    },
    {
      "_id": "60d9c6b0f1b4d72a8c8b4568",
      "name": "Jane Smith",
      "email": "janesmith@example.com",
      "rating": 4,
      "feedback": "Good experience overall.",
      "createdAt": "2024-07-11T12:34:56.789Z",
      "updatedAt": "2024-07-11T12:34:56.789Z"
    }
  ],
  "totalResults": 2,
  "totalPages": 1,
  "currentPage": 1
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

- **500**: Internal server error.

### Controller Function

The `getAllMyFeedbacks` function handles the retrieval of all feedback entries associated with the authenticated user. It performs the necessary operations as described above, including pagination and search functionality.