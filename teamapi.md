# Team API Documentation

All routes require authentication with a valid JWT token.

## Authentication

All requests must include the JWT token in the Authorization header:

```
Authorization: Bearer <YOUR_JWT_TOKEN>
```

## Endpoints

### POST /api/teams

Creates a new team in the system.

**Example Request:**
```
POST /api/teams
```

**Request Body:**
```json
{
  "name": "Varsity Basketball",
  "description": "School's varsity basketball team",
  "sport": "60d21b4667d0d8992e610c80",
  "organization": "60d21b4667d0d8992e610c90"
}
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "team": {
      "_id": "60d21b4667d0d8992e610c95",
      "name": "Varsity Basketball",
      "description": "School's varsity basketball team",
      "sport": "60d21b4667d0d8992e610c80",
      "organization": "60d21b4667d0d8992e610c90",
      "coaches": [],
      "createdBy": "60d21b4667d0d8992e610c85",
      "createdAt": "2023-06-23T12:34:56.789Z"
    }
  }
}
```

---

### GET /api/teams/:id

Retrieves information about a specific team.

**Example Request:**
```
GET /api/teams/60d21b4667d0d8992e610c95
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "team": {
      "_id": "60d21b4667d0d8992e610c95",
      "name": "Varsity Basketball",
      "description": "School's varsity basketball team",
      "sport": {
        "_id": "60d21b4667d0d8992e610c80",
        "name": "Basketball"
      },
      "organization": "60d21b4667d0d8992e610c90",
      "coaches": [
        {
          "_id": "60d21b4667d0d8992e610c88",
          "name": "Coach Smith",
          "email": "coach@example.com"
        }
      ],
      "createdBy": "60d21b4667d0d8992e610c85",
      "createdAt": "2023-06-23T12:34:56.789Z"
    }
  }
}
```

-----------------------------------------------------------

### PATCH /api/teams/:id

Updates a specific team's information.

**Example Request:**
```
PATCH /api/teams/60d21b4667d0d8992e610c95
```

**Request Body:**
```json
{
  "name": "Junior Varsity Basketball",
  "description": "Updated description for the team"
}
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "team": {
      "_id": "60d21b4667d0d8992e610c95",
      "name": "Junior Varsity Basketball",
      "description": "Updated description for the team",
      "sport": "60d21b4667d0d8992e610c80",
      "organization": "60d21b4667d0d8992e610c90",
      "coaches": [],
      "createdBy": "60d21b4667d0d8992e610c85",
      "createdAt": "2023-06-23T12:34:56.789Z"
    }
  }
}
```

---

### DELETE /api/teams/:id

Deletes a specific team from the system.

**Example Request:**
```
DELETE /api/teams/60d21b4667d0d8992e610c95
```

**Example Response:**
```
Status: 204 No Content
```

-----------------------------------------------------------

## Permissions

Team operations are restricted based on user roles:

1. **Admin**: Can manage all teams across all organizations.
2. **Organization Owner**: Can manage teams only within their own organization.
3. **Manager**: Can manage teams only within their assigned organization.

## Testing in Postman

1. First, authenticate using the login endpoint to get a JWT token:
   - POST `/api/auth/login`
   - Body: `{ "email": "user@example.com", "password": "userpassword" }`
   - Save the returned token

2. For all team API requests:
   - Set the Authorization header: `Bearer <your_token>`
   - Select the appropriate HTTP method (POST, GET, PATCH, DELETE)
   - Enter the full URL (e.g., `http://localhost:3000/api/teams`)
   - For POST and PATCH requests, set the body to JSON format and include the required fields
   - Send the request
