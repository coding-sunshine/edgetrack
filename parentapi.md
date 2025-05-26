# Parent API Documentation

All routes require authentication with a valid JWT token. Parents can be created by managers or coaches within an organization.

## Authentication

All requests must include the JWT token in the Authorization header:

```
Authorization: Bearer <YOUR_JWT_TOKEN>
```

## Endpoints

### GET /api/organizations/:orgId/parents

Retrieves all parents for a specific organization.

**Example Request:**
```
GET /api/organizations/60d21b4667d0d8992e610c95/parents
```

**Example Response:**
```json
{
  "status": "success",
  "results": 2,
  "data": {
    "parents": [
      {
        "_id": "60d21b4667d0d8992e610c100",
        "name": "John Smith",
        "email": "john.smith@example.com",
        "role": "parent",
        "organization": "60d21b4667d0d8992e610c95",
        "teams": [
          {
            "_id": "60d21b4667d0d8992e610c70",
            "name": "Varsity Soccer"
          }
        ],
        "children": [
          {
            "_id": "60d21b4667d0d8992e610c101",
            "name": "Alex Smith",
            "email": "alex.smith@example.com"
          }
        ],
        "isPro": true,
        "createdAt": "2023-01-01T00:00:00.000Z"
      },
      {
        "_id": "60d21b4667d0d8992e610c102",
        "name": "Mary Johnson",
        "email": "mary.johnson@example.com",
        "role": "parent",
        "organization": "60d21b4667d0d8992e610c95",
        "teams": [],
        "children": [
          {
            "_id": "60d21b4667d0d8992e610c103",
            "name": "Emma Johnson",
            "email": "emma.johnson@example.com"
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

### POST /api/organizations/:orgId/parents

Creates a new parent account for a specific organization.

**Example Request:**
```
POST /api/organizations/60d21b4667d0d8992e610c95/parents
```

**Request Body:**
```json
{
  "name": "David Brown",
  "email": "david.brown@example.com",
  "password": "password123",
  "teams": ["60d21b4667d0d8992e610c70"]
}
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "parent": {
      "_id": "60d21b4667d0d8992e610c104",
      "name": "David Brown",
      "email": "david.brown@example.com",
      "role": "parent",
      "organization": "60d21b4667d0d8992e610c95",
      "teams": ["60d21b4667d0d8992e610c70"],
      "children": [],
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

### GET /api/organizations/parents/:id

Retrieves information about a specific parent.

**Example Request:**
```
GET /api/organizations/parents/60d21b4667d0d8992e610c100
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "parent": {
      "_id": "60d21b4667d0d8992e610c100",
      "name": "John Smith",
      "email": "john.smith@example.com",
      "role": "parent",
      "organization": "60d21b4667d0d8992e610c95",
      "teams": [
        {
          "_id": "60d21b4667d0d8992e610c70",
          "name": "Varsity Soccer"
        }
      ],
      "children": [
        {
          "_id": "60d21b4667d0d8992e610c101",
          "name": "Alex Smith",
          "email": "alex.smith@example.com",
          "dateOfBirth": "2010-05-15T00:00:00.000Z"
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

### PATCH /api/organizations/parents/:id

Updates a specific parent's information.

**Example Request:**
```
PATCH /api/organizations/parents/60d21b4667d0d8992e610c100
```

**Request Body:**
```json
{
  "name": "John David Smith",
  "teams": ["60d21b4667d0d8992e610c70", "60d21b4667d0d8992e610c71"]
}
```

**Example Response:**
```json
{
  "status": "success",
  "data": {
    "parent": {
      "_id": "60d21b4667d0d8992e610c100",
      "name": "John David Smith",
      "email": "john.smith@example.com",
      "role": "parent",
      "organization": "60d21b4667d0d8992e610c95",
      "teams": [
        {
          "_id": "60d21b4667d0d8992e610c70",
          "name": "Varsity Soccer"
        },
        {
          "_id": "60d21b4667d0d8992e610c71",
          "name": "JV Basketball"
        }
      ],
      "children": [
        {
          "_id": "60d21b4667d0d8992e610c101",
          "name": "Alex Smith",
          "email": "alex.smith@example.com"
        }
      ],
      "isPro": true,
      "createdAt": "2023-01-01T00:00:00.000Z"
    }
  }
}
```

-----------------------------------------------------------
  
### DELETE /api/organizations/parents/:id

Deletes a specific parent and all their associated athlete children.

**Example Request:**
```
DELETE /api/organizations/parents/60d21b4667d0d8992e610c100
```

**Example Response:**
```
Status: 204 No Content
```

---

## Authorization Rules

1. **Admin users** can access all parents across all organizations.

2. **Organization owners** can manage parents only within their own organization.

3. **Managers and coaches** can manage parents only within their assigned organization.

4. **Parents** can view and update their own profile information.

---

## Error Responses

### Not Found

```json
{
  "status": "fail",
  "message": "Parent not found"
}
```

### Permission Error

```json
{
  "status": "fail",
  "message": "You do not have permission to create parents for this organization"
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
   - Body: `{ "email": "manager@example.com", "password": "password" }`
   - Save the returned token

2. For all Parent API requests:
   - Set the Authorization header: `Bearer <your_token>`
   - Select the appropriate HTTP method (GET, POST, PATCH, DELETE)
   - Enter the full URL (e.g., `http://localhost:3000/api/organizations/60d21b4667d0d8992e610c95/parents`)
   - For POST and PATCH requests, set the body to JSON format and include the required fields
   - Send the request
