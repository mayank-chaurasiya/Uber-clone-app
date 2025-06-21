# Backend API Documentation

## POST `/users/register`

Registers a new user in the system.

### Request Body

Send a JSON object with the following structure:

```json
{
  "fullname": {
    "firstname": "string (min 3 chars, required)",
    "lastname": "string (min 3 chars, optional)"
  },
  "email": "string (valid email, required)",
  "password": "string (min 6 chars, required)"
}
```

#### Example

```json
{
  "fullname": {
    "firstname": "John",
    "lastname": "Doe"
  },
  "email": "john.doe@example.com",
  "password": "securePassword123"
}
```

### Responses

- **201 Created**
  - User registered successfully.
  - Returns a JSON object with a JWT token and the user data.
  - Example:
    ```json
    {
      "token": "jwt_token_here",
      "user": {
        "_id": "user_id_here",
        "fullname": {
          "firstname": "John",
          "lastname": "Doe"
        },
        "email": "john.doe@example.com",
        "socketId": null
      }
    }
    ```

- **400 Bad Request**
  - Validation failed (e.g., missing fields, invalid email, short password).
  - Returns an array of error messages.
  - Example:
    ```json
    {
      "errors": [
        {
          "msg": "First name must be at least 3 characters long.",
          "param": "fullname.firstname",
          "location": "body"
        }
      ]
    }
    ```

---

**Note:**  
- All fields marked as required must be present in the request body.
- The password is stored securely (hashed) and not returned in the response.