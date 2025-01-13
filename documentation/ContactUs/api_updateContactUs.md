# API Documentation

## Endpoint: Update Contact Us

### URL

`PUT /contact-us/:id`

### Description

This endpoint allows users to update an existing "Contact Us" form submission. At least one field must be provided for the update.

### Authentication

No authentication is required for this endpoint.

### Request Headers

No specific headers are required.

### Request Parameters

- **id** (string, required): The ID of the "Contact Us" form submission to be updated.

### Request Body

The request body must be in JSON format and include at least one of the following fields:

- **name** (string, optional): The name of the person submitting the form.
- **email** (string, optional): The email address of the person submitting the form.
- **phoneNumber** (string, optional): The phone number of the person submitting the form.
- **nameOfCompanyOrPlatform** (string, optional): The name of the company or platform.
- **message** (string, optional): The message or inquiry from the person submitting the form.

### Request Example

```json
{
  "name": "John Doe",
  "email": "johndoe@example.com",
  "phoneNumber": "123-456-7890",
  "nameOfCompanyOrPlatform": "Example Company",
  "message": "I would like to update my inquiry."
}
```

### Response

#### Success (200 OK)

If the "Contact Us" form submission is updated successfully, the server responds with a JSON object containing the success status and the updated form data.

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
    "message": "I would like to update my inquiry.",
    "createdAt": "2024-07-10T12:34:56.789Z",
    "updatedAt": "2024-07-10T12:34:56.789Z"
  }
}
```

#### Client Error (400 Bad Request)

If no fields are provided for the update, the server responds with an error message.

##### Response Example

```json
{
  "success": false,
  "message": "At least one field is required to update."
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

- **400**: No fields provided for the update.
- **500**: Internal server error.

### Controller Function

The `handleUpdateContactUs` function handles the updating of an existing "Contact Us" form submission and performs the necessary validations and operations as described above.