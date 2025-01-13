# API Documentation

## Endpoint: Create Contact Us

### URL

`POST /contact-us`

### Description

This endpoint allows users to submit a "Contact Us" form. The form includes details such as name, email, phone number, company or platform name, and a message. All fields are required.

### Authentication

No authentication is required for this endpoint.

### Request Headers

No specific headers are required.

### Request Body

The request body must be in JSON format and include the following fields:

- **name** (string, required): The name of the person submitting the form.
- **email** (string, required): The email address of the person submitting the form.
- **phoneNumber** (string, required): The phone number of the person submitting the form.
- **nameOfCompanyOrPlatform** (string, required): The name of the company or platform.
- **message** (string, required): The message or inquiry from the person submitting the form.

### Request Example

```json
{
  "name": "John Doe",
  "email": "johndoe@example.com",
  "phoneNumber": "123-456-7890",
  "nameOfCompanyOrPlatform": "Example Company",
  "message": "I would like to inquire about your services."
}
```

### Response

#### Success (201 Created)

If the "Contact Us" form is submitted successfully, the server responds with a JSON object containing the success status and the submitted form data.

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

#### Client Error (400 Bad Request)

If any required fields are missing, the server responds with an error message specifying the missing field.

##### Response Example

```json
{
  "success": false,
  "field": "name",
  "error": "please enter name"
}
```

##### Response Example

```json
{
  "success": false,
  "field": "email",
  "error": "please enter email address"
}
```

##### Response Example

```json
{
  "success": false,
  "field": "phoneNumber",
  "error": "please enter phoneNumber"
}
```

##### Response Example

```json
{
  "success": false,
  "field": "nameOfCompanyOrPlatform",
  "error": "please enter Platform or company name"
}
```

##### Response Example

```json
{
  "success": false,
  "field": "message",
  "error": "please enter message"
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

- **400**: Missing required fields.
- **500**: Internal server error.

### Controller Function

The `handleCreateContactUs` function handles the submission of the "Contact Us" form and performs the necessary validations and operations as described above.