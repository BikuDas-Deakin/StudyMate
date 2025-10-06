# StudyMate API Documentation

## Base URL
```
http://localhost:5000/api
```

## Authentication

All protected routes require JWT authentication via Bearer token in the Authorization header.

```
Authorization: Bearer <your-jwt-token>
```

JWT tokens expire after 24 hours and contain:
- `id` - User MongoDB ObjectId
- `username` - User's username
- `role` - User role (admin/member)

---

## Authentication Endpoints

### Register User

**POST** `/auth/register`

Create a new user account.

**Request Body:**
```json
{
  "username": "johndoe",
  "email": "john@example.com",
  "password": "securePassword123"
}
```

**Validation Rules:**
- `username`: Required, minimum 3 characters
- `email`: Required, valid email format
- `password`: Required, minimum 6 characters

**Success Response (201):**
```json
{
  "message": "User registered successfully",
  "user": {
    "_id": "64abc123def456789",
    "username": "johndoe",
    "email": "john@example.com",
    "role": "member",
    "totalSessions": 0,
    "currentStreak": 0,
    "totalMinutesStudied": 0
  }
}
```

**Error Responses:**

| Code | Response |
|------|----------|
| 400 | `{ "message": "Email already in use" }` |
| 400 | Validation errors from validator middleware |
| 500 | `{ "error": "error message" }` |

---

### Login User

**POST** `/auth/login`

Authenticate user and receive JWT token.

**Request Body:**
```json
{
  "email": "john@example.com",
  "password": "securePassword123"
}
```

**Success Response (200):**
```json
{
  "message": "Login successful",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

**Error Responses:**

| Code | Response |
|------|----------|
| 400 | `{ "message": "Invalid credentials" }` |
| 500 | `{ "error": "error message" }` |

---

### Get User Profile

**GET** `/auth/profile`

Retrieve authenticated user's profile information.

**Headers:**
```
Authorization: Bearer <token>
```

**Success Response (200):**
```json
{
  "user": {
    "_id": "64abc123def456789",
    "username": "johndoe",
    "email": "john@example.com",
    "role": "member",
    "totalSessions": 12,
    "currentStreak": 5,
    "totalMinutesStudied": 340
  }
}
```

**Error Responses:**

| Code | Response |
|------|----------|
| 401 | `{ "message": "Unauthorized" }` |
| 500 | `{ "error": "error message" }` |

---

## Room Endpoints

### Create Room

**POST** `/rooms`

Create a new study room.

**Headers:**
```
Authorization: Bearer <token>
```

**Request Body:**
```json
{
  "name": "Math Study Group",
  "studyInterval": 25,
  "breakInterval": 5,
  "privacy": "public"
}
```

**For Private Rooms:**
```json
{
  "name": "Private Study Session",
  "studyInterval": 30,
  "breakInterval": 10,
  "privacy": "private",
  "code": "SECRET123"
}
```

**Validation Rules:**
- `name`: Required
- `studyInterval`: Required, number (minutes)
- `breakInterval`: Required, number (minutes)
- `privacy`: Required, either "public" or "private"
- `code`: Required if privacy is "private"

**Success Response (201):**
```json
{
  "name": "Math Study Group",
  "success": true,
  "roomId": "64xyz789abc123def",
  "message": "Room created successfully"
}
```

**Error Responses:**

| Code | Response |
|------|----------|
| 400 | `{ "message": "Room code is required for private rooms" }` |
| 400 | Validation errors from validator middleware |
| 401 | `{ "message": "Unauthorized" }` |
| 500 | `{ "message": "Server Error" }` |

---

### Get All Rooms

**GET** `/rooms`

Retrieve dashboard data including public rooms and user's rooms.

**Headers:**
```
Authorization: Bearer <token>
```

**Success Response (200):**
```json
{
  "username": "johndoe",
  "sessions": 12,
  "streak": 5,
  "timeStudied": 340,
  "publicRooms": [
    {
      "_id": "64xyz789abc123def",
      "name": "Math Study Group",
      "creator": {
        "_id": "64abc123def456789",
        "username": "janedoe"
      },
      "studyInterval": 25,
      "breakInterval": 5,
      "privacy": "public",
      "status": "active",
      "participants": ["64abc123def456789"],
      "createdAt": "2025-10-01T10:00:00.000Z"
    }
  ],
  "myRooms": [
    {
      "_id": "64xyz789abc123def",
      "name": "My Private Study",
      "creator": {
        "_id": "64abc123def456789",
        "username": "johndoe"
      },
      "studyInterval": 30,
      "breakInterval": 10,
      "privacy": "private",
      "status": "active",
      "participants": ["64abc123def456789"],
      "createdAt": "2025-10-01T11:00:00.000Z"
    }
  ],
  "rooms": [
    // All active rooms (for search functionality)
  ]
}
```

**Note:** Room codes are NEVER included in responses for security.

**Error Responses:**

| Code | Response |
|------|----------|
| 401 | `{ "message": "Unauthorized" }` |
| 500 | `{ "message": "Server Error" }` |

---

### Get Room By ID

**GET** `/rooms/:id`

Retrieve detailed information about a specific room.

**Headers:**
```
Authorization: Bearer <token>
```

**Path Parameters:**
- `id`: Room MongoDB ObjectId

**Success Response (200):**
```json
{
  "_id": "64xyz789abc123def",
  "name": "Math Study Group",
  "creator": "64abc123def456789",
  "studyInterval": 25,
  "breakInterval": 5,
  "privacy": "public",
  "status": "active",
  "participants": [
    {
      "_id": "64abc123def456789",
      "username": "johndoe"
    },
    {
      "_id": "64abc456def789123",
      "username": "janedoe"
    }
  ],
  "createdAt": "2025-10-01T10:00:00.000Z",
  "updatedAt": "2025-10-01T10:00:00.000Z"
}
```

**Error Responses:**

| Code | Response |
|------|----------|
| 401 | `{ "message": "Unauthorized" }` |
| 403 | `{ "message": "Access denied", "isPrivate": true }` |
| 404 | `{ "message": "Room not found" }` |
| 500 | `{ "message": "Server error" }` |

**Note:** Private room access requires user to be creator or participant.

---

## Chat Endpoints

### Send Message

**POST** `/chat/rooms/:id/messages`

Post a message to a room's chat.

**Headers:**
```
Authorization: Bearer <token>
```

**Path Parameters:**
- `id`: Room MongoDB ObjectId

**Request Body:**
```json
{
  "message": "Hello everyone! Ready to study?"
}
```

**Validation Rules:**
- `message`: Required, cannot be empty or whitespace only
- Message is sanitized to prevent XSS attacks

**Success Response (201):**
```json
{
  "message": "Message sent",
  "chat": {
    "_id": "64msg123abc456def",
    "roomId": "64xyz789abc123def",
    "senderId": "64abc123def456789",
    "message": "Hello everyone! Ready to study?",
    "createdAt": "2025-10-06T14:30:00.000Z"
  }
}
```

**Error Responses:**

| Code | Response |
|------|----------|
| 400 | `{ "message": "Message cannot be empty" }` |
| 400 | Validation errors from validator middleware |
| 401 | `{ "message": "Unauthorized" }` |
| 500 | `{ "error": "error message" }` |

---

### Get Messages

**GET** `/chat/rooms/:id/messages`

Retrieve chat messages for a specific room.

**Headers:**
```
Authorization: Bearer <token>
```

**Path Parameters:**
- `id`: Room MongoDB ObjectId

**Query Parameters:**
- `limit` (optional): Number of messages to retrieve (default: 50)

**Example Request:**
```
GET /chat/rooms/64xyz789abc123def/messages?limit=100
```

**Success Response (200):**
```json
{
  "messages": [
    {
      "_id": "64msg123abc456def",
      "roomId": "64xyz789abc123def",
      "senderId": {
        "_id": "64abc123def456789",
        "username": "johndoe"
      },
      "message": "Hello everyone!",
      "createdAt": "2025-10-06T14:30:00.000Z"
    },
    {
      "_id": "64msg456def789abc",
      "roomId": "64xyz789abc123def",
      "senderId": {
        "_id": "64abc456def789123",
        "username": "janedoe"
      },
      "message": "Hi! Let's get started.",
      "createdAt": "2025-10-06T14:31:00.000Z"
    }
  ]
}
```

**Note:** Messages are returned in chronological order (oldest first).

**Error Responses:**

| Code | Response |
|------|----------|
| 401 | `{ "message": "Unauthorized" }` |
| 500 | `{ "error": "error message" }` |

---

## Dashboard Endpoint

### Get Dashboard Data

**GET** `/dashboard`

Retrieve user-specific dashboard statistics.

**Headers:**
```
Authorization: Bearer <token>
```

**Success Response (200):**
```json
{
  "username": "johndoe",
  "sessions": 12,
  "streak": 5,
  "timeStudied": 340
}
```

**Error Responses:**

| Code | Response |
|------|----------|
| 401 | `{ "message": "Unauthorized" }` |
| 500 | `{ "message": "Server Error" }` |

---

## Testing Endpoints

**⚠️ These endpoints are only available in test/development environments.**

### Health Check

**GET** `/test/health`

Simple health check endpoint for CI/CD and monitoring.

**Success Response (200):**
```json
{
  "ok": true
}
```

---

### Reset Database

**POST** `/test/reset`

Wipe all data from the database (test fixtures only).

**Success Response (204):**
```
No content
```

**Error Response (500):**
```json
{
  "error": "reset_failed"
}
```

---

### Seed Database

**POST** `/test/seed`

Load deterministic test fixtures into the database.

**Success Response (204):**
```
No content
```

**Error Response (500):**
```json
{
  "error": "seed_failed"
}
```

---

## Common Error Response Format

All endpoints follow consistent error response patterns:

### Validation Errors (400)
```json
{
  "errors": [
    {
      "field": "email",
      "message": "Invalid email format"
    },
    {
      "field": "password",
      "message": "Password must be at least 6 characters"
    }
  ]
}
```

### Authentication Errors (401)
```json
{
  "message": "Unauthorized"
}
```

### Authorization Errors (403)
```json
{
  "message": "Access denied"
}
```

### Not Found Errors (404)
```json
{
  "message": "Resource not found"
}
```

### Server Errors (500)
```json
{
  "error": "error message"
}
```
or
```json
{
  "message": "Server Error"
}
```

---

## WebSocket Events (Socket.io)

StudyMate uses Socket.io for real-time features. Connect to the WebSocket endpoint after authentication:

```javascript
const socket = io('http://localhost:5000', {
  auth: {
    token: '<your-jwt-token>'
  }
});
```

### Room Events

**Join Room:**
```javascript
socket.emit('join-room', {
  roomId: '64xyz789abc123def',
  roomCode: 'SECRET123' // Only for private rooms
});
```

**Leave Room:**
```javascript
socket.emit('leave-room', {
  roomId: '64xyz789abc123def'
});
```

**Chat Message:**
```javascript
socket.emit('chat-message', {
  roomId: '64xyz789abc123def',
  message: 'Hello everyone!'
});
```

**Timer Events:**
```javascript
socket.emit('start-timer', { roomId: '64xyz789abc123def' });
socket.emit('pause-timer', { roomId: '64xyz789abc123def' });
socket.emit('reset-timer', { roomId: '64xyz789abc123def' });
```

### Listening for Events

```javascript
socket.on('user-joined', (data) => {
  // Handle user joining room
});

socket.on('chat-message', (data) => {
  // Handle incoming chat message
});

socket.on('timer-update', (data) => {
  // Handle timer state changes
});
```

---

## Rate Limiting

Currently, no rate limiting is implemented. Consider adding rate limiting in production for:
- Authentication endpoints (login/register): 5 requests per minute
- Chat endpoints: 10 messages per minute
- Room creation: 5 rooms per hour

---

## Security Notes

1. **JWT Tokens**: Store securely (httpOnly cookies or secure storage), never in localStorage
2. **Room Codes**: Never exposed in API responses for security
3. **Password Hashing**: bcrypt with salt rounds
4. **Input Sanitization**: All user inputs are validated and sanitized
5. **CORS**: Configure appropriately for production
6. **HTTPS**: Always use HTTPS in production

---

## Response Times (Target)

- Authentication: < 200ms
- Room operations: < 150ms
- Chat operations: < 100ms
- Dashboard data: < 200ms
- WebSocket latency: < 50ms

---

## API Versioning

Current version: **v1** (implicit)

Future versions will use explicit versioning:
```
/api/v2/rooms
```
