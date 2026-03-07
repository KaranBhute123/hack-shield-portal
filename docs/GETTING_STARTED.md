# 📖 Getting Started with HackShield Portal

A step-by-step guide to set up and run HackShield Portal on your local machine.

---

## 🎯 Before You Start

Ensure you have:**
- **Node.js 18+** installed ([Download](https://nodejs.org/))
- **Git** for version control ([Download](https://git-scm.com/))
- **npm** (comes with Node.js)
- **MongoDB Atlas** account (free at [mongodb.com](https://cloud.mongodb.com))

Check versions:
```bash
node --version    # Should be v18.0.0 or higher
npm --version     # Should be 9.0.0 or higher
```

---

## 🚀 Step 1: Installation

### Clone the Repository
```bash
git clone https://github.com/yourusername/hackshield-portal.git
cd hackshield-portal
```

### Install Dependencies
```bash
npm install
```

This will install all packages listed in `package.json`. Wait for completion (may take a few minutes).

#### Troubleshooting Install Issues
- **Slow installation?** Try: `npm install --legacy-peer-deps`
- **Permission denied?** Try: `sudo npm install` (macOS/Linux)
- **Port conflicts?** Check no other Node processes are running

---

## 🗄️ Step 2: Database Setup (MongoDB Atlas)

### Create a MongoDB Cluster

1. **Sign up/Login** at [MongoDB Atlas](https://cloud.mongodb.com)
2. **Create Organization** (or use existing)
3. **Create Project** (e.g., "HackShield")
4. **Create Cluster:**
   - Click "Create" → Choose "Free M0 Shared Cluster"
   - Select region closest to you
   - Click "Create Cluster" (wait 5-10 minutes)

### Create Database User

1. In Atlas Dashboard → **Database Access** → **Add New Database User**
2. Set credentials:
   - **Username:** `hackshield_user`
   - **Password:** Generate strong password (e.g., 16+ characters)
   - **Save the password!** ⚠️

3. **Database User Privileges:**
   - Select "Built-in Role"
   - Choose "Read and write to any database"
   - Click "Add User"

### Whitelist IP Address

1. Go to **Network Access** → **Add IP Address**
2. For **development:** Click "Allow Access from Anywhere" (0.0.0.0/0)
3. For **production:** Whitelist specific IP only
4. Click "Confirm"

### Get Connection String

1. Click "Databases" → Your cluster → "Connect"
2. Select "Drivers"
3. Choose "Node.js" version 3.0 or later
4. Copy the connection string:
   ```
   mongodb+srv://username:password@cluster.mongodb.net/hackshield?retryWrites=true&w=majority
   ```

---

## 🔑 Step 3: Environment Variables

### Create .env.local File

In project root, create `.env.local` file:

```bash
# Windows PowerShell
New-Item -Path ".env.local" -ItemType File

# Or copy from example
cp .env.example .env.local
```

### Fill in Environment Variables

Edit `.env.local` and add:

```env
# MongoDB Connection String
MONGODB_URI=mongodb+srv://hackshield_user:your_password@cluster0.xxxxx.mongodb.net/hackshield?retryWrites=true&w=majority

# NextAuth Configuration
NEXTAUTH_URL=http://localhost:3000
NEXTAUTH_SECRET=generate-random-key-here-min-32-chars

# JWT Secret (can be similar to NEXTAUTH_SECRET)
JWT_SECRET=your-jwt-secret-key-min-32-chars

# Optional - Uncomment when implementing OAuth
# GOOGLE_CLIENT_ID=your-google-client-id
# GOOGLE_CLIENT_SECRET=your-google-client-secret
# GITHUB_CLIENT_ID=your-github-id
# GITHUB_CLIENT_SECRET=your-github-secret
```

### Generate Secure Secrets

Generate random secrets (pick one method):

**Option A: Using OpenSSL**
```bash
openssl rand -base64 32
```

**Option B: Using Node.js**
```bash
node -e "console.log(require('crypto').randomBytes(32).toString('hex'))"
```

**Option C: Online Generator**
Visit [Lastpass Generator](https://www.lastpass.com/features/password-generator)

---

## ▶️ Step 4: Running the Application

### Start Development Server

```bash
npm run dev
```

You should see:
```
> hackshield-portal@1.0.0 dev
> next dev

- ready started server on 0.0.0.0:3000, url: http://localhost:3000
```

### Open Application

1. Open browser → **http://localhost:3000**
2. You should see HackShield Portal homepage
3. Click "Register" to create your first account

### Verify Everything Works

1. **Register new account**
   - Email: `test@example.com`
   - Password: Any password
   - Name: Your name

2. **Check MongoDB**
   - Go to MongoDB Atlas dashboard
   - Select database → Collections
   - You should see "users" collection created

3. **Check logs**
   - Terminal should show API requests
   - No red error messages

---

## 🧪 Testing the Application

### Test User Registration Flow
```
1. Navigate: http://localhost:3000/auth/register
2. Fill form with test data
3. Click "Register"
4. Should redirect to login
```

### Test User Login
```
1. Navigate: http://localhost:3000/auth/login
2. Enter credentials from registration
3. Click "Login"
4. Should redirect to dashboard
```

### Test Dashboard Access
```
1. After login, navigate: http://localhost:3000/dashboard
2. Should display dashboard without errors
3. Check browser console (F12) for errors
```

### Test API Endpoints
```bash
# In new terminal, test API
curl http://localhost:3000/api/user

# Should return user data (requires login token)
```

---

## 🛠️ Development Tips

### Hot Reload
- Edit any file in `app/` or `components/`
- Browser automatically refreshes (magic!)

### Debug Mode
Press `F12` in browser to open DevTools:
- **Console** - See JavaScript errors
- **Network** - Monitor API calls
- **Application** - View cookies and storage

### Common Issues & Solutions

#### MongoDB Connection Failed
```
Error: MongoServerError: authentication failed
```
**Solution:** Check username/password in MONGODB_URI

#### Port Already in Use
```
Error: listen EADDRINUSE: address already in use :::3000
```
**Solution:** Kill process or use different port:
```bash
npm run dev -- -p 3001
```

#### Build Errors
```
Error: Failed to load SWC binary
```
**Solution:** Clear cache and reinstall:
```bash
rm -rf .next node_modules
npm install
npm run dev
```

#### NEXTAUTH_SECRET Not Set
```
Error: NEXTAUTH_SECRET not set
```
**Solution:** Add strong secret to `.env.local`

---

## 📁 File Structure After Setup

```
hackshield-portal/
├── .env.local              ✅ Environment variables (you created)
├── node_modules/           ✅ Dependencies installed
├── .next/                  ✅ Build cache (auto-generated)
├── app/                    ✅ Application code
├── components/             ✅ React components
├── models/                 ✅ Database schemas
├── public/                 ✅ Static assets
├── docs/                   ✅ Documentation
├── README.md               ✅ This project
├── package.json            ✅ Dependencies list
└── tsconfig.json           ✅ TypeScript config
```

---

## 🔒 Security Best Practices

### Development Only
- ✅ Using `0.0.0.0/0` for MongoDB IP whitelist
- ✅ Storing secrets in `.env.local` (not committed)
- ✅ Using `http://localhost:3000`

### Before Production
- ❌ Change NEXTAUTH_SECRET to new, stronger secret
- ❌ Whitelist only your actual IPs in MongoDB
- ❌ Use HTTPS with domain name
- ❌ Review and harden all environment variables
- ❌ Enable Database Access audit logging
- ❌ Set up automated backups

---

## 🚀 Next Steps

After successful setup:

1. **Explore Codebase**
   - Check `app/` structure
   - Read component implementations
   - Understand API routes

2. **Learn Architecture**
   - Read [ARCHITECTURE.md](./ARCHITECTURE.md)
   - Understand flow of data
   - Study authentication system

3. **Customize Features**
   - Modify dashboard layouts
   - Add new pages
   - Extend API endpoints

4. **Deploy Application**
   - Choose hosting (Vercel recommended)
   - Configure environment variables
   - Deploy to production

---

## 📚 Additional Commands

```bash
# Build for production
npm run build

# Run production server
npm start

# Lint code quality
npm run lint

# Run TypeScript compiler check
npx tsc --noEmit

# Clean build artifacts
rm -rf .next

# View installed packages
npm list

# Update packages
npm update
```

---

## 🆘 Getting Help

### Check These First
- ✅ Is Node.js installed? (`node --version`)
- ✅ Is MongoDB connected? (check `.env.local`)
- ✅ Are all npm packages installed? (`npm install`)
- ✅ Check port 3000 not in use

### Debug Resources
- **Browser Console** - Press F12 → Console tab
- **Terminal Output** - Check error messages in `npm run dev`
- **MongoDB Atlas** - Check cluster status and collections
- **Documentation** - Read relevant `.md` files

### Still Stuck?
1. Check [API_DOCUMENTATION.md](./API_DOCUMENTATION.md)
2. Review error messages carefully
3. Search GitHub issues
4. Create new issue with error details

---

## ✅ Setup Checklist

- [ ] Node.js 18+ installed
- [ ] Repository cloned
- [ ] Dependencies installed (`npm install`)
- [ ] MongoDB Atlas cluster created
- [ ] Database user created
- [ ] IP whitelist configured
- [ ] Connection string obtained
- [ ] `.env.local` file created
- [ ] All environment variables filled
- [ ] Development server runs (`npm run dev`)
- [ ] Can access http://localhost:3000
- [ ] Can register and login
- [ ] MongoDB shows data being stored

---

**Ready to build the next great hackathon platform? Let's go! 🚀**
