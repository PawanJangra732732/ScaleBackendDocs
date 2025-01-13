### API Documentation: Forgot Password Endpoint

#### Endpoint
`POST /api/auth/forgot-password`

#### Description
This endpoint handles user requests to reset their password. When a user requests a password reset, an email with reset instructions and a secure token is sent to their registered email address.

#### Request

##### Headers
- `Content-Type: application/json`

##### Body
- `email` (string, required): The email address associated with the user account.

##### Example Request
```json
{
  "email": "user@example.com"
}
```

#### Response

##### Success Response
- **Status Code:** 200 OK
- **Body:**
  ```json
  {
    "success": true,
    "message": "Email sent to user@example.com successfully"
  }
  ```

##### Error Responses
- **User Not Found**
  - **Status Code:** 404 Not Found
  - **Body:**
    ```json
    {
      "success": false,
      "message": "User Not Found"
    }
    ```

- **Internal Server Error**
  - **Status Code:** 500 Internal Server Error
  - **Body:**
    ```json
    {
      "success": false,
      "message": "Internal Server Error"
    }
    ```

#### Implementation Details

**Function Name:** `handleForgotPassword`

**Function Definition:**
```javascript
exports.handleForgotPassword = catchAsyncErrors(async (req, res, next) => {
  const { email } = req.body;

  const user = await User.findOne({ email });

  if (!user) {
    return next(new ErrorHandler("User Not Found", 404));
  }

  try {
    // Generate reset password token
    const token = jwt.sign(
      { userId: user._id },
      process.env.RESET_PASSWORD_TOKEN_SECRET,
      {
        expiresIn: process.env.RESET_PASSWORD_EXPIRE,
      }
    );

    user.resetPasswordToken = token;
    await user.save();

    // Construct reset password URL
    const resetPasswordUrl = `${process.env.FRONTEND_URL}/api/set-new-password?token=${token}`;

    // Compose email message
    const message = `Dear User,\n\nWe have received a request to reset your account password.\n\nClick on the link below to reset your password:\n\n${resetPasswordUrl}\n\nAlternatively, you can copy and paste this link in your browser.\n\nThis link will be valid for 15 minutes.\n\nIgnore this email if you did not ask for a password reset.\n\nThank you,\n\nTeam Scale Healthcare.`;

    // Send email with reset password instructions
    await sendEmail({
      email: user.email,
      subject: "Reset your password",
      message,
    });

    // Respond with success message
    return res.status(200).json({
      success: true,
      message: `Email sent to ${user.email} successfully`,
    });
  } catch (error) {
    await user.save({ validateBeforeSave: false });
    // Return JSON format error
    res.status(error.statusCode || 500).json({
      success: false,
      message: error.message || "Internal Server Error",
    });
  }
});
```

### Key Points

- **Token Generation:** The token is generated using `jwt.sign` and includes the user ID. It is signed with a secret key and has an expiration time defined in the environment variables.
- **URL Construction:** The reset password URL is constructed using the frontend URL from the environment variables.
- **Email Composition:** The email message includes instructions and the reset password link.
- **Error Handling:** The function includes error handling for cases where the user is not found and for internal server errors during email sending.

#### Call-to-Action
For further assistance or queries, please contact our support team. If you encounter any issues with the password reset process, let us know, and we’ll be happy to help! 💪📧

---
