# 🏗️ System Architecture

Technical architecture, data flow, and system design of HackShield Portal.

---

## 📐 High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         CLIENT LAYER                            │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐           │
│  │   Browser    │  │  Mobile Web  │  │   PWA App    │           │
│  │   (React)    │  │   (React)    │  │   (React)    │           │
│  └──────────────┘  └──────────────┘  └──────────────┘           │
└─────────────────────────────────────────────────────────────────┘
              ▼                    ▼                  ▼
┌─────────────────────────────────────────────────────────────────┐
│                    API & SERVICES LAYER                         │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │        Next.js API Routes (Serverless)                  │   │
│  ├──────────────────────────────────────────────────────────┤   │
│  │ • Authentication   • Hackathons    • Teams               │   │
│  │ • Projects         • Notifications • Marketplace         │   │
│  │ • User Management  • Analytics     • Admin               │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
              ▼                    ▼                  ▼
┌─────────────────────────────────────────────────────────────────┐
│                    BUSINESS LOGIC LAYER                         │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │ • Authorization & Access Control                         │   │
│  │ • Smart Team Matching Algorithm                          │   │
│  │ • Validation & Data Processing                           │   │
│  │ • Notification Engine                                    │   │
│  │ • AI/ML Services                                         │   │
│  │ • File Processing                                        │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
              ▼                    ▼                  ▼
┌─────────────────────────────────────────────────────────────────┐
│                    DATA ACCESS LAYER                            │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │     Mongoose ODM (Object-Document Mapper)               │   │
│  │  Models & Schemas, Query Builders, Middleware           │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
              ▼                    ▼                  ▼
┌─────────────────────────────────────────────────────────────────┐
│                    PERSISTENCE LAYER                            │
│  ┌──────────────────────────────────────────────────────────┐   │
│  │     MongoDB Atlas (Cloud Database)                       │   │
│  │  Collections: Users, Teams, Projects, etc.              │   │
│  └──────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────┘
              ▼                    ▼                  ▼
┌─────────────────────────────────────────────────────────────────┐
│                  SUPPORTING SERVICES                            │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐           │
│  │   Email      │  │   File       │  │   Cache      │           │
│  │   Service    │  │   Storage    │  │   (Redis)    │           │
│  │  (Nodemailer)│  │   (AWS S3)   │  │              │           │
│  └──────────────┘  └──────────────┘  └──────────────┘           │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🔄 Request/Response Cycle

```
User Action
    ▼
┌─────────────────────┐
│  Next.js Client     │
│  (React Component)  │
│                     │
│ • Validates input   │
│ • Shows loading UI  │
│ • Handles errors    │
└──────────┬──────────┘
           ▼
    HTTP Request
      (with JWT)
           ▼
┌─────────────────────┐
│  API Route Handler  │
│  (/app/api/...)     │
│                     │
│ • Verify JWT token  │
│ • Validate request  │
│ • Check permissions │
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│  Business Logic     │
│  (/lib, /utils)     │
│                     │
│ • Process data      │
│ • Run algorithms    │
│ • Validate rules    │
└──────────┬──────────┘
           ▼
┌─────────────────────┐
│  Database Query     │
│  (Mongoose)         │
│                     │
│ • Find/Create/Update│
│ • Save to MongoDB   │
│ • Return results    │
└──────────┬──────────┘
           ▼
    HTTP Response
      (JSON data)
           ▼
┌─────────────────────┐
│  Next.js Client     │
│  (React Component)  │
│                     │
│ • Update state      │
│ • Re-render UI      │
│ • Show results      │
└─────────────────────┘
```

---

## 🔐 Authentication Flow

### Registration
```
User Registration Form
    ▼
Validate Email & Password
    ▼
Hash Password (bcrypt)
    ▼
Create User in MongoDB
    ▼
Generate JWT Token
    ▼
Store in HTTP-only Cookie
    ▼
Redirect to Dashboard
```

### Login
```
Email & Password Input
    ▼
Find User in MongoDB
    ▼
Compare Password (bcrypt)
    ▼
Generate JWT Token
    ▼
Store in HTTP-only Cookie
    ▼
Create NextAuth Session
    ▼
Redirect to Dashboard
```

### API Request with Auth
```
API Request made
    ▼
Middleware checks JWT cookie
    ▼
Verify JWT signature
    ▼
Check token expiration
    ▼
Allow/Deny request
    ▼
Request processed or Rejected
```

---

## 📊 Database Schema Relationships

```
┌─────────────┐
│    User     │
├─────────────┤
│ _id (PK)    │
│ email       │
│ password    │
│ name        │
│ role        │
│ profile     │
│ createdAt   │
└──────┬──────┘
       │
       ├─────────────────────┬─────────────────────┐
       ▼                     ▼                     ▼
┌─────────────┐        ┌─────────────┐      ┌─────────────┐
│    Team     │        │  Project    │      │Notification │
├─────────────┤        ├─────────────┤      ├─────────────┤
│ _id (FK)    │        │ _id (FK)    │      │ _id (FK)    │
│ members[]   │        │ teamId (FK) │      │ userId (FK) │
│ hackId (FK) │        │ links[]     │      │ type        │
│ project (FK)│        │ createdAt   │      │ message     │
│ score       │        └─────────────┘      │ isRead      │
└──────┬──────┘                             └─────────────┘
       │
       └─────────────────────┐
                             ▼
                      ┌─────────────┐
                      │  Hackathon  │
                      ├─────────────┤
                      │ _id (PK)    │
                      │ title       │
                      │ orgId (FK)  │
                      │ teams[]     │
                      │ prizes      │
                      │ createdAt   │
                      └─────────────┘

Legend:
PK = Primary Key
FK = Foreign Key
[] = Array/Reference to multiple documents
```

---

## 🔌 Real-Time Features (Socket.io)

```
Client Browser
    ▼
WebSocket Connection (Socket.io)
    ▼
┌──────────────────────────────┐
│   Socket Events              │
├──────────────────────────────┤
│ • user-joined                │
│ • code-changed               │
│ • cursor-moved               │
│ • chat-message               │
│ • file-saved                 │
│ • notification               │
│ • activity-update            │
└──────────────────────────────┘
    ▼
Server (Socket.io Handler)
    ▼
Broadcast to Other Clients
    ▼
Update UI in Real-Time
    ▼
Reflect Changes for All Users
```

---

## 🎯 State Management Architecture

```
Global State (Zustand)
├── Auth State
│   ├── user object
│   ├── isAuthenticated
│   ├── accessToken
│   └── sessionExpiry
│
├── UI State
│   ├── sidebarOpen
│   ├── themeMode
│   ├── selectedHackathon
│   └── notificationCount
│
├── IDE State
│   ├── openFiles[]
│   ├── activeFile
│   ├── unsavedChanges
│   ├── terminalOutput
│   └── previewUrl
│
├── Team State
│   ├── currentTeam
│   ├── teamMembers[]
│   ├── teamChat[]
│   └── collaborators[]
│
└── Notifications
    ├── notifications[]
    ├── unread count
    └── preferences
```

---

## 🚀 Deployment Architecture

### Development
```
Developer Machine
    ▼
npm run dev
    ▼
Local Next.js Server (port 3000)
    ▼
LocalMongoDBAtlas (test cluster)
    ▼
Browser (http://localhost:3000)
```

### Production
```
GitHub Repository
    ▼
Vercel Deploy Trigger
    ▼
Build Process
├── Compile TypeScript
├── Build Next.js bundle
├── Run tests
└── Generate optimized output
    ▼
Deploy to Vercel CDN
├── Edge Network
├── Serverless Functions
└── Static Assets
    ▼
MongoDB Atlas (production cluster)
    ▼
Live Application
├── https://hackshield.vercel.app
├── Auto SSL/TLS
├── CDN caching
└── Automatic scaling
```

---

## 🔒 Security Architecture

```
┌──────────────────────────────────────┐
│        Security Layers               │
├──────────────────────────────────────┤
│                                      │
│  1. HTTPS/TLS Encryption             │
│     └─ Encrypts data in transit      │
│                                      │
│  2. CORS Policy                      │
│     └─ Restricts cross-origin req    │
│                                      │
│  3. Request Validation               │
│     └─ Validates request payload     │
│                                      │
│  4. Authentication (JWT)             │
│     └─ HTTP-only cookies             │
│     └─ Token expiration              │
│     └─ Signature verification        │
│                                      │
│  5. Authorization (Role-based)       │
│     └─ Checks user permissions       │
│     └─ Route-level middleware        │
│                                      │
│  6. Database Security                │
│     └─ MongoDB IP whitelist          │
│     └─ Database user: limited priv   │
│     └─ Password hashing (bcrypt)     │
│                                      │
│  7. Input Sanitization               │
│     └─ Zod schema validation         │
│     └─ XSS prevention                │
│     └─ SQL injection prevention      │
│                                      │
│  8. Rate Limiting                    │
│     └─ API endpoint throttling       │
│                                      │
└──────────────────────────────────────┘
```

---

## 📈 Scalability Design

### Horizontal Scaling
- **Stateless API Routes** - Can run on multiple servers
- **Database Connection Pooling** - MongoDB Atlas handles scaling
- **CDN Distribution** - Vercel edge network

### Caching Strategy
```
├── Page Caching (Next.js ISR)
│   └─ Static pages revalidated periodically
├── API Caching
│   └─ User data cached in session
└── Database Queries
    └─ Frequently accessed data indexed
```

### Database Optimization
```
├── Indexing
│   ├─ User email (unique index)
│   ├─ Team members (compound index)
│   └─ Hackathon dates (range index)
├── Query Optimization
│   ├─ Lean queries (select specific fields)
│   ├─ Pagination (limit result sets)
│   └─ Populate (eager loading)
└── Connection Management
    └─ Connection pooling
```

---

## 🔄 Data Flow Examples

### User Registration Flow
```
1. User fills form
   ▼
2. Client validates (React Hook Form + Zod)
   ▼
3. Submit to /api/auth/register
   ▼
4. Server validates request body
   ▼
5. Check email not already used
   ▼
6. Hash password with bcrypt
   ▼
7. Create User document in MongoDB
   ▼
8. Generate JWT token
   ▼
9. Return token + user data
   ▼
10. Store token in cookie
   ▼
11. Redirect to dashboard
```

### Team Formation Flow
```
1. User clicks "Create Team"
   ▼
2. Form modal opens
   ▼
3. User enters team name, members
   ▼
4. Client validates
   ▼
5. POST /api/teams with team data
   ▼
6. Server validates team data
   ▼
7. Check user permissions
   ▼
8. Create Team document
   ▼
9. Send invites to team members
   ▼
10. Update User documents (teams ref)
   ▼
11. Send notifications to invitees
   ▼
12. Return team data to client
   ▼
13. Update local state
   ▼
14. Show team formation success
```

### Real-Time IDE Collaboration
```
User 1 edits code
   ▼
Change event captured
   ▼
Emit "code-changed" via Socket.io
   ▼
Server receives event
   ▼
Broadcast to all team members
   ▼
User 2 & 3 receive update
   ▼
Local state updated
   ▼
Editor re-renders with new code
   ▼
Cursor positions updated too
   ▼
Live collaboration visible
```

---

## 🛠️ API Architecture

### RESTful Endpoints
```
Authentication:
POST   /api/auth/register
POST   /api/auth/login
POST   /api/auth/logout
POST   /api/auth/refresh-token

Users:
GET    /api/users/:id
PUT    /api/users/:id
DELETE /api/users/:id

Teams:
GET    /api/teams
POST   /api/teams
GET    /api/teams/:id
PUT    /api/teams/:id
DELETE /api/teams/:id

Projects:
GET    /api/projects
POST   /api/projects
GET    /api/projects/:id

Hackathons:
GET    /api/hackathons
POST   /api/hackathons
GET    /api/hackathons/:id
PUT    /api/hackathons/:id

Notifications:
GET    /api/notifications
POST   /api/notifications
PUT    /api/notifications/:id/read
DELETE /api/notifications/:id
```

### Status Codes
```
✅ 200 - Success
✅ 201 - Created
✅ 204 - No Content
❌ 400 - Bad Request
❌ 401 - Unauthorized
❌ 403 - Forbidden
❌ 404 - Not Found
❌ 409 - Conflict
❌ 422 - Validation Error
❌ 500 - Server Error
```

---

## 🎨 Component Hierarchy

```
App (root layout)
├── Providers (NextAuth, Zustand)
│
├── Auth Pages
│   ├── Login
│   └── Register
│
├── Dashboard Layout
│   ├── Sidebar Navigation
│   ├── Header Bar
│   └── Page Content
│       ├── Participant Dashboard
│       ├── Organization Dashboard
│       ├── IDE
│       ├── Team Management
│       ├── Notifications
│       └── Settings
│
└── Public Pages
    ├── Landing Page
    ├── Hackathon Browse
    └── Marketplace
```

---

## 📡 Environment Variables & Configuration

```
Production (.env.local):
├── Database
│   └── MONGODB_URI
├── Authentication
│   ├── NEXTAUTH_URL
│   ├── NEXTAUTH_SECRET
│   └── JWT_SECRET
├── OAuth (Optional)
│   ├── GOOGLE_*
│   └── GITHUB_*
├── Email (Optional)
│   ├── SMTP_*
│   └── EMAIL_FROM
└── Services (Optional)
    └── SOCKET_SERVER_URL
```

---

**This architecture ensures scalability, security, and maintainability! 🔐🚀**
