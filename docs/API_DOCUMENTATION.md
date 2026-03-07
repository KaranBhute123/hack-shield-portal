# 📡 API Documentation

Complete API reference for HackShield Portal with examples and usage guidelines.

---

## 🔐 Authentication Endpoints

### User Registration
```http
POST /api/auth/register
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "SecurePassword123!",
  "name": "John Doe",
  "role": "participant"
}
```

**Response (201):**
```json
{
  "success": true,
  "message": "User registered successfully",
  "token": "eyJhbGciOiJIUzI1NiIs...",
  "user": {
    "id": "507f1f77bcf86cd799439011",
    "email": "user@example.com",
    "name": "John Doe",
    "role": "participant"
  }
}
```

**Errors:**
- `400` - Invalid email/password format
- `409` - Email already registered
- `422` - Validation error

---

### User Login
```http
POST /api/auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "SecurePassword123!"
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "Login successful",
  "token": "eyJhbGciOiJIUzI1NiIs...",
  "user": {
    "id": "507f1f77bcf86cd799439011",
    "email": "user@example.com",
    "name": "John Doe",
    "role": "participant"
  }
}
```

**Errors:**
- `401` - Invalid credentials
- `404` - User not found
- `422` - Validation error

---

### Logout
```http
POST /api/auth/logout
Authorization: Bearer <token>
```

**Response (200):**
```json
{
  "success": true,
  "message": "Logged out successfully"
}
```

---

## 👤 User Endpoints

### Get Current User
```http
GET /api/user
Authorization: Bearer <token>
```

**Response (200):**
```json
{
  "id": "507f1f77bcf86cd799439011",
  "email": "user@example.com",
  "name": "John Doe",
  "role": "participant",
  "profile": {
    "bio": "Developer and designer",
    "skills": ["React", "Node.js", "UI/UX"],
    "avatar": "https://...",
    "links": {
      "github": "https://github.com/johndoe",
      "linkedin": "https://linkedin.com/in/johndoe"
    }
  },
  "statistics": {
    "hackathonsParticipated": 5,
    "teamsCreated": 2,
    "projectsSubmitted": 3,
    "wins": 1,
    "xp": 2500,
    "level": 5,
    "streak": 2
  },
  "createdAt": "2024-01-15T10:30:00Z",
  "updatedAt": "2024-03-07T15:45:00Z"
}
```

---

### Update User Profile
```http
PUT /api/user
Authorization: Bearer <token>
Content-Type: application/json

{
  "name": "John Doe Updated",
  "profile": {
    "bio": "Full-stack developer",
    "skills": ["React", "Node.js", "Python", "UI/UX"],
    "links": {
      "github": "https://github.com/johndoe",
      "linkedin": "https://linkedin.com/in/johndoe",
      "portfolio": "https://johndoe.dev"
    }
  }
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "Profile updated",
  "user": { /* updated user object */ }
}
```

---

### Get User Statistics
```http
GET /api/user/stats
Authorization: Bearer <token>
```

**Response (200):**
```json
{
  "statistics": {
    "totalHackathons": 5,
    "wins": 1,
    "secondPlaces": 1,
    "thirdPlaces": 1,
    "participations": 5,
    "totalXP": 2500,
    "currentLevel": 5,
    "currentStreak": 2,
    "longestStreak": 4,
    "teamsCreated": 2,
    "projectsSubmitted": 3,
    "averagePlacement": 2.6,
    "achievements": 12
  },
  "recentEvents": [
    {
      "hackathonId": "507f1f77bcf86cd799439011",
      "hackathonName": "AI for Climate",
      "placement": 1,
      "date": "2024-03-01"
    }
  ]
}
```

---

## 🏆 Hackathon Endpoints

### Get All Hackathons
```http
GET /api/hackathons?page=1&limit=10&filter=ongoing&sort=prize
Authorization: Bearer <token>
```

**Query Parameters:**
- `page` - Page number (default: 1)
- `limit` - Results per page (default: 10)
- `filter` - ongoing, upcoming, past, all
- `sort` - prize, date, registrations
- `search` - Search term

**Response (200):**
```json
{
  "success": true,
  "data": [
    {
      "id": "507f1f77bcf86cd799439011",
      "title": "AI for Climate Change",
      "description": "Build AI solutions...",
      "organizer": {
        "id": "507f1f77bcf86cd799439012",
        "name": "TechCorp"
      },
      "theme": "AI/ML",
      "mode": "online",
      "startDate": "2024-03-15T00:00:00Z",
      "endDate": "2024-03-17T00:00:00Z",
      "registrationDeadline": "2024-03-14T23:59:59Z",
      "prizePool": 50000,
      "prizes": {
        "first": 25000,
        "second": 15000,
        "third": 10000
      },
      "teamSize": { "min": 1, "max": 4 },
      "registeredTeams": 248,
      "maxTeams": 500,
      "status": "registering",
      "image": "https://..."
    }
  ],
  "pagination": {
    "page": 1,
    "limit": 10,
    "total": 45,
    "pages": 5
  }
}
```

---

### Get Hackathon Details
```http
GET /api/hackathons/:id
Authorization: Bearer <token>
```

**Response (200):**
```json
{
  "success": true,
  "data": {
    "id": "507f1f77bcf86cd799439011",
    "title": "AI for Climate Change",
    "description": "...",
    "rules": "No plagiarism...",
    "requirements": {
      "skills": ["Python", "Machine Learning"],
      "experience": "Beginner"
    },
    "prizes": { /* ... */ },
    "sponsors": [
      {
        "name": "Microsoft",
        "logo": "https://...",
        "benefits": "Free Azure credits"
      }
    ],
    "judges": [
      {
        "name": "Jane Smith",
        "expertise": "AI/ML"
      }
    ],
    "schedule": [
      {
        "event": "Kick-off",
        "time": "2024-03-15T10:00:00Z"
      },
      {
        "event": "Submission Deadline",
        "time": "2024-03-17T23:59:59Z"
      }
    ]
  }
}
```

---

### Create Hackathon (Organization Only)
```http
POST /api/hackathons
Authorization: Bearer <token>
Content-Type: application/json

{
  "title": "Web Development Hackathon",
  "description": "Build amazing web apps",
  "theme": "web",
  "mode": "online",
  "startDate": "2024-04-01T00:00:00Z",
  "endDate": "2024-04-02T23:59:59Z",
  "registrationDeadline": "2024-03-31T23:59:59Z",
  "prizePool": 25000,
  "prizes": {
    "first": 12000,
    "second": 8000,
    "third": 5000
  },
  "teamSize": { "min": 1, "max": 4 },
  "maxTeams": 200,
  "requirements": {
    "skills": ["React", "Node.js"],
    "experience": "Intermediate"
  }
}
```

**Response (201):**
```json
{
  "success": true,
  "message": "Hackathon created",
  "data": { /* created hackathon */ }
}
```

---

### Register for Hackathon
```http
POST /api/hackathons/:id/register
Authorization: Bearer <token>
Content-Type: application/json

{
  "teamId": "507f1f77bcf86cd799439015",
  "or": {
    "teamName": "Innovation Squad",
    "members": ["507f1f77bcf86cd799439016"]
  }
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "Registered for hackathon",
  "registration": {
    "hackathonId": "507f1f77bcf86cd799439011",
    "teamId": "507f1f77bcf86cd799439015",
    "registeredAt": "2024-03-10T14:30:00Z",
    "status": "confirmed"
  }
}
```

---

## 👥 Team Endpoints

### Get All Teams
```http
GET /api/teams?hackathonId=507f1f77bcf86cd799439011&page=1&limit=20
Authorization: Bearer <token>
```

**Response (200):**
```json
{
  "success": true,
  "data": [
    {
      "id": "507f1f77bcf86cd799439015",
      "name": "Innovation Squad",
      "hackathon": "507f1f77bcf86cd799439011",
      "members": [
        {
          "id": "507f1f77bcf86cd799439016",
          "name": "Alice Roberts",
          "role": "Frontend",
          "skills": ["React"]
        },
        {
          "id": "507f1f77bcf86cd799439017",
          "name": "Bob Johnson",
          "role": "Backend",
          "skills": ["Node.js"]
        }
      ],
      "project": {
        "title": "ClimateAI",
        "description": "..."
      },
      "status": "active",
      "score": 850,
      "rank": 2,
      "createdAt": "2024-03-01T10:00:00Z"
    }
  ],
  "pagination": { /* ... */ }
}
```

---

### Create Team
```http
POST /api/teams
Authorization: Bearer <token>
Content-Type: application/json

{
  "name": "Tech Titans",
  "description": "A team of passionate developers",
  "hackathonId": "507f1f77bcf86cd799439011",
  "members": [
    {
      "userId": "507f1f77bcf86cd799439016",
      "role": "Frontend Developer"
    },
    {
      "userId": "507f1f77bcf86cd799439017",
      "role": "Backend Developer"
    }
  ]
}
```

**Response (201):**
```json
{
  "success": true,
  "message": "Team created",
  "data": { /* created team */ },
  "invites": {
    "sent": 1,
    "pending": 1
  }
}
```

---

### Join Team
```http
POST /api/teams/join
Authorization: Bearer <token>
Content-Type: application/json

{
  "teamCode": "TECH2024"
}
```

**Response (200):**
```json
{
  "success": true,
  "message": "Joined team",
  "team": { /* team data */ }
}
```

---

### Leave Team
```http
POST /api/teams/:id/leave
Authorization: Bearer <token>
```

**Response (200):**
```json
{
  "success": true,
  "message": "Left team"
}
```

---

## 💬 Notification Endpoints

### Get Notifications
```http
GET /api/notifications?unread=true&page=1&limit=20
Authorization: Bearer <token>
```

**Query Parameters:**
- `unread` - true/false (filter unread)
- `page` - Page number
- `limit` - Results per page
- `type` - Filter by type

**Response (200):**
```json
{
  "success": true,
  "data": [
    {
      "id": "507f1f77bcf86cd799439020",
      "type": "team-invite",
      "title": "Team Invitation",
      "message": "You've been invited to join TechCorp Team",
      "link": "/teams/507f1f77bcf86cd799439015",
      "isRead": false,
      "priority": "high",
      "createdAt": "2024-03-10T14:30:00Z"
    }
  ],
  "unreadCount": 5
}
```

---

### Mark Notification as Read
```http
PUT /api/notifications/:id/read
Authorization: Bearer <token>
```

**Response (200):**
```json
{
  "success": true,
  "message": "Notification marked as read"
}
```

---

### Mark All as Read
```http
PUT /api/notifications/read-all
Authorization: Bearer <token>
```

**Response (200):**
```json
{
  "success": true,
  "message": "All notifications marked as read",
  "count": 5
}
```

---

### Delete Notification
```http
DELETE /api/notifications/:id
Authorization: Bearer <token>
```

**Response (200):**
```json
{
  "success": true,
  "message": "Notification deleted"
}
```

---

## 🛒 Marketplace Endpoints

### Get Marketplace Projects
```http
GET /api/marketplace/projects?category=ai&sort=rating&page=1&limit=12
Authorization: Bearer <token>
```

**Query Parameters:**
- `category` - ai, web, mobile, iot, etc.
- `sort` - rating, views, latest
- `page` - Pagination
- `limit` - Results per page
- `search` - Search term

**Response (200):**
```json
{
  "success": true,
  "data": [
    {
      "id": "507f1f77bcf86cd799439021",
      "title": "ClimateAI",
      "description": "AI-powered climate analysis tool",
      "team": {
        "id": "507f1f77bcf86cd799439015",
        "name": "EcoWarriors",
        "members": [...]
      },
      "hackathon": {
        "id": "507f1f77bcf86cd799439011",
        "name": "AI for Climate"
      },
      "category": "ai",
      "technologies": ["Python", "TensorFlow"],
      "links": {
        "github": "https://github.com/...",
        "demo": "https://climateai.app"
      },
      "rating": 4.8,
      "reviews": 12,
      "views": 450
    }
  ],
  "pagination": { /* ... */ }
}
```

---

## 🔔 WebSocket Events (Socket.io)

### Connecting
```javascript
import io from 'socket.io-client';

const socket = io('http://localhost:3001', {
  auth: {
    token: 'your-jwt-token'
  }
});
```

### IDE Collaboration Events
```javascript
// Code changes
socket.emit('code-changed', {
  fileId: 'file-123',
  content: 'new code',
  userId: 'user-456'
});

socket.on('code-changed', (data) => {
  // Update local code editor
});

// Cursor tracking
socket.emit('cursor-moved', {
  line: 10,
  column: 5,
  userId: 'user-456'
});

socket.on('cursor-moved', (data) => {
  // Update cursor position visualization
});

// Chat messages
socket.emit('chat-message', {
  message: 'Let's use this approach',
  teamId: 'team-123'
});

socket.on('chat-message', (data) => {
  // Display new chat message
});
```

### Notification Events
```javascript
// New notification
socket.on('notification', (data) => {
  console.log('New notification:', data);
});

// Notification read
socket.on('notification-read', (id) => {
  console.log('Notification marked read:', id);
});
```

---

## ⚠️ Error Responses

### Standard Error Format
```json
{
  "success": false,
  "error": "Error description",
  "statusCode": 400,
  "timestamp": "2024-03-10T14:30:00Z"
}
```

### Validation Error
```json
{
  "success": false,
  "error": "Validation failed",
  "statusCode": 422,
  "details": [
    {
      "field": "email",
      "message": "Invalid email format"
    },
    {
      "field": "password",
      "message": "Password must be at least 8 characters"
    }
  ]
}
```

### Authentication Error
```json
{
  "success": false,
  "error": "Unauthorized",
  "statusCode": 401,
  "message": "Invalid or expired token"
}
```

### Not Found Error
```json
{
  "success": false,
  "error": "Not found",
  "statusCode": 404,
  "message": "Hackathon with ID 507f1f77bcf86cd799439011 not found"
}
```

---

## 🔑 Authentication Header

All protected endpoints require the Authorization header:

```http
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

The token is automatically included in HTTP-only cookies by NextAuth.js, but you can also send it in the header.

---

## 📊 Rate Limiting

API endpoints have rate limits:
- **Auth endpoints**: 5 requests per minute
- **General endpoints**: 100 requests per minute
- **File upload**: 10 MB per request

**Rate limit exceeded response:**
```json
{
  "success": false,
  "error": "Rate limit exceeded",
  "statusCode": 429,
  "retryAfter": 60
}
```

---

## 🧪 Testing API Endpoints

### Using cURL
```bash
# Get all hackathons
curl -X GET http://localhost:3000/api/hackathons \
  -H "Authorization: Bearer YOUR_TOKEN"

# Create hackathon
curl -X POST http://localhost:3000/api/hackathons \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"title": "Web Hackathon", ...}'
```

### Using Postman
1. Import collection from docs
2. Set environment variables (token, baseUrl)
3. Run requests with pre-configured auth

### Using Thunder Client (VS Code)
Code extension with built-in test history.

---

**Happy API integrating! 🚀**
