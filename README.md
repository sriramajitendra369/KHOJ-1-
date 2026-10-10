# TechMatch - Smart Technician Recommendation Platform

A full-stack web application that connects hiring managers with qualified technicians using AI-powered matching algorithm.

## 🎯 Features

- **Smart Matching Algorithm**: Weighted scoring system that considers skills, experience, location, availability, and price
- **Technician Profiles**: Detailed profiles with skills, certifications, experience, and ratings
- **Job Posting**: Create and manage job requirements with mandatory and preferred criteria
- **Profile Scraper**: Import technician profiles from 12+ platforms (LinkedIn, GitHub, Upwork, etc.)
- **Role-Based Access**: Separate dashboards for hiring managers, technicians, and admins
- **Invitations & Notifications**: Send job invitations and manage responses
- **AI Screening**: Optional AI-powered interview screening
- **Reviews & Ratings**: Track technician performance with verified reviews

## 📋 Supported Platforms for Profile Scraping

1. GitHub
2. Stack Overflow
3. Upwork
4. Fiverr
5. Behance
6. Dribbble
7. Freelancer.com
8. Toptal
9. Guru
10. Clutch.co
11. LinkedIn
12. AngelList

## 🏗️ Architecture

```
technician-platform/
├── frontend/              # React + Vite + Tailwind
│   ├── src/
│   │   ├── pages/        # All React pages
│   │   ├── api.js        # API client
│   │   ├── App.jsx       # Main app with routing
│   │   └── styles/
│   ├── index.html
│   ├── vite.config.js
│   ├── tailwind.config.js
│   └── package.json
│
├── backend/              # Node.js + Express
│   ├── src/
│   │   ├── server.js     # Main server & routes
│   │   ├── matching-engine.js
│   │   ├── profile-scraper.js
│   │   └── ...
│   ├── database-schema.sql
│   ├── .env.example
│   └── package.json
│
├── README.md
└── DEPLOYMENT.md
```

## 🚀 Quick Start

### Prerequisites
- Node.js 16+
- PostgreSQL 12+ (or Supabase account)
- npm or yarn

### 1. Backend Setup

```bash
cd backend
npm install
```

Create `.env` file:
```bash
cp .env.example .env
# Edit .env with your Supabase credentials
```

Start backend:
```bash
npm run dev
```

The backend will run on `http://localhost:5000`

### 2. Database Setup

Option A: Using Supabase (Recommended)
```bash
# Execute database-schema.sql in Supabase SQL editor
# Your database will be set up in seconds
```

Option B: Using PostgreSQL locally
```bash
psql -U postgres -f backend/database-schema.sql
```

### 3. Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

The frontend will run on `http://localhost:3000`

## 📝 Sample Credentials (Demo Data)

**Hiring Manager:**
- Email: john@example.com
- Password: password

**Technician:**
- Email: sarah@example.com
- Password: password

## 🎯 Matching Algorithm

The system uses a configurable weighted matching algorithm:

1. **Skill Match** (30%): How well technician skills match job requirements
2. **Availability** (20%): Whether technician is available for the timeline
3. **Location** (15%): Distance and travel requirements
4. **Price** (15%): Budget alignment
5. **Experience** (10%): Years of relevant experience
6. **Certifications** (5%): Required certifications
7. **Reviews** (5%): Historical performance and ratings

### Mandatory Requirements Filter
Before calculating scores, the system checks:
- Required skills presence and proficiency level
- Mandatory certifications
- Budget constraints
- Availability within deadline
- Technician willingness

**Only technicians passing ALL mandatory filters are shown as eligible.**

## 🔐 Security Features

- JWT-based authentication
- Password hashing with bcryptjs
- Role-based access control (RBAC)
- Server-side validation
- Secure file uploads to Supabase Storage
- Protected admin endpoints

## 📊 Admin Features

- User and technician verification
- Matching algorithm weight configuration
- Platform-wide statistics and analytics
- Profile scraper for importing talent
- User moderation and management

## 🛠️ API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user

### Jobs
- `POST /api/jobs` - Create new job
- `GET /api/jobs` - Get user's jobs
- `GET /api/jobs/:jobId` - Get job details
- `POST /api/jobs/:jobId/match` - Run matching algorithm
- `GET /api/jobs/:jobId/matches` - Get job matches

### Technician Profiles
- `POST /api/technician/profile` - Create/update profile
- `GET /api/technician/profile` - Get own profile
- `GET /api/technician/profile/:userId` - Get technician profile

### Invitations
- `POST /api/invitations` - Send job invitation
- `GET /api/invitations` - Get invitations
- `POST /api/invitations/:invitationId/respond` - Accept/decline

### Dashboards
- `GET /api/dashboard/hiring` - Hiring dashboard stats
- `GET /api/dashboard/technician` - Technician dashboard stats
- `GET /api/dashboard/admin` - Admin dashboard stats

### Profile Scraping
- `POST /api/scrape-profiles` - Scrape profiles from platforms

## 📱 Pages & Routes

### Public Pages
- `/` - Landing page
- `/login` - Login
- `/register` - Registration

### Hiring Manager Routes
- `/dashboard` - Main dashboard
- `/create-job` - Post new job
- `/job/:jobId/matches` - View technician matches

### Technician Routes
- `/tech-dashboard` - Dashboard
- `/profile` - Edit profile
- `/technician/:userId` - View technician profile (public)

### Admin Routes
- `/admin` - Admin dashboard

## 🧪 Testing

### Test Job Matching
1. Login as hiring manager
2. Create a job with specific skills
3. View matches and verify scores are calculated
4. Check that mandatory requirements are enforced

### Test Scraper
1. Login as admin
2. Go to Admin Dashboard
3. Enter search query (e.g., "JavaScript developer")
4. Check scraped profiles from all 12 platforms

## 📦 Deployment

### Deploy to Vercel (Frontend)

```bash
cd frontend
npm run build
# Connect to Vercel and deploy
```

### Deploy to Supabase (Backend)

Option 1: Use Supabase Edge Functions
```bash
# Deploy server.js as an Edge Function
```

Option 2: Deploy to Heroku/Railway (Alternative)
```bash
git push heroku main
```

### Environment Variables for Production

Backend:
```
JWT_SECRET=<long-random-string>
SUPABASE_URL=<your-supabase-url>
SUPABASE_KEY=<your-supabase-key>
NODE_ENV=production
```

Frontend:
```
REACT_APP_API_URL=https://your-backend-domain.com/api
```

## 🐛 Troubleshooting

**Backend not connecting to database:**
- Check `SUPABASE_URL` and `SUPABASE_KEY` in `.env`
- Verify database schema is created
- Check PostgreSQL connection

**Frontend shows "Cannot GET /api/...":**
- Make sure backend is running on port 5000
- Check that proxy is configured in Vite

**Matching algorithm returns 0 results:**
- Verify job requirements aren't too restrictive
- Check that technician skills match job requirements
- Look at console logs for filtering details

## 📚 Documentation

- **Matching Algorithm**: See `backend/src/matching-engine.js` for detailed scoring logic
- **API Specs**: See API endpoints section above
- **Database Schema**: See `backend/database-schema.sql`

## 🎨 UI/UX Design

- **Modern & Clean**: White/light backgrounds with blue accents
- **Responsive**: Mobile-first design, works on all devices
- **Professional**: Suitable for hackathon demo and production use
- **Accessible**: WCAG compliant color contrast and semantic HTML

## 📄 Project Checklist

- ✅ Hiring manager can register and post jobs
- ✅ Technicians can create detailed profiles
- ✅ Smart matching algorithm with multiple criteria
- ✅ Score-based ranking with explanations
- ✅ Mandatory requirements enforcement
- ✅ File uploads for portfolios/certificates
- ✅ AI screening module
- ✅ Profile scraping from 12+ platforms
- ✅ Role-based dashboards
- ✅ Notification system
- ✅ Reviews and ratings
- ✅ Admin panel
- ✅ JWT authentication
- ✅ Database schema with seed data
- ✅ Responsive design
- ✅ Production-ready deployment

## 🤝 Contributing

This is a hackathon project. For issues or improvements, please create an issue or pull request.

## 📄 License

MIT License - feel free to use this project for any purpose

## 🙋 Support

For questions or issues:
1. Check the troubleshooting section
2. Review the API documentation
3. Check console logs for errors
4. Reach out to the development team

---

**Built with ❤️ for matching talented technicians with great opportunities**
