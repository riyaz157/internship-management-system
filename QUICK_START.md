# Quick Start Guide

## Project Overview

**Internship Management System** - A full-stack platform for managing remote internships with task tracking, student progress monitoring, and mentor feedback.

**Repository**: https://github.com/riyaz157/internship-management-system

## What's Been Created

✅ **Complete Project Structure**
- Frontend folder with React setup
- Backend folder with Node.js/Express setup
- Comprehensive README.md with full documentation
- DEPLOYMENT.md with step-by-step deployment instructions
- .env.example with all required environment variables
- Proper .gitignore configuration

## Files Included

```
internship-management-system/
├── backend/
│   └── package.json (Express, Mongoose, JWT, CORS)
├── frontend/
│   └── package.json (React, React Router, Axios, Tailwind)
├── README.md (Full documentation)
├── DEPLOYMENT.md (Vercel & Render guide)
├── .env.example (Environment template)
├── .gitignore (Node.js & React ignores)
└── QUICK_START.md (This file)
```

## Local Development Setup

### Backend Setup

```bash
cd backend
npm install

# Create .env file
cp ../.env.example .env
# Edit .env with your MongoDB URI and JWT secret

# Start development server
npm run dev
# Backend runs on http://localhost:5000
```

### Frontend Setup

```bash
cd frontend
npm install

# Create .env file
echo "REACT_APP_API_URL=http://localhost:5000" > .env

# Start development server
npm start
# Frontend runs on http://localhost:3000
```

## Production Deployment

### Frontend (Vercel)

1. Push code to GitHub
2. Go to https://vercel.com
3. Import repository
4. Set root directory to `frontend`
5. Add environment variables
6. Deploy

### Backend (Render)

1. Create MongoDB cluster on https://mongodb.com/cloud/atlas
2. Go to https://render.com
3. Create web service
4. Set root directory to `backend`
5. Add environment variables
6. Deploy

**See DEPLOYMENT.md for detailed instructions**

## Database Schema

### Collections
- **Users**: Student, Admin, Mentor profiles
- **Internships**: Job postings with requirements
- **Applications**: Student applications to internships
- **Tasks**: Work assignments for interns
- **Feedback**: Performance ratings and comments

## API Endpoints

### Authentication
- `POST /api/auth/register`
- `POST /api/auth/login`
- `GET /api/auth/profile`

### Internships
- `GET /api/internships`
- `POST /api/internships` (Admin)
- `GET /api/internships/:id`
- `PUT /api/internships/:id` (Admin)

### Applications
- `POST /api/applications`
- `GET /api/applications/:internshipId` (Admin)
- `PUT /api/applications/:id/status` (Admin)

### Tasks
- `GET /api/tasks/:internshipId`
- `POST /api/tasks` (Mentor)
- `PUT /api/tasks/:id/progress` (Student)

### Feedback
- `POST /api/feedback` (Mentor)
- `GET /api/feedback/intern/:userId`
- `GET /api/feedback/evaluation/:internshipId`

## Tech Stack

**Frontend**
- React 18+
- React Router v6
- Tailwind CSS
- Axios

**Backend**
- Node.js
- Express.js
- MongoDB & Mongoose
- JWT Authentication
- CORS enabled

## Next Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/riyaz157/internship-management-system.git
   cd internship-management-system
   ```

2. **Install dependencies**
   ```bash
   cd backend && npm install
   cd ../frontend && npm install
   ```

3. **Set up environment variables**
   - Create `.env` files in both backend and frontend
   - Copy from `.env.example` and fill in values

4. **Start development servers**
   - Terminal 1: `cd backend && npm run dev`
   - Terminal 2: `cd frontend && npm start`

5. **Deploy when ready**
   - Follow DEPLOYMENT.md for Vercel and Render

## Key Features

✨ **Admin Dashboard**
- Post and manage internships
- Review student applications
- Track intern progress
- Generate performance reports

✨ **Student Portal**
- Browse internship opportunities
- Submit applications
- Track assigned tasks
- View feedback from mentors

✨ **Task Management**
- Create and assign tasks
- Update progress status
- Upload task submissions
- Leave comments

✨ **Evaluation System**
- Rating system (1-5 stars)
- Written feedback
- Performance metrics
- Certificate generation

## Troubleshooting

**Port already in use?**
```bash
# Change port in backend .env
PORT=5001

# Or kill process on port 5000
lsof -ti :5000 | xargs kill -9
```

**MongoDB connection error?**
- Check MongoDB URI is correct
- Ensure IP whitelist includes your IP
- Verify database user credentials

**Frontend not connecting to backend?**
- Check REACT_APP_API_URL environment variable
- Ensure backend is running
- Check CORS settings in backend

## Support & Documentation

- **README.md**: Full project documentation
- **DEPLOYMENT.md**: Production deployment guide
- **GitHub Issues**: Report bugs or request features

## Author

riyaz157 - Computer Science Student, KLU

---

**Last Updated**: 2025-11-30
**Status**: ✅ Ready for Development & Deployment
