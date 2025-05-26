# Athlete API Documentation

All routes require authentication with a valid JWT token. Athletes can be created by their parents or by managers/coaches within an organization.

## Authentication

All requests must include the JWT token in the Authorization header:

```
Authorization: Bearer <YOUR_JWT_TOKEN>
```

## Endpoints

### GET /api/organizations/parents/:parentId/athletes

Retrieves all athletes for a specific parent.

**Example Request:**
```
GET /api/organizations/parents/60d21b4667d0d8992e610c100/athletes
```

**Example Response:**
```json
{
  "status": "success",
  "results": 2,
  "data": {
    "athletes": [
      {
        "_id": "60d21b4667d0d8992e610c101",
        "name": "Alex Smith",
        "email": "alex.smith@example.com",
        "role": "athlete",
        "organization": "60d21b4667d0d8992e610c95",
        "parent": {
          "_id": "60d21b4667d0d8992e610c100",
          "name": "John Smith",
          "email": "john.smith@example.com"
        },
        "dateOfBirth": "2010-05-15T00:00:00.000Z",
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
        "_id": "60d21b4667d0d8992e610c105",
        "name": "Jamie Smith",
        "email": "jamie.smith@example.com",
        "role": "athlete",
        "organization": "60d21b4667d0d8992e610c95",
        "parent": {
          "_id": "60d21b4667d0d8992e610c100",
          "name": "John Smith",
          "email": "john.smith@example.com"
        },
        "dateOfBirth": "2012-08-20T00:00:00.000Z",
        "teams": [],
        "isPro": true,
        "createdAt": "2023-01-05T00:00:00.000Z"
      }
    ]
  }
}
```

---

### POST /api/organizations/parents/:parentId/athletes

Creates a new athlete account for a specific parent.

**Example Request:**
```
POST /api/organizations/parents/60d21b4667d0d8992e610c100/athletes
```

**Request Body:**
```json
{
  "name": "Taylor Smith",
  "email": "taylor.smith@example.com",
  "password": "password123",
  "dateOfBirth": "2008-03-10",
  "teams": ["60d21b4667d0d8992e610c70"]
}
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "athlete": {
      "_id": "60d21b4667d0d8992e610c106",
      "name": "Taylor Smith",
      "email": "taylor.smith@example.com",
      "role": "athlete",
      "organization": "60d21b4667d0d8992e610c95",
      "parent": "60d21b4667d0d8992e610c100",
      "dateOfBirth": "2008-03-10T00:00:00.000Z",
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

### GET /api/organizations/:orgId/athletes

Retrieves all athletes for a specific organization (not available to parents).

**Example Request:**
```
GET /api/organizations/60d21b4667d0d8992e610c95/athletes
```

**Example Response:**
```json
{
  "status": "success",
  "results": 3,
  "data": {
    "athletes": [
      {
        "_id": "60d21b4667d0d8992e610c101",
        "name": "Alex Smith",
        "email": "alex.smith@example.com",
        "role": "athlete",
        "organization": "60d21b4667d0d8992e610c95",
        "parent": {
          "_id": "60d21b4667d0d8992e610c100",
          "name": "John Smith",
          "email": "john.smith@example.com"
        },
        "dateOfBirth": "2010-05-15T00:00:00.000Z",
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
        "_id": "60d21b4667d0d8992e610c103",
        "name": "Emma Johnson",
        "email": "emma.johnson@example.com",
        "role": "athlete",
        "organization": "60d21b4667d0d8992e610c95",
        "parent": {
          "_id": "60d21b4667d0d8992e610c102",
          "name": "Mary Johnson",
          "email": "mary.johnson@example.com"
        },
        "dateOfBirth": "2009-11-22T00:00:00.000Z",
        "teams": [
          {
            "_id": "60d21b4667d0d8992e610c71",
            "name": "JV Basketball"
          }
        ],
        "isPro": true,
        "createdAt": "2023-01-02T00:00:00.000Z"
      },
      {
        "_id": "60d21b4667d0d8992e610c105",
        "name": "Jamie Smith",
        "email": "jamie.smith@example.com",
        "role": "athlete",
        "organization": "60d21b4667d0d8992e610c95",
        "parent": {
          "_id": "60d21b4667d0d8992e610c100",
          "name": "John Smith",
          "email": "john.smith@example.com"
        },
        "dateOfBirth": "2012-08-20T00:00:00.000Z",
        "teams": [],
        "isPro": true,
        "createdAt": "2023-01-05T00:00:00.000Z"
      }
    ]
  }
}
```

---

### GET /api/organizations/athletes/:id

Retrieves information about a specific athlete.

**Example Request:**
```
GET /api/organizations/athletes/60d21b4667d0d8992e610c101
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "athlete": {
      "_id": "60d21b4667d0d8992e610c101",
      "name": "Alex Smith",
      "email": "alex.smith@example.com",
      "role": "athlete",
      "organization": "60d21b4667d0d8992e610c95",
      "parent": {
        "_id": "60d21b4667d0d8992e610c100",
        "name": "John Smith",
        "email": "john.smith@example.com"
      },
      "dateOfBirth": "2010-05-15T00:00:00.000Z",
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

-----------------------------------------------------------

### PATCH /api/organizations/athletes/:id

Updates a specific athlete's information.

**Example Request:**
```
PATCH /api/organizations/athletes/60d21b4667d0d8992e610c101
```

**Request Body:**
```json
{
  "name": "Alexander Smith",
  "teams": ["60d21b4667d0d8992e610c70", "60d21b4667d0d8992e610c72"]
}
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "athlete": {
      "_id": "60d21b4667d0d8992e610c101",
      "name": "Alexander Smith",
      "email": "alex.smith@example.com",
      "role": "athlete",
      "organization": "60d21b4667d0d8992e610c95",
      "parent": {
        "_id": "60d21b4667d0d8992e610c100",
        "name": "John Smith",
        "email": "john.smith@example.com"
      },
      "dateOfBirth": "2010-05-15T00:00:00.000Z",
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
      "createdAt": "2023-01-01T00:00:00.000Z"
    }
  }
}
```

---

### DELETE /api/organizations/athletes/:id

Deletes a specific athlete from the system.

**Example Request:**
```
DELETE /api/organizations/athletes/60d21b4667d0d8992e610c101
```

**Example Response:**
```
Status: 204 No Content
```

-----------------------------------------------------------

## Authorization Rules

1. **Admin users** can access all athletes across all organizations.

2. **Organization owners** can manage athletes only within their own organization.

3. **Managers and coaches** can manage athletes only within their assigned organization.

4. **Parents** can only access and manage their own children (athletes).

---

## Error Responses

### Not Found

```json
{
  "status": "fail",
  "message": "Athlete not found"
}
```

### Permission Error

```json
{
  "status": "fail",
  "message": "You do not have permission to create athletes for this parent"
}
```

### Parent Access Restriction

```json
{
  "status": "fail",
  "message": "Parents can only access their own athletes"
}
```

### Invalid Teams

```json
{
  "status": "fail",
  "message": "One or more teams are invalid or do not belong to this organization"
}
```

---

## Testing in Postman

1. Authenticate using the login endpoint to get a JWT token:
   - POST `/api/auth/login`
   - Body: `{ "email": "parent@example.com", "password": "password" }`
   - Save the returned token

2. For all Athlete API requests:
   - Set the Authorization header: `Bearer <your_token>`
   - Select the appropriate HTTP method (GET, POST, PATCH, DELETE)
   - Enter the full URL (e.g., `http://localhost:3000/api/organizations/parents/60d21b4667d0d8992e610c100/athletes`)
   - For POST and PATCH requests, set the body to JSON format and include the required fields
   - Send the request

## Special Notes

- Athletes inherit their parent's plan information (isPro and planInfo)
- Date of birth is required for all athletes
- Athletes are automatically added to their parent's children array when created
- Deleting an athlete removes them from their parent's children array
