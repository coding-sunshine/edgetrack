# Sports API Documentation

The Sports API provides endpoints for managing sports within organizations and their associated teams.

## Authentication

All routes require authentication with a valid JWT token.

```
Authorization: Bearer <YOUR_JWT_TOKEN>
```

## Endpoints

### POST /api/sports

Creates a new sport for an organization.

**Example Request:**
```
POST /api/sports
```

**Request Body:**
```json
{
  "name": "Soccer",
  "description": "Association football, commonly known as soccer",
  "organization": "60d21b4667d0d8992e610c85"
}
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "sport": {
      "_id": "60d21b4667d0d8992e610c87",
      "name": "Soccer",
      "description": "Association football, commonly known as soccer",
      "organization": "60d21b4667d0d8992e610c85",
      "createdBy": "60d21b4667d0d8992e610c80"
    }
  }
}
```

---

### GET /api/sports/organization/:orgId

Retrieves all sports for a specific organization.

**Example Request:**
```
GET /api/sports/organization/60d21b4667d0d8992e610c85
```

**Example Response:**
```json
{
  "status": "success",
  "results": 2,
  "data": {
    "sports": [
      {
        "_id": "60d21b4667d0d8992e610c87",
        "name": "Soccer",
        "description": "Association football, commonly known as soccer",
        "organization": "60d21b4667d0d8992e610c85",
        "createdBy": "60d21b4667d0d8992e610c80"
      },
      {
        "_id": "60d21b4667d0d8992e610c88",
        "name": "Basketball",
        "description": "Indoor team sport",
        "organization": "60d21b4667d0d8992e610c85",
        "createdBy": "60d21b4667d0d8992e610c80"
      }
    ]
  }
}
```

-----------------------------------------------------------

### GET /api/sports/:id

Retrieves details about a specific sport.

**Example Request:**
```
GET /api/sports/60d21b4667d0d8992e610c87
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "sport": {
      "_id": "60d21b4667d0d8992e610c87",
      "name": "Soccer",
      "description": "Association football, commonly known as soccer",
      "organization": "60d21b4667d0d8992e610c85",
      "createdBy": "60d21b4667d0d8992e610c80"
    }
  }
}
```

---

### PATCH /api/sports/:id

Updates a specific sport's information.

**Example Request:**
```
PATCH /api/sports/60d21b4667d0d8992e610c87
```

**Request Body:**
```json
{
  "name": "Football",
  "description": "Updated description for football/soccer"
}
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "sport": {
      "_id": "60d21b4667d0d8992e610c87",
      "name": "Football",
      "description": "Updated description for football/soccer",
      "organization": "60d21b4667d0d8992e610c85",
      "createdBy": "60d21b4667d0d8992e610c80"
    }
  }
}
```

-----------------------------------------------------------

### DELETE /api/sports/:id

Deletes a specific sport.

**Example Request:**
```
DELETE /api/sports/60d21b4667d0d8992e610c87
```

**Example Response:**
```
Status: 204 No Content
```

---

### GET /api/sports/:sportId/teams

Retrieves all teams associated with a specific sport.

**Example Request:**
```
GET /api/sports/60d21b4667d0d8992e610c87/teams
```

**Example Response:**
```json
{
  "status": "success",
  "results": 2,
  "data": {
    "teams": [
      {
        "_id": "60d21b4667d0d8992e610c90",
        "name": "Eagles",
        "description": "Club's first team",
        "sport": "60d21b4667d0d8992e610c87",
        "organization": "60d21b4667d0d8992e610c85",
        "coaches": [
          {
            "_id": "60d21b4667d0d8992e610c95",
            "name": "Coach Johnson",
            "email": "coach@example.com"
          }
        ],
        "createdBy": "60d21b4667d0d8992e610c80"
      },
      {
        "_id": "60d21b4667d0d8992e610c91",
        "name": "Junior Eagles",
        "description": "Club's youth team",
        "sport": "60d21b4667d0d8992e610c87",
        "organization": "60d21b4667d0d8992e610c85",
        "coaches": [],
        "createdBy": "60d21b4667d0d8992e610c80"
      }
    ]
  }
}
```

---

## Authorization Rules

1. **Admin users** can access all sports and teams across all organizations.

2. **Organization owners** can only access sports and teams in their own organization.

3. **Managers** can only access sports and teams in the organization they are assigned to.

---

## Error Responses

### Not Found

```json
{
  "status": "fail",
  "message": "Sport not found"
}
```

### Permission Error

```json
{
  "status": "fail",
  "message": "You do not have permission to access sports for this organization"
}
```

### Invalid Input

```json
{
  "status": "fail",
  "message": "Organization not found"
}
```

---

## Testing in Postman

1. Authenticate using the login endpoint to get a JWT token:
   - POST `/api/auth/login`
   - Body: `{ "email": "user@example.com", "password": "password" }`
   - Save the returned token

2. For all Sports API requests:
   - Set the Authorization header: `Bearer <your_token>`
   - Select the appropriate HTTP method (GET, POST, PATCH, DELETE)
   - Enter the full URL (e.g., `http://localhost:3000/api/sports`)
   - For POST and PATCH requests, set the body to JSON format and include the required fields
   - Send the request
