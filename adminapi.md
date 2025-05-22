# Admin API Documentation

All routes require authentication with a valid JWT token and are restricted to users with the `admin` role.

## Authentication

All requests must include the JWT token in the Authorization header:

```
Authorization: Bearer <YOUR_JWT_TOKEN>
```

## Endpoints

### GET /api/admin/users

Retrieves a list of all users in the system.

**Example Request:**
```
GET /api/admin/users
```

**Example Response:**
```json
{
  "status": "success",
  "results": 2,
  "data": {
    "users": [
      {
        "_id": "60d21b4667d0d8992e610c85",
        "name": "Admin User",
        "email": "admin@example.com",
        "role": "admin",
        "createdAt": "2023-01-01T00:00:00.000Z",
        "isPro": true,
        "planInfo": {
          "planType": "premium",
          "startDate": "2023-01-01T00:00:00.000Z"
        }
      },
      {
        "_id": "60d21b4667d0d8992e610c86",
        "name": "Organization Owner",
        "email": "owner@example.com",
        "role": "orgowner",
        "createdAt": "2023-01-01T00:00:00.000Z",
        "isPro": false,
        "planInfo": {
          "planType": "free"
        }
      }
    ]
  }
}
```

---

### POST /api/admin/users

Creates a new user in the system.

**Example Request:**
```
POST /api/admin/users
```

**Request Body:**
```json
{
  "name": "New User",
  "email": "newuser@example.com",
  "password": "password123",
  "role": "orgowner",
  "isPro": false
}
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "user": {
      "_id": "60d21b4667d0d8992e610c87",
      "name": "New User",
      "email": "newuser@example.com",
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

### GET /api/admin/users/:id

Retrieves information about a specific user.

**Example Request:**
```
GET /api/admin/users/60d21b4667d0d8992e610c85
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "user": {
      "_id": "60d21b4667d0d8992e610c85",
      "name": "Admin User",
      "email": "admin@example.com",
      "role": "admin",
      "createdAt": "2023-01-01T00:00:00.000Z",
      "isPro": true,
      "planInfo": {
        "planType": "premium",
        "startDate": "2023-01-01T00:00:00.000Z"
      }
    }
  }
}
```

---

### PATCH /api/admin/users/:id

Updates a specific user's information.

**Example Request:**
```
PATCH /api/admin/users/60d21b4667d0d8992e610c86
```

**Request Body:**
```json
{
  "name": "Updated Name",
  "isPro": true,
  "planInfo": {
    "planType": "premium",
    "startDate": "2023-06-23T00:00:00.000Z",
    "endDate": "2024-06-23T00:00:00.000Z"
  }
}
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "user": {
      "_id": "60d21b4667d0d8992e610c86",
      "name": "Updated Name",
      "email": "owner@example.com",
      "role": "orgowner",
      "createdAt": "2023-01-01T00:00:00.000Z",
      "isPro": true,
      "planInfo": {
        "planType": "premium",
        "startDate": "2023-06-23T00:00:00.000Z",
        "endDate": "2024-06-23T00:00:00.000Z"
      }
    }
  }
}
```

-----------------------------------------------------------

### DELETE /api/admin/users/:id

Deletes a specific user from the system.

**Example Request:**
```
DELETE /api/admin/users/60d21b4667d0d8992e610c87
```

**Example Response:**
```
Status: 204 No Content
```

---

## Testing in Postman

1. First, authenticate using the login endpoint to get a JWT token:
   - POST `/api/auth/login`
   - Body: `{ "email": "admin@example.com", "password": "adminpassword" }`
   - Save the returned token

2. For all admin API requests:
   - Set the Authorization header: `Bearer <your_token>`
   - Select the appropriate HTTP method (GET, POST, PATCH, DELETE)
   - Enter the full URL (e.g., `http://localhost:3000/api/admin/users`)
   - For POST and PATCH requests, set the body to JSON format and include the required fields
   - Send the request
