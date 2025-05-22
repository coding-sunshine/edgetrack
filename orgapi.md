# Organization API Documentation

All routes require authentication with a valid JWT token.

## Authentication

All requests must include the JWT token in the Authorization header:

```
Authorization: Bearer <YOUR_JWT_TOKEN>
```

## Organization Endpoints

### GET /api/organizations

Retrieves the current user's organization.

**Example Request:**
```
GET /api/organizations
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "organization": {
      "_id": "60d21b4667d0d8992e610c95",
      "name": "Edge Sports Academy",
      "description": "Premier sports training organization",
      "owner": {
        "_id": "60d21b4667d0d8992e610c86",
        "name": "Organization Owner",
        "email": "owner@example.com"
      },
      "managers": [
        {
          "_id": "60d21b4667d0d8992e610c87",
          "name": "Manager User",
          "email": "manager@example.com"
        }
      ],
      "createdAt": "2023-01-01T00:00:00.000Z",
      "updatedAt": "2023-01-01T00:00:00.000Z"
    }
  }
}
```

---

### POST /api/organizations

Creates a new organization. Available only to pro users with the 'orgowner' role.

**Example Request:**
```
POST /api/organizations
```

**Request Body:**
```json
{
  "name": "New Sports Academy",
  "description": "Training the champions of tomorrow"
}
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "organization": {
      "_id": "60d21b4667d0d8992e610c96",
      "name": "New Sports Academy",
      "description": "Training the champions of tomorrow",
      "owner": "60d21b4667d0d8992e610c86",
      "managers": [],
      "createdAt": "2023-06-23T12:34:56.789Z",
      "updatedAt": "2023-06-23T12:34:56.789Z"
    }
  }
}
```

-----------------------------------------------------------

### GET /api/organizations/:id

Retrieves information about a specific organization.

**Example Request:**
```
GET /api/organizations/60d21b4667d0d8992e610c95
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "organization": {
      "_id": "60d21b4667d0d8992e610c95",
      "name": "Edge Sports Academy",
      "description": "Premier sports training organization",
      "owner": {
        "_id": "60d21b4667d0d8992e610c86",
        "name": "Organization Owner",
        "email": "owner@example.com"
      },
      "managers": [
        {
          "_id": "60d21b4667d0d8992e610c87",
          "name": "Manager User",
          "email": "manager@example.com"
        }
      ],
      "createdAt": "2023-01-01T00:00:00.000Z",
      "updatedAt": "2023-01-01T00:00:00.000Z"
    }
  }
}
```

---

### PATCH /api/organizations/:id

Updates a specific organization's information.

**Example Request:**
```
PATCH /api/organizations/60d21b4667d0d8992e610c95
```

**Request Body:**
```json
{
  "name": "Updated Sports Academy",
  "description": "New description for our organization"
}
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "organization": {
      "_id": "60d21b4667d0d8992e610c95",
      "name": "Updated Sports Academy",
      "description": "New description for our organization",
      "owner": "60d21b4667d0d8992e610c86",
      "managers": [],
      "createdAt": "2023-01-01T00:00:00.000Z",
      "updatedAt": "2023-06-23T12:34:56.789Z"
    }
  }
}
```

-----------------------------------------------------------

### DELETE /api/organizations/:id

Deletes a specific organization.

**Example Request:**
```
DELETE /api/organizations/60d21b4667d0d8992e610c95
```

**Example Response:**
```
Status: 204 No Content
```

---

## Manager Endpoints

### GET /api/organizations/:orgId/managers

Retrieves all managers for a specific organization.

**Example Request:**
```
GET /api/organizations/60d21b4667d0d8992e610c95/managers
```

**Example Response:**
```json
{
  "status": "success",
  "results": 2,
  "data": {
    "managers": [
      {
        "_id": "60d21b4667d0d8992e610c97",
        "name": "Manager One",
        "email": "manager1@example.com",
        "role": "manager",
        "organization": "60d21b4667d0d8992e610c95",
        "isPro": true,
        "createdAt": "2023-01-01T00:00:00.000Z"
      },
      {
        "_id": "60d21b4667d0d8992e610c98",
        "name": "Manager Two",
        "email": "manager2@example.com",
        "role": "manager",
        "organization": "60d21b4667d0d8992e610c95",
        "isPro": true,
        "createdAt": "2023-01-02T00:00:00.000Z"
      }
    ]
  }
}
```

---

### POST /api/organizations/:orgId/managers

Creates a new manager for a specific organization.

**Example Request:**
```
POST /api/organizations/60d21b4667d0d8992e610c95/managers
```

**Request Body:**
```json
{
  "name": "New Manager",
  "email": "newmanager@example.com",
  "password": "password123"
}
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "manager": {
      "_id": "60d21b4667d0d8992e610c99",
      "name": "New Manager",
      "email": "newmanager@example.com",
      "role": "manager",
      "organization": "60d21b4667d0d8992e610c95",
      "isPro": true,
      "createdAt": "2023-06-23T12:34:56.789Z",
      "planInfo": {
        "planType": "premium",
        "startDate": "2023-01-01T00:00:00.000Z"
      }
    }
  }
}
```

-----------------------------------------------------------

### GET /api/organizations/managers/:id

Retrieves information about a specific manager.

**Example Request:**
```
GET /api/organizations/managers/60d21b4667d0d8992e610c97
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "manager": {
      "_id": "60d21b4667d0d8992e610c97",
      "name": "Manager One",
      "email": "manager1@example.com",
      "role": "manager",
      "organization": "60d21b4667d0d8992e610c95",
      "isPro": true,
      "createdAt": "2023-01-01T00:00:00.000Z",
      "planInfo": {
        "planType": "premium",
        "startDate": "2023-01-01T00:00:00.000Z"
      }
    }
  }
}
```

---

### PATCH /api/organizations/managers/:id

Updates a specific manager's information.

**Example Request:**
```
PATCH /api/organizations/managers/60d21b4667d0d8992e610c97
```

**Request Body:**
```json
{
  "name": "Updated Manager Name",
  "email": "updatedmanager@example.com"
}
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "manager": {
      "_id": "60d21b4667d0d8992e610c97",
      "name": "Updated Manager Name",
      "email": "updatedmanager@example.com",
      "role": "manager",
      "organization": "60d21b4667d0d8992e610c95",
      "isPro": true,
      "createdAt": "2023-01-01T00:00:00.000Z",
      "planInfo": {
        "planType": "premium",
        "startDate": "2023-01-01T00:00:00.000Z"
      }
    }
  }
}
```

-----------------------------------------------------------

### DELETE /api/organizations/managers/:id

Deletes a specific manager.

**Example Request:**
```
DELETE /api/organizations/managers/60d21b4667d0d8992e610c97
```

**Example Response:**
```
Status: 204 No Content
```

---

## Coach Endpoints

### GET /api/organizations/:orgId/coaches

Retrieves all coaches for a specific organization.

**Example Request:**
```
GET /api/organizations/60d21b4667d0d8992e610c95/coaches
```

**Example Response:**
```json
{
  "status": "success",
  "results": 2,
  "data": {
    "coaches": [
      {
        "_id": "60d21b4667d0d8992e610c91",
        "name": "Coach One",
        "email": "coach1@example.com",
        "role": "coach",
        "organization": "60d21b4667d0d8992e610c95",
        "sport": {
          "_id": "60d21b4667d0d8992e610c80",
          "name": "Soccer"
        },
        "teams": [
          {
            "_id": "60d21b4667d0d8992e610c70",
            "name": "Varsity Soccer"
          }
        ],
        "isPro": true,
        "createdAt": "2023-01-01T00:00:00.000Z"
      },
      {
        "_id": "60d21b4667d0d8992e610c92",
        "name": "Coach Two",
        "email": "coach2@example.com",
        "role": "coach",
        "organization": "60d21b4667d0d8992e610c95",
        "sport": {
          "_id": "60d21b4667d0d8992e610c81",
          "name": "Basketball"
        },
        "teams": [
          {
            "_id": "60d21b4667d0d8992e610c71",
            "name": "JV Basketball"
          }
        ],
        "isPro": true,
        "createdAt": "2023-01-02T00:00:00.000Z"
      }
    ]
  }
}
```

---

### POST /api/organizations/:orgId/coaches

Creates a new coach for a specific organization.

**Example Request:**
```
POST /api/organizations/60d21b4667d0d8992e610c95/coaches
```

**Request Body:**
```json
{
  "name": "New Coach",
  "email": "newcoach@example.com",
  "password": "password123",
  "sport": "60d21b4667d0d8992e610c80",
  "teams": ["60d21b4667d0d8992e610c70"]
}
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "coach": {
      "_id": "60d21b4667d0d8992e610c93",
      "name": "New Coach",
      "email": "newcoach@example.com",
      "role": "coach",
      "organization": "60d21b4667d0d8992e610c95",
      "sport": "60d21b4667d0d8992e610c80",
      "teams": ["60d21b4667d0d8992e610c70"],
      "isPro": true,
      "createdAt": "2023-06-23T12:34:56.789Z",
      "planInfo": {
        "planType": "premium",
        "startDate": "2023-01-01T00:00:00.000Z"
      }
    }
  }
}
```

-----------------------------------------------------------

### GET /api/organizations/coaches/:id

Retrieves information about a specific coach.

**Example Request:**
```
GET /api/organizations/coaches/60d21b4667d0d8992e610c91
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "coach": {
      "_id": "60d21b4667d0d8992e610c91",
      "name": "Coach One",
      "email": "coach1@example.com",
      "role": "coach",
      "organization": "60d21b4667d0d8992e610c95",
      "sport": {
        "_id": "60d21b4667d0d8992e610c80",
        "name": "Soccer"
      },
      "teams": [
        {
          "_id": "60d21b4667d0d8992e610c70",
          "name": "Varsity Soccer"
        }
      ],
      "isPro": true,
      "createdAt": "2023-01-01T00:00:00.000Z",
      "planInfo": {
        "planType": "premium",
        "startDate": "2023-01-01T00:00:00.000Z"
      }
    }
  }
}
```

---

### PATCH /api/organizations/coaches/:id

Updates a specific coach's information.

**Example Request:**
```
PATCH /api/organizations/coaches/60d21b4667d0d8992e610c91
```

**Request Body:**
```json
{
  "name": "Updated Coach Name",
  "teams": ["60d21b4667d0d8992e610c70", "60d21b4667d0d8992e610c72"]
}
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "coach": {
      "_id": "60d21b4667d0d8992e610c91",
      "name": "Updated Coach Name",
      "email": "coach1@example.com",
      "role": "coach",
      "organization": "60d21b4667d0d8992e610c95",
      "sport": {
        "_id": "60d21b4667d0d8992e610c80",
        "name": "Soccer"
      },
      "teams": [
        {
          "_id": "60d21b4667d0d8992e610c70",
          "name": "Varsity Soccer"
        },
        {
          "_id": "60d21b4667d0d8992e610c72",
          "name": "JV Soccer"
        }
      ],
      "isPro": true,
      "createdAt": "2023-01-01T00:00:00.000Z",
      "planInfo": {
        "planType": "premium",
        "startDate": "2023-01-01T00:00:00.000Z"
      }
    }
  }
}
```

-----------------------------------------------------------

### DELETE /api/organizations/coaches/:id

Deletes a specific coach.

**Example Request:**
```
DELETE /api/organizations/coaches/60d21b4667d0d8992e610c91
```

**Example Response:**
```
Status: 204 No Content
```

---

## Error Responses

### Not Found

```json
{
  "status": "fail",
  "message": "Organization not found"
}
```

### Unauthorized

```json
{
  "status": "fail",
  "message": "You do not have permission to access this organization"
}
```

### Plan Restriction

```json
{
  "status": "fail",
  "message": "Only pro users can create an organization"
}
```

---

## Testing in Postman

1. First, authenticate using the login endpoint to get a JWT token:
   - POST `/api/auth/login`
   - Body: `{ "email": "owner@example.com", "password": "ownerpassword" }`
   - Save the returned token

2. For all organization API requests:
   - Set the Authorization header: `Bearer <your_token>`
   - Select the appropriate HTTP method (GET, POST, PATCH, DELETE)
   - Enter the full URL (e.g., `http://localhost:3000/api/organizations`)
   - For POST and PATCH requests, set the body to JSON format and include the required fields
   - Send the request
