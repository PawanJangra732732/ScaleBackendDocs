# API Documentation

## Endpoint: Get Contact Us by ID

### URL

`GET /contact-us/:id`

### Description

This endpoint allows users to retrieve a specific "Contact Us" form submission by its ID. The response includes the details of the specified submission.

### Authentication

No authentication is required for this endpoint.

### Request Headers

No specific headers are required.

### Request Parameters

- **id** (string, required): The ID of the "Contact Us" form submission to be retrieved.

### Request Example

```
GET /contact-us/60d9c6b0f1b4d72a8c8b4567
```

### Response

#### Success (200 OK)

If the "Contact Us" form submission is retrieved successfully, the server responds with a JSON object containing the success status and the submission data.

##### Response Example

```json
{
  "success": true,
  "data": {
    "_id": "60d9c6b0f1b4d72a8c8b4567",
    "name": "John Doe",
    "email": "johndoe@example.com",
    "phoneNumber": "123-456-7890",
    "nameOfCompanyOrPlatform": "Example Company",
    "message": "I would like to inquire about your services.",
    "createdAt": "2024-07-10T12:34:56.789Z",
    "updatedAt": "2024-07-10T12:34:56.789Z"
  }
}
```

#### Client Error (404 Not Found)

If the "Contact Us" form submission with the specified ID is not found, the server responds with a not found error message.

##### Response Example

```json
{
  "success": false,
  "message": "Contact not found"
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

- **404**: Contact not found.
- **500**: Internal server error.

### Controller Function

The `getContactUsById` function handles the retrieval of a specific "Contact Us" form submission by its ID and performs the necessary validations and operations as described above.