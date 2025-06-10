
```markdown
# Chat API Documentation

## Message Endpoints

### POST /api/messages/send
Send a new message to a user

**Request Body:**
```json
{
  "receiverId": "string (required)",
  "message": "string (required)"
}
```

**Successful Response (201):**
```json
{
  "status": "success",
  "data": {
    "_id": "string",
    "chat": "string",
    "sender": "string",
    "receiver": "string",
    "message": "string",
    "read": false,
    "createdAt": "ISO Date",
    "updatedAt": "ISO Date"
  },
  "channel": "string"
}
```

**Behavior:**
- Creates new chat if one doesn't exist between users
- Triggers Pusher event on channel `private-chat-{user1}-{user2}` (sorted IDs)
- Returns the created message with chat details

---

### GET /api/messages/chat/:userId1/:userId2
Get all messages between two users

**URL Parameters:**
- `userId1`: string (required)
- `userId2`: string (required)

**Successful Response (200):**
```json
{
  "status": "success",
  "data": {
    "chat": {
      "_id": "string",
      "participants": ["string", "string"],
      "createdAt": "ISO Date",
      "updatedAt": "ISO Date"
    },
    "messages": [
      {
        "_id": "string",
        "chat": "string",
        "sender": "string",
        "receiver": "string",
        "message": "string",
        "read": "boolean",
        "createdAt": "ISO Date",
        "updatedAt": "ISO Date"
      }
    ],
    "channel": "string"
  }
}
```

**Behavior:**
- Returns messages in chronological order (oldest first)
- Creates new chat if one doesn't exist
- Includes Pusher channel name for the chat

## Data Models

### Message
```javascript
{
  _id: ObjectId,
  chat: ObjectId,    // Reference to Chat
  sender: ObjectId,  // Reference to User
  receiver: ObjectId,// Reference to User
  message: String,
  read: Boolean,
  createdAt: Date,
  updatedAt: Date
}
```

### Chat
```javascript
{
  _id: ObjectId,
  participants: [ObjectId],  // Array of User references
  createdAt: Date,
  updatedAt: Date
}
```

## Real-Time Events
- **Channel:** `private-chat-{user1Id}-{user2Id}` (user IDs sorted numerically)
- **Event:** `new-message`
- **Event Data:**
```json
{
  "_id": "string",
  "message": "string",
  "sender": "string",
  "receiver": "string",
  "timestamp": "ISO Date"
}
```

## Error Responses
All endpoints return:
- `400` for invalid/missing parameters
- `500` for server errors with error details in response
```json
{
  "message": "Error description",
  "error": "Detailed error message (in development)"
}
```
