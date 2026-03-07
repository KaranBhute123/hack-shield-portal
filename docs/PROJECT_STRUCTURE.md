# 📁 Project Structure Overview

Complete file organization and component breakdown for HackShield Portal.

---

## 🏗️ Directory Structure

```
hackshield-portal/
│
├── 📄 Configuration Files
│   ├── next.config.js           - Next.js server config
│   ├── tsconfig.json            - TypeScript compiler settings
│   ├── tailwind.config.js       - Tailwind CSS theme customization
│   ├── postcss.config.js        - CSS post-processing
│   ├── package.json             - Project dependencies and scripts
│   ├── package-lock.json        - Dependency lock file
│   ├── .env.example             - Environment variables template
│   ├── .env.local               - Local environment (not in git)
│   ├── .gitignore               - Git exclusion patterns
│   └── middleware.ts            - Next.js middleware for auth
│
├── 🌐 App Directory (Next.js 14 App Router)
│   └── app/
│       ├── page.tsx                    - Landing page (/)
│       ├── layout.tsx                  - Root layout wrapper
│       ├── globals.css                 - Global CSS styles
│       ├── providers.tsx               - Context providers (NextAuth, etc.)
│       │
│       ├── 🔐 auth/                    - Authentication pages
│       │   ├── page.tsx                - Auth hub
│       │   ├── login/
│       │   │   └── page.tsx            - Login page (/auth/login)
│       │   └── register/
│       │       └── page.tsx            - Register page (/auth/register)
│       │
│       ├── 🎯 dashboard/               - Protected dashboard routes
│       │   ├── page.tsx                - Dashboard home (/dashboard)
│       │   ├── layout.tsx              - Dashboard layout with sidebar
│       │   ├── analytics/
│       │   │   └── page.tsx            - Analytics dashboard
│       │   ├── hackathons/
│       │   │   └── page.tsx            - Browse hackathons
│       │   ├── ide/
│       │   │   └── page.tsx            - Lockdown IDE
│       │   ├── investments/
│       │   │   └── page.tsx            - Investment tracking
│       │   ├── judging/
│       │   │   └── page.tsx            - Judging interface
│       │   ├── manage/
│       │   │   └── page.tsx            - Event management
│       │   ├── messages/
│       │   │   └── page.tsx            - Direct messaging
│       │   ├── monitor/
│       │   │   └── page.tsx            - Participant monitoring
│       │   ├── notifications/
│       │   │   └── page.tsx            - Notification center
│       │   ├── organization/
│       │   │   └── page.tsx            - Organization dashboard
│       │   ├── profile/
│       │   │   └── page.tsx            - User profile
│       │   ├── projects/
│       │   │   └── page.tsx            - User projects
│       │   ├── settings/
│       │   │   └── page.tsx            - User settings
│       │   └── teams/
│       │       └── page.tsx            - Team management
│       │
│       ├── 📌 hackathons/              - Hackathon browsing pages
│       │   ├── page.tsx                - All hackathons (/hackathons)
│       │   └── [id]/                   - Dynamic hackathon routes
│       │       ├── page.tsx            - Hackathon details
│       │       ├── find-team/
│       │       │   └── page.tsx        - Team finder for event
│       │       ├── ide/
│       │       │   └── page.tsx        - IDE during hackathon
│       │       ├── ide-access/
│       │       │   └── page.tsx        - IDE access control
│       │       ├── monitor/
│       │       │   └── page.tsx        - Event monitoring
│       │       ├── register/
│       │       │   └── page.tsx        - Hackathon registration
│       │       ├── team-formation/
│       │       │   └── page.tsx        - Team formation UI
│       │       └── browse/
│       │           └── page.tsx        - Browse hackathons
│       │
│       ├── 🛒 marketplace/             - Project marketplace
│       │   └── page.tsx                - Marketplace view (/marketplace)
│       │
│       ├── 🔔 notifications/           - Notifications page
│       │   └── page.tsx                - Notification center (/notifications)
│       │
│       └── 🔌 api/                     - Next.js API Routes
│           ├── ai/
│           │   └── chat/
│           │       └── route.ts        - AI chat endpoint
│           │
│           ├── auth/                   - Authentication endpoints
│           │   ├── [...nextauth]/
│           │   │   └── route.ts        - NextAuth provider routes
│           │   └── register/
│           │       └── route.ts        - User registration
│           │
│           ├── hackathons/             - Hackathon management
│           │   ├── route.ts            - GET/POST hackathons
│           │   ├── [id]/route.ts       - GET/PUT/DELETE specific
│           │   ├── [id]/ai-assistant/
│           │   │   └── route.ts        - AI assistance
│           │   ├── [id]/branches/
│           │   │   └── route.ts        - Git branches
│           │   ├── [id]/deploy/
│           │   │   └── route.ts        - Deployment endpoint
│           │   ├── [id]/execute-code/
│           │   │   └── route.ts        - Code execution
│           │   ├── [id]/ide-activity/
│           │   │   └── route.ts        - Activity logging
│           │   ├── [id]/ide-auth/
│           │   │   └── route.ts        - IDE authentication
│           │   ├── [id]/ide-credentials/
│           │   │   └── route.ts        - IDE credentials
│           │   ├── [id]/ide-disqualify/
│           │   │   └── route.ts        - Disqualification
│           │   ├── [id]/ide-schedule/
│           │   │   └── route.ts        - Event scheduling
│           │   ├── [id]/monitor/
│           │   │   ├── activities/
│           │   │   │   └── route.ts    - Activity monitoring
│           │   │   └── teams/
│           │   │       └── route.ts    - Team monitoring
│           │   ├── [id]/notifications/
│           │   │   └── route.ts        - Event notifications
│           │   ├── [id]/open-invites/
│           │   │   └── route.ts        - Open invitations
│           │   ├── [id]/participants/
│           │   │   └── route.ts        - Participant list
│           │   ├── [id]/preview/
│           │   │   └── route.ts        - Event preview
│           │   ├── [id]/register/
│           │   │   └── route.ts        - Event registration
│           │   ├── [id]/select-team/
│           │   │   └── route.ts        - Team selection
│           │   ├── [id]/send-credentials/
│           │   │   └── route.ts        - Send IDE credentials
│           │   ├── [id]/smart-matching/
│           │   │   └── route.ts        - AI team matching
│           │   ├── [id]/status/
│           │   │   └── route.ts        - Event status
│           │   ├── [id]/team/route.ts  - Team operations
│           │   ├── [id]/team-files/
│           │   │   └── route.ts        - File management
│           │   ├── [id]/team-matching/
│           │   │   └── route.ts        - Team matching
│           │   ├── [id]/teams/
│           │   │   └── route.ts        - Teams list
│           │   ├── [id]/terminal/
│           │   │   └── route.ts        - Terminal emulation
│           │   ├── [id]/verify-access/
│           │   │   └── route.ts        - Access verification
│           │   ├── my/route.ts         - User's hackathons
│           │   ├── upload-ppt/
│           │   │   └── route.ts        - PPT upload
│           │   └── violations/
│           │       └── route.ts        - Violation reports
│           │
│           ├── marketplace/            - Marketplace API
│           │   ├── contributors/
│           │   │   └── route.ts        - Contributor listing
│           │   └── projects/
│           │       └── route.ts        - Project listing
│           │
│           ├── notifications/          - Notification system
│           │   ├── route.ts            - GET/POST notifications
│           │   ├── [id]/route.ts       - Individual notification
│           │   ├── [id]/read/
│           │   │   └── route.ts        - Mark as read
│           │   ├── archive/
│           │   │   └── route.ts        - Archive notification
│           │   ├── delete/
│           │   │   └── route.ts        - Delete notification
│           │   ├── mark-all-read/
│           │   │   └── route.ts        - Mark all read
│           │   ├── preferences/
│           │   │   └── route.ts        - User preferences
│           │   ├── read-all/
│           │   │   └── route.ts        - Read all notifications
│           │   ├── reminders/
│           │   │   └── route.ts        - Reminder system
│           │   └── test/
│           │       └── route.ts        - Test notification
│           │
│           ├── projects/
│           │   └── route.ts            - Project endpoints
│           │
│           ├── teams/                  - Team management
│           │   ├── route.ts            - GET/POST teams
│           │   ├── [id]/route.ts       - Individual team
│           │   ├── [id]/invite/
│           │   │   └── route.ts        - Team invite
│           │   ├── [id]/leave/
│           │   │   └── route.ts        - Leave team
│           │   ├── [id]/project/
│           │   │   └── route.ts        - Team project
│           │   ├── join/route.ts       - Join team
│           │   └── my/route.ts         - User's teams
│           │
│           └── user/                   - User endpoints
│               ├── route.ts            - User profile
│               └── stats/route.ts      - User statistics
│
├── 🎨 Components (Reusable UI)
│   └── components/
│       ├── dashboard/
│       │   ├── ParticipantDashboard.tsx    - Participant view
│       │   ├── OrganizationDashboard.tsx   - Organization view
│       │   └── ContributorDashboard.tsx    - Contributor view
│       │
│       ├── hackathons/
│       │   ├── RegistrationForm.tsx        - Registration form
│       │   └── RegistrationButton.tsx      - Registration button
│       │
│       ├── ide/
│       │   ├── AIAssistant.tsx             - AI helper panel
│       │   ├── CollaborativeFiles.tsx      - Real-time collab
│       │   ├── FileExplorer.tsx            - File browser
│       │   ├── IDELockdown.tsx             - Security layer
│       │   ├── LiveCursors.tsx             - Cursor tracking
│       │   ├── LivePreview.tsx             - Live preview pane
│       │   ├── SettingsPanel.tsx           - IDE settings
│       │   ├── TeamVideoChat.tsx           - Video chat
│       │   └── Terminal.tsx                - Terminal emulator
│       │
│       ├── team/
│       │   └── BrowseParticipants.tsx      - Participant browser
│       │
│       └── organization/
│           └── MonitoringDashboard.tsx     - Monitoring view
│
├── 📚 Utilities & Libraries
│   └── lib/
│       ├── auth.ts                         - Auth utilities
│       ├── database.ts                     - DB utilities
│       ├── auth/
│       │   ├── authOptions.ts              - NextAuth config
│       │   └── [other auth utils]
│       └── db/
│           ├── connect.ts                  - MongoDB connection
│           └── models/
│               └── [other schemas]
│
├── 💾 Database Models (MongoDB Schemas)
│   └── models/
│       ├── User.ts                         - User schema
│       │   ├── email (unique)
│       │   ├── password (hashed)
│       │   ├── name
│       │   ├── role (participant/org/contrib)
│       │   ├── profile (bio, skills, etc.)
│       │   ├── achievements (awards, XP)
│       │   ├── notifications settings
│       │   └── createdAt, updatedAt
│       │
│       ├── Team.ts                         - Team schema
│       │   ├── name
│       │   ├── members (user IDs)
│       │   ├── hackathon (hackathon ID)
│       │   ├── status (active, completed)
│       │   ├── project (project details)
│       │   ├── rank, score
│       │   └── createdAt, updatedAt
│       │
│       ├── Project.ts                      - Project schema
│       │   ├── title
│       │   ├── description
│       │   ├── team (team ID)
│       │   ├── links (GitHub, demo, etc.)
│       │   ├── rating, reviews
│       │   ├── tags
│       │   └── createdAt, updatedAt
│       │
│       ├── Notification.ts                 - Notification schema
│       │   ├── user (recipient)
│       │   ├── type (event, message, etc.)
│       │   ├── message
│       │   ├── isRead
│       │   ├── link
│       │   └── createdAt, updatedAt
│       │
│       ├── NotificationPreferences.ts      - User preferences
│       │   ├── user
│       │   ├── email (enabled/disabled)
│       │   ├── sms (enabled/disabled)
│       │   ├── push (enabled/disabled)
│       │   ├── categories
│       │   └── frequency
│       │
│       └── Contributor.ts                  - Contributor schema
│           ├── user
│           ├── bio
│           ├── skills
│           ├── portfolio
│           ├── investments
│           └── createdAt, updatedAt
│
├── 🎨 Public Assets
│   └── public/
│       ├── uploads/
│       │   └── ppts/                       - Uploaded PPT files
│       ├── [other assets]
│       └── favicon.ico
│
├── 📝 Type Definitions
│   └── types/
│       ├── next-auth.d.ts                  - NextAuth types
│       └── [other type defs]
│
├── 📄 Documentation
│   └── docs/
│       ├── PROJECT_STRUCTURE.md            - This file
│       ├── ARCHITECTURE.md                 - System architecture
│       ├── FEATURES.md                     - Features list
│       ├── GETTING_STARTED.md              - Setup guide
│       └── API_DOCUMENTATION.md            - API reference
│
└── 📋 Root Files
    ├── README.md                           - Main documentation
    ├── .env.example                        - Environment template
    ├── .gitignore                          - Git ignore rules
    ├── package.json                        - Dependencies & scripts
    ├── tsconfig.json                       - TypeScript config
    └── middleware.ts                       - Auth middleware
```

---

## 🌳 Page Routes Map

```
/                                    - Landing page
/auth/login                          - User login
/auth/register                       - New user registration

/dashboard                           - Main dashboard hub
/dashboard/analytics                 - Analytics view
/dashboard/hackathons                - Browse hackathons
/dashboard/ide                       - IDE interface
/dashboard/investments               - Investment tracking
/dashboard/judging                   - Judging interface
/dashboard/manage                    - Event management
/dashboard/messages                  - Messaging
/dashboard/monitor                   - Participant monitor
/dashboard/notifications             - Notification center
/dashboard/organization              - Org dashboard
/dashboard/profile                   - User profile
/dashboard/projects                  - User projects
/dashboard/settings                  - User settings
/dashboard/teams                     - Team management

/hackathons                          - All hackathons
/hackathons/[id]                     - Hackathon details
/hackathons/[id]/find-team           - Team finder
/hackathons/[id]/ide                 - IDE workspace
/hackathons/[id]/ide-access          - IDE access control
/hackathons/[id]/monitor             - Event monitoring
/hackathons/[id]/register            - Registration
/hackathons/[id]/team-formation      - Team formation
/hackathons/browse                   - Browse all

/marketplace                         - Project marketplace
/notifications                       - Notifications center
```

---

## 🔌 API Routes Map

```
Authentication:
  POST   /api/auth/register          - User registration
  GET    /api/auth/[...nextauth]     - NextAuth endpoints
  POST   /api/auth/[...nextauth]

Hackathons:
  GET    /api/hackathons             - List all
  POST   /api/hackathons             - Create
  GET    /api/hackathons/[id]        - Get one
  PUT    /api/hackathons/[id]        - Update
  DELETE /api/hackathons/[id]        - Delete
  GET    /api/hackathons/my           - User's hackathons
  Various /api/hackathons/[id]/...   - Specific features

Teams:
  GET    /api/teams                  - List teams
  POST   /api/teams                  - Create team
  GET    /api/teams/[id]             - Get team
  PUT    /api/teams/[id]             - Update team
  DELETE /api/teams/[id]             - Delete team
  POST   /api/teams/join             - Join team
  POST   /api/teams/[id]/leave       - Leave team

Projects:
  GET    /api/projects               - List projects
  POST   /api/projects               - Create project
  GET    /api/marketplace/projects   - Marketplace

Notifications:
  GET    /api/notifications          - List notifications
  POST   /api/notifications          - Create
  PUT    /api/notifications/read-all - Mark all read
  PUT    /api/notifications/[id]/read- Mark read

User:
  GET    /api/user                   - User profile
  GET    /api/user/stats             - User stats
```

---

## 📦 Dependencies Organization

### Frontend Framework
- `next` - React framework
- `react` - UI library
- `react-dom` - React renderer

### UI & Styling
- `tailwindcss` - CSS framework
- `postcss` - CSS processing
- `framer-motion` - Animations
- `lucide-react` - Icons

### Forms & Validation
- `react-hook-form` - Form management
- `@hookform/resolvers` - Validation resolvers
- `zod` - Schema validation

### Authentication
- `next-auth` - Auth framework
- `@next-auth/mongodb-adapter` - MongoDB adapter
- `bcryptjs` - Password hashing
- `jsonwebtoken` - JWT tokens

### Database
- `mongoose` - MongoDB ODM
- `mongodb` - Database driver

### Real-time & Communication
- `socket.io` - WebSocket server
- `socket.io-client` - WebSocket client

### Code Editing
- `@monaco-editor/react` - Monaco editor wrapper
- `xterm` - Terminal emulator
- `xterm-addon-fit` - Terminal fit addon

### Utilities
- `date-fns` - Date utilities
- `uuid` - ID generation
- `clsx` - Class name utilities
- `react-hot-toast` - Toast notifications
- `recharts` - Data visualization
- `zustand` - State management
- `nodemailer` - Email sending

---

## 🔄 Data Flow Example

```
User Registration:
1. User fills form (frontend)
   └─→ /app/auth/register/page.tsx

2. Form submitted to API
   └─→ POST /api/auth/register

3. API validates and hashes password
   └─→ /lib/auth.ts

4. Save to MongoDB
   └─→ /models/User.ts

5. Create session with JWT
   └─→ /lib/auth/authOptions.ts

6. Redirect to dashboard
   └─→ /app/dashboard/page.tsx
```

---

## ✅ Component Usage Patterns

### Server Components (Default)
```typescript
// app/dashboard/page.tsx
export default async function Dashboard() {
  // Can access database directly
  // Can access secrets
  const data = await fetchUserData();
  return <div>{data}</div>;
}
```

### Client Components
```typescript
// components/IDE.tsx
'use client'; // Mark as client

import { useEffect } from 'react';

export function IDE() {
  useEffect(() => {
    // Browser APIs only
  }, []);
  return <div>IDE</div>;
}
```

---

## 🎯 Getting Around the Codebase

### Finding a Feature
1. Start at route in `/app`
2. Check component in `/components`
3. Review API route in `/app/api`
4. Check database model in `/models`
5. Review utility functions in `/lib`

### Making Changes
1. Identify component/page
2. Make edit
3. Check related API routes
4. Update database schema if needed
5. Test in browser with hot reload

### Adding New Feature
1. Create route in `/app`
2. Create component in `/components`
3. Create API endpoint in `/app/api`
4. Add database model in `/models`
5. Document in README/docs

---

**This structure promotes clean code organization and scalability!**
