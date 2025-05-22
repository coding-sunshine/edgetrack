# Authentication API Documentation

The Authentication API provides endpoints for user registration and login.

## Endpoints

### POST /api/auth/signup

Creates a new user account in the system.

**Example Request:**
```
POST /api/auth/signup
```

**Request Body:**
```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "password123",
  "role": "orgowner"
}
```

**Example Response:**
```json
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "data": {
    "user": {
      "_id": "60d21b4667d0d8992e610c90",
      "name": "John Doe",
      "email": "john@example.com",
      "role": "orgowner",
      "createdAt": "2023-06-23T12:34:56.789Z",
      "isPro": false,
      "planInfo": {
        "planType": "free"
      }
    }
  }
}
```

---

### POST /api/auth/login

Authenticates a user and provides a JWT token for accessing protected routes.

**Example Request:**
```
POST /api/auth/login
```

**Request Body:**
```json
{
  "email": "john@example.com",
  "password": "password123"
}
```

**Example Response:**
```json
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "data": {
    "user": {
      "_id": "60d21b4667d0d8992e610c90",
      "name": "John Doe",
      "email": "john@example.com",
      "role": "orgowner",
      "createdAt": "2023-06-23T12:34:56.789Z",
      "isPro": false,
      "planInfo": {
        "planType": "free"
      }
    }
  }
}
```

-----------------------------------------------------------

## Using Authentication Token

After successful login or signup, you will receive a JWT token that should be used for accessing protected routes:

1. Copy the token from the response
2. Include it in subsequent requests in the Authorization header:
   ```
   Authorization: Bearer <YOUR_JWT_TOKEN>
   ```

---

## Error Responses

### Invalid Credentials

```json
{
  "status": "fail",
  "message": "Incorrect email or password"
}
```

### Missing Fields

```json
{
  "status": "fail",
  "message": "Please provide email and password"
}
```

### Registration Error

```json
{
  "status": "fail",
  "message": "Email already in use"
}
```

---

## Testing in Postman

1. Create a new request:
   - For registration: POST `/api/auth/signup`
   - For login: POST `/api/auth/login`

2. Set the request body to JSON format and include the required fields

3. Send the request and save the returned token for accessing protected routes

4. For protected routes, set the Authorization header: `Bearer <your_token>`
