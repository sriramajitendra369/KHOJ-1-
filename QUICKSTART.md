# TechMatch - 5 Minute Quick Start

## ⚡ The Fastest Way to Get Running Locally

### Prerequisites (1 minute)
```bash
# Make sure you have:
node --version  # Should be 16+
npm --version
```

### Backend Setup (2 minutes)

```bash
# 1. Go to backend directory
cd backend

# 2. Install dependencies
npm install

# 3. Create .env file with minimal setup
cat > .env << EOF
PORT=5000
JWT_SECRET=test-secret-change-in-production
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_KEY=your-anon-key
NODE_ENV=development
EOF

# 4. Start backend server
npm run dev

# Backend will start on http://localhost:5000
```

**Keep this terminal open!**

### Frontend Setup (2 minutes)

Open **NEW terminal** (don't close backend):

```bash
# 1. Go to frontend directory
cd frontend

# 2. Install dependencies
npm install

# 3. Start frontend dev server
npm run dev

# Frontend will start on http://localhost:3000
```

### You're Done! 🎉

**Access the platform:**
- Frontend: http://localhost:3000
- Backend API: http://localhost:5000/api

## 🔓 Test Login Credentials

```
Hiring Manager:
Email: john@example.com
Password: password

Technician:
Email: sarah@example.com
Password: password
```

## 🧪 Quick Test Workflow

1. **Login as hiring manager**
   - Click "Login" → Enter john@example.com / password

2. **Create a job**
   - Click "Post a Job"
   - Fill form: "Build Website", select skills, set budget
   - Complete 3-step form

3. **View matches**
   - Click "View Matches"
   - See technician recommendations with scores
   - Scores are calculated in real-time

4. **Login as technician**
   - Logout (top right)
   - Login as sarah@example.com / password
   - Update your profile with skills

5. **Send invitation**
   - Login back as hiring manager
   - Go to job matches
   - Click "Send Invitation" on a technician

## 🚨 Common Issues & Fixes

### "Cannot connect to database"
**Problem:** Backend can't reach Supabase

**Solution:**
1. Copy your actual Supabase credentials
2. Update .env file with real SUPABASE_URL and SUPABASE_KEY
3. Restart backend: `npm run dev`

### "Frontend shows blank page"
**Problem:** Frontend can't reach backend API

**Solution:**
1. Make sure backend is running: `npm run dev` in backend folder
2. Check backend is on port 5000: http://localhost:5000/api/jobs should show error (that's ok)
3. Restart frontend: `npm run dev`

### "Port already in use"
**Problem:** Port 3000 or 5000 already in use

**Solution:**
```bash
# Change port in backend:
# Edit backend/src/server.js, change PORT to 5001

# Change port in frontend:
# Edit frontend/vite.config.js, change port to 3001
```

### "npm install fails"
**Problem:** Dependency issues

**Solution:**
```bash
# Clear npm cache
npm cache clean --force

# Try again
npm install
```

## 📁 File Structure You Just Created

```
technician-platform/
├── backend/           # Node.js + Express API
│   ├── src/
│   │   ├── server.js              (All API routes)
│   │   ├── matching-engine.js     (Smart algorithm)
│   │   ├── profile-scraper.js     (12 data sources)
│   ├── database-schema.sql        (PostgreSQL schema)
│   ├── .env.example
│   └── package.json
│
├── frontend/          # React + Vite + Tailwind
│   ├── src/
│   │   ├── pages/                 (All UI pages)
│   │   ├── App.jsx                (Routing)
│   │   ├── api.js                 (HTTP client)
│   │   └── styles/global.css
│   ├── index.html
│   ├── vite.config.js
│   └── package.json
│
├── README.md          (Full documentation)
├── DEPLOYMENT.md      (Production guide)
├── PROJECT_SUMMARY.md (Architecture)
└── QUICKSTART.md      (This file)
```

## 🔑 Key Features You Can Test

✅ **User Registration & Login**
- JWT authentication
- Password hashing
- Role-based access

✅ **Job Posting**
- 3-step form
- Skill selection
- Budget setting

✅ **Smart Matching**
- Weighted algorithm
- Real-time scoring
- Detailed explanations

✅ **Technician Profiles**
- Skill management
- Certification tracking
- Availability setting

✅ **Job Invitations**
- Send offers
- Track responses
- Manage status

✅ **Admin Panel**
- System statistics
- Profile scraper (12 sources)
- Algorithm configuration

## 📊 Test Data Included

The seed database comes with:
- 10 technician profiles (different skills, experience)
- 1 sample job
- 2 reviews
- Ready to use immediately!

## 🎯 Next Steps

### To Deploy to Production:
1. Read **DEPLOYMENT.md**
2. Create Supabase account (free)
3. Create Vercel account (free)
4. Follow deployment steps (15 mins)

### To Customize:
1. Edit job categories in `frontend/src/pages/JobCreationForm.jsx`
2. Adjust matching weights in `backend/src/matching-engine.js`
3. Add more test data in `backend/database-schema.sql`
4. Customize colors in `frontend/tailwind.config.js`

### To Understand the Code:
1. Start with `backend/src/matching-engine.js` (algorithm)
2. Then `frontend/src/pages/JobMatches.jsx` (UI)
3. Then `backend/src/server.js` (API endpoints)

## 💡 Pro Tips

**Faster Development:**
- Keep both servers running (2 terminals)
- Frontend hot-reloads on every save
- Backend auto-restarts on file changes

**Testing Faster:**
- Use demo credentials (see above)
- Seed database has sample data ready
- No need to create test technicians

**Debugging:**
- Check browser console (F12) for frontend errors
- Check terminal for backend errors
- Network tab shows API requests

## 📞 Got Stuck?

1. **Check logs:**
   - Frontend: Browser DevTools (F12)
   - Backend: Terminal where npm run dev is running

2. **Read documentation:**
   - README.md for overview
   - PROJECT_SUMMARY.md for architecture
   - Code comments explain complex logic

3. **Common fixes:**
   - Restart backend: Ctrl+C then `npm run dev`
   - Restart frontend: Ctrl+C then `npm run dev`
   - Clear browser cache: Cmd/Ctrl + Shift + Delete

## 🎓 To Learn the Architecture

**Backend Execution Path:**
```
POST /jobs → server.js 
           → Validation 
           → Supabase insert 
           → Return job ID

POST /jobs/:id/match → Fetch all technicians
                    → Run matching-engine.js
                    → Calculate weighted scores
                    → Save results
                    → Return sorted matches
```

**Frontend Execution Path:**
```
User fills job form → Validation → api.js (axios)
                  → Backend stores job
                  → Redirect to /job/:id/matches
                  → api.js fetches matches
                  → Display cards with scores
                  → User clicks "Send Invitation"
                  → POST invitation endpoint
```

## ✨ What Makes This Special

- ✅ **Real matching algorithm** (not fake AI)
- ✅ **12 platform scraper** (LinkedIn, GitHub, Stack Overflow, etc)
- ✅ **Profile from multiple sources** (automated talent acquisition)
- ✅ **Smart scoring system** (transparent, configurable)
- ✅ **Production-ready code** (ready to deploy in 15 minutes)
- ✅ **Seed data included** (test immediately)
- ✅ **Full documentation** (README + Deployment guide)

---

**Now go build something amazing! 🚀**

Any issues? Check README.md or look at console logs.
