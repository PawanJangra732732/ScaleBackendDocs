# User Registration API Documentation

## Endpoint: User Registration

This endpoint handles the registration of a new user. The request should be made to the endpoint with the necessary user information.

### URL

`/api/register`

### Method

`POST`

### Request Headers

- `Content-Type: application/json`
- `Authorization: Bearer <token>`

### Request Body

The request body should be a JSON object containing the following fields:

| Field                   | Type   | Required | Description                                 |
| ----------------------- | ------ | -------- | ------------------------------------------- |
| `firstName`             | String | Yes      | User's first name                           |
| `lastName`              | String | No       | User's last name                            |
| `email`                 | String | Yes      | User's email address                        |
| `dateOfBirth`           | String | Yes      | User's date of birth in `YYYY-MM-DD` format |
| `password`              | String | Yes      | User's password                             |
| `role`                  | String | Yes      | User's role (`admin` or `user`)             |
| `entityId`              | String | Yes      | Entity ID associated with the user          |
| `primaryAddressLine1`   | String | No       | Primary address line 1                      |
| `primaryAddressLine2`   | String | No       | Primary address line 2                      |
| `primaryCity`           | String | No       | Primary city                                |
| `primaryState`          | String | No       | Primary state                               |
| `primaryPostalCode`     | String | No       | Primary postal code                         |
| `primaryCountry`        | String | No       | Primary country                             |
| `secondaryAddressLine1` | String | No       | Secondary address line 1                    |
| `secondaryAddressLine2` | String | No       | Secondary address line 2                    |
| `secondaryCity`         | String | No       | Secondary city                              |
| `secondaryState`        | String | No       | Secondary state                             |
| `secondaryPostalCode`   | String | No       | Secondary postal code                       |
| `secondaryCountry`      | String | No       | Secondary country                           |
| `primaryPhoneNumber`    | String | No       | Primary phone number                        |
| `secondaryPhoneNumber`  | String | No       | Secondary phone number                      |
| `faxNumber`             | String | No       | Fax number                                  |
| `website`               | String | No       | User's website                              |

### Response

#### Success Response

- **Status Code:** `201 Created`
- **Content:**
  ```json
  {
    "success": true,
    "message": "User registered successfully",
    "data": {
      "user": {
        "_id": "string",
        "firstName": "string",
        "lastName": "string",
        "email": "string",
        "dateOfBirth": "string",
        "role": "string",
        "entityId": "string",
        "address": "object",
        "personalInfo": "object"
      }
    }
  }
  ```

#### Error Responses

- **400 Bad Request**
  - This status code is returned if required fields are missing or invalid.
  - **Example:**
    ```json
    {
      "success": false,
      "field": "email",
      "error": "please enter email address"
    }
    ```
- **409 Conflict**

  - This status code is returned if the email address is already in use.
  - **Example:**
    ```json
    {
      "success": false,
      "message": "Email address is already in use."
    }
    ```

- **500 Internal Server Error**
  - This status code is returned for any unexpected server errors.
  - **Example:**
    ```json
    {
      "success": false,
      "message": "Internal Server Error"
    }
    ```

### Notes

- **Admin User:** If the authenticated user is an admin, the `entityId` will be automatically assigned to the user being registered.
- **Validation:** All required fields must be provided in the request body. If any required field is missing, the server will respond with a `400 Bad Request` status code indicating the missing field.
- **Unique Email:** The email address must be unique. If the email is already in use, the server will respond with a `409 Conflict` status code.

### Example Request

````json
{
  "firstName": "John",
  "lastName": "Doe",
  "email": "john.doe@example.com",
  "dateOfBirth": "1990-01-01",
  "password": "password123",
  "role": "user",
  "entityId": "entity123",
  "primaryAddressLine1": "123 Main St",
  "primaryCity": "Anytown",
  "primaryState": "Anystate",
  "primaryPostalCode": "12345",
  "primaryCountry": "USA",
  "primaryPhoneNumber": "123-456-7890"
}

### Example Success Response

```json
{
  "success": true,
  "message": "User registered successfully",
  "data": {
    "user": {
      "_id": "60e6b7f10a1e0c001c8e4e5b",
      "firstName": "John",
      "lastName": "Doe",
      "email": "john.doe@example.com",
      "dateOfBirth": "1990-01-01",
      "role": "user",
      "entityId": "entity123",
      "address": {
        "primaryAddress": {
          "addressLine1": "123 Main St",
          "city": "Anytown",
          "state": "Anystate",
          "postalCode": "12345",
          "country": "USA"
        }
      },
      "personalInfo": {
        "primaryPhoneNumber": "123-456-7890",
        "secondaryPhoneNumber": "",
        "faxNumber": "",
        "website": ""
      }
    }
  }
}