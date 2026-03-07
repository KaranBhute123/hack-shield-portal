# 🚀 HackShield Portal

> **The Ultimate Hackathon Management & Collaboration Platform**

# 🥈 **RUNNER-UP** - Central India Hackathon 2026

> *Proudly securing 2nd place in a competitive hackathon with innovative features and professional execution*

A comprehensive, feature-rich platform designed to revolutionize hackathon experiences with secure coding environments, intelligent team matching, real-time collaboration, and project marketplace integration.

**[🏆 View Hackathon Achievement →](./HACKATHON_RESULTS.md)**

---

## 📌 Quick Navigation

- 📖 **[Project Structure](./docs/PROJECT_STRUCTURE.md)** - File organization and component breakdown
- 🏗️ **[Architecture](./docs/ARCHITECTURE.md)** - System design and technical details
- ✨ **[Features](./docs/FEATURES.md)** - Complete feature list and descriptions
- 🚀 **[Getting Started](./docs/GETTING_STARTED.md)** - Setup and installation guide
- 📡 **[API Documentation](./docs/API_DOCUMENTATION.md)** - API endpoints and usage

---

## 🎯 Overview

HackShield Portal is an **all-in-one hackathon platform** that brings together participants, organizations, and investors in one unified ecosystem. With cutting-edge features like a **Lockdown IDE**, **AI-powered team matching**, and **real-time collaboration**, it provides an unmatched hackathon experience.

### 👥 Three-User System

| User Type | Dashboard | Key Features |
|-----------|-----------|--------------|
| 🧑‍💻 **Participant** | Personal Hub | Browse hackathons, form/join teams, compete, earn achievements |
| 🏢 **Organization** | Management Panel | Create hackathons, monitor participation, judge submissions |
| 💼 **Contributor/Investor** | Marketplace View | Discover projects, invest in teams, connect with winners |

---

## ⚡ Core Features

### 🔐 Secure Lockdown IDE
- **Monaco Editor** - VS Code-like coding environment in browser
- **Real-time Collaboration** - Code together simultaneously with team members
- **Integrated Terminal** - Xterm.js for command execution
- **Live Preview** - Sandbox preview of web projects
- **AI Assistant** - Pair programming support

### 👥 Smart Team Matching
- **AI-Powered Algorithm** - Intelligent team suggestions based on skills & compatibility
- **Skill Matching** - Connect with complementary developers
- **Open Invite System** - Broadcast your skills to find teams
- **Team Formation Chat** - Real-time communication before competition starts

### 📊 Comprehensive Dashboards
- **Participant Dashboard** - Track hackathons, teams, XP, and achievements
- **Organization Dashboard** - Manage events, monitor participants, judge entries
- **Contributor Dashboard** - Browse projects, analyze investment opportunities

### 🔔 Unified Notification System
- **Email Notifications** - Important updates via email
- **In-App Notifications** - Real-time platform alerts
- **SMS Notifications** - Critical alerts via text
- **Custom Preferences** - User-controlled notification settings

### 🛒 Project Marketplace
- **Project Discovery** - Browse winning projects from past hackathons
- **Investment Opportunities** - Connect with successful teams
- **Direct Messaging** - Contact project owners
- **Rating & Reviews** - Community feedback system

### 🎖️ Gamification System
- **Experience Points (XP)** - Earn XP for participating and winning
- **Levels & Badges** - Unlock achievements and badges
- **Leaderboards** - Compete on global and team rankings
- **Reputation Score** - Build your hackathon profile

---

## 🛠️ Tech Stack

```
Frontend Layer:
├── Next.js 14              - React framework with App Router
├── TypeScript              - Type-safe JavaScript
├── Tailwind CSS            - Utility-first CSS framework
├── Framer Motion           - Smooth animations
├── React Hook Form         - Form state management
└── Zustand                 - Lightweight state management

Editor & Collaboration:
├── Monaco Editor           - Code editor (VS Code foundation)
├── Xterm.js                - Terminal emulator
├── Socket.io               - Real-time communication
└── WebRTC                  - P2P video/audio

Backend:
├── Next.js API Routes      - Serverless functions
├── MongoDB Atlas           - Cloud database
├── Mongoose ODM            - MongoDB object modeling
└── NextAuth.js             - Authentication framework

Security & Auth:
├── bcryptjs                - Password hashing
├── JWT                     - Token-based auth
└── NextAuth.js             - OAuth ready

UI & Utils:
├── Lucide React            - Icon library
├── React Hot Toast         - Toast notifications
├── Recharts                - Data visualization
├── date-fns                - Date utilities
└── Zod                     - Schema validation
```

---

## 📦 Installation & Setup

### Prerequisites
- **Node.js** 18 or higher
- **npm** or **yarn** package manager
- **MongoDB Atlas** account (create free at [mongodb.com](https://cloud.mongodb.com))
- **Git** for version control

### Quick Start

**1️⃣ Install Dependencies**
```bash
cd hackshield-portal
npm install
```

**2️⃣ Setup Environment Variables**
```bash
# Copy example to local config
cp .env.example .env.local

# Edit .env.local with your credentials:
MONGODB_URI=mongodb+srv://username:password@cluster.xxxxx.mongodb.net/hackshield
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=your-generated-secret-key
JWT_SECRET=your-jwt-secret
```

**3️⃣ Setup MongoDB**
1. Visit [MongoDB Atlas](https://cloud.mongodb.com)
2. Create a free M0 cluster
3. Create database user (e.g., `hackshield_user`)
4. Whitelist your IP (or use 0.0.0.0/0 for development)
5. Copy connection string and update `.env.local`

**4️⃣ Run Development Server**
```bash
npm run dev
```
🎉 Open [http://localhost:3000](http://localhost:3000)

---

## 📖 Available Scripts

```bash
# Development
npm run dev          # Start dev server with hot-reload

# Production
npm run build        # Build optimized production bundle
npm start            # Start production server

# Maintenance
npm run lint         # ESLint code quality check
npm run server       # Run custom Node server
```

---

## 🚀 Deployment

### Vercel (Recommended for Next.js)
1. Push code to GitHub
2. Connect Vercel to repository
3. Configure environment variables
4. Deploy with one click

### Other Platforms
- **Netlify** - Full Next.js support
- **Railway** - Simple deployment
- **Heroku** - Traditional hosting
- **AWS** - Enterprise option

---

## 🐛 Troubleshooting

| Issue | Solution |
|-------|----------|
| Port 3000 already in use | Use different port: `npm run dev -- -p 3001` |
| MongoDB connection failed | Check connection string and whitelist IP in Atlas |
| Build errors | Clear `.next`: `rm -rf .next && npm run build` |
| Dependencies issues | Reinstall: `rm -rf node_modules && npm install` |
| Blank page load | Check MongoDB connection, review console errors |

---

## 📚 Additional Resources

- [Next.js Documentation](https://nextjs.org/docs)
- [MongoDB Atlas Guide](https://docs.atlas.mongodb.com/)
- [NextAuth.js Docs](https://next-auth.js.org/)
- [Tailwind CSS Docs](https://tailwindcss.com/docs)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)

---

## 🤝 Contributing

We welcome contributions! Please:
- Report bugs via GitHub Issues
- Submit pull requests for improvements
- Suggest new features
- Improve documentation

---

## 📄 License

MIT License - open source and free to use

---

## 👤 Author & Support

**HackShield Team** - Building the future of hackathons 🚀

For issues or questions, check the documentation or create a GitHub issue.

---

**Last Updated:** March 2026  
**Version:** 1.0.0  
**Status:** ✅ Production Ready
