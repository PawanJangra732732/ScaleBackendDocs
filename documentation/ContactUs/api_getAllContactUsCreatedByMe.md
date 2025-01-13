# API Documentation

## Endpoint: Get All Contact Us Submissions

### URL

`GET /contact-us`

### Description

This endpoint allows users to retrieve all "Contact Us" form submissions. The response includes the details of all submissions.

### Authentication

No authentication is required for this endpoint.

### Request Headers

No specific headers are required.

### Request Example

```
GET /contact-us
```

### Response

#### Success (200 OK)

If the "Contact Us" form submissions are retrieved successfully, the server responds with a JSON object containing the success status and the data of all submissions.

##### Response Example

```json
{
  "success": true,
  "data": [
    {
      "_id": "60d9c6b0f1b4d72a8c8b4567",
      "name": "John Doe",
      "email": "johndoe@example.com",
      "phoneNumber": "123-456-7890",
      "nameOfCompanyOrPlatform": "Example Company",
      "message": "I would like to inquire about your services.",
      "createdAt": "2024-07-10T12:34:56.789Z",
      "updatedAt": "2024-07-10T12:34:56.789Z"
    },
    {
      "_id": "60d9c6b0f1b4d72a8c8b4568",
      "name": "Jane Smith",
      "email": "janesmith@example.com",
      "phoneNumber": "987-654-3210",
      "nameOfCompanyOrPlatform": "Another Company",
      "message": "I have a question about your product.",
      "createdAt": "2024-07-11T12:34:56.789Z",
      "updatedAt": "2024-07-11T12:34:56.789Z"
    }
  ]
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

The `GetAllContactUsCreatedByMe` function handles the retrieval of all "Contact Us" form submissions and performs the necessary operations as described above.