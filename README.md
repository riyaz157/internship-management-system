# Internship Management System

A comprehensive full-stack platform for managing remote internships with real-time task tracking, student progress monitoring, and mentor feedback. Built following the evalsystem architecture pattern.

## Features

### Admin Dashboard (Employers)
- Create and manage internship opportunities
- Post internship details (title, description, skills, duration, stipend, deadline)
- Review and manage student applications
- Track intern progress and task completion
- Generate performance reports
- Send notifications and feedback

### Student Dashboard
- Browse available internship opportunities
- Submit applications with resume and statement
- Track assigned tasks and deadlines
- Update task progress (todo/in-progress/done)
- View mentor feedback and ratings
- Download certificates and evaluations
- Log weekly activity reports

### Task Management
- Create tasks with descriptions and due dates
- Real-time progress tracking
- File/link uploads for task submissions
- Comments and clarifications per task
- Status: Todo, In Progress, Completed

### Feedback & Evaluation
- Mentor ratings (communication, quality, punctuality)
- Written feedback per task
- Overall internship evaluation
- Performance metrics dashboard
- Certificate generation

## Tech Stack

### Frontend
- **Framework:** React 18+ with React Router
- **Styling:** Tailwind CSS
- **State Management:** Context API + Redux (optional)
- **HTTP Client:** Axios
- **Deployment:** Vercel

### Backend
- **Runtime:** Node.js with Express.js
- **Database:** MongoDB + Mongoose
- **Authentication:** JWT (JSON Web Tokens)
- **Validation:** Joi/Yup
- **Deployment:** Render

## Project Structure

```
internship-management-system/
├── frontend/                    # React application
│   ├── src/
│   │   ├── components/        # Reusable UI components
│   │   ├── pages/             # Page components
│   │   ├─┐ ├── AdminDashboard/
│   │   ├─┐ ├── StudentDashboard/
│   │   ├┐ ├── InternshipDetails/
│   │   ├┐ ├── Tasks/
│   │   ├┐ ├── Feedback/
│   │   ├┐ ├── Auth/
│   │   ├── hooks/             # Custom React hooks
│   │   ├── context/           # Context API setup
│   │   ├── services/         # API services
│   │   ├── utils/            # Utility functions
│   │   ├── styles/           # Global styles
│   │   ├── App.js
│   │   ├── index.js
│   ├── public/
│   ├── package.json
│   ├── .env
│   ├── .gitignore
│   ├─┐ tailwind.config.js
│
├── backend/                    # Express.js application
│   ├── src/
│   │   ├── models/           # MongoDB schemas
│   │   │   ├── User.js
│   │   │   ├── Internship.js
│   │   │   ├── Application.js
│   │   │   ├── Task.js
│   │   │   ├─┐ Feedback.js
│   │   ├── routes/           # API endpoints
│   │   │   ├── auth.js
│   │   │   ├── internships.js
│   │   │   ├── applications.js
│   │   │   ├── tasks.js
│   │   │   ├─┐ feedback.js
│   │   ├── controllers/      # Business logic
│   │   ├── middleware/       # Custom middleware
│   │   │   ├── auth.js
│   │   │   ├─┐ error.js
│   │   ├── utils/            # Utility functions
│   │   ├── config/           # Configuration
│   │   ├── app.js
│   │   ├─┐ server.js
│   ├── .env
│   ├── .gitignore
│   ├── package.json
│   ├─┐ README.md
│
├── .github/                   # GitHub workflows
├── .gitignore
├── README.md
├─┐ package.json               # Root package.json for workspace
```

## Installation

### Prerequisites
- Node.js (v14+)
- MongoDB (local or Atlas)
- npm or yarn

### Clone and Setup

```bash
# Clone repository
git clone https://github.com/riyaz157/internship-management-system.git
cd internship-management-system

# Setup Backend
cd backend
npm install

# Setup Frontend
cd ../frontend
npm install
```

### Environment Variables

**Backend (.env)**
```
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_secret_key
JWT_EXPIRE=7d
NODE_ENV=development
PORT=5000
```

**Frontend (.env)**
```
REACT_APP_API_URL=http://localhost:5000
```

### Run Development Servers

```bash
# Terminal 1 - Backend
cd backend
npm start

# Terminal 2 - Frontend
cd frontend
npm start
```

## API Endpoints

### Authentication
- `POST /api/auth/register` - Register user
- `POST /api/auth/login` - User login
- `POST /api/auth/logout` - User logout
- `GET /api/auth/profile` - Get user profile

### Internships
- `GET /api/internships` - List all internships
- `POST /api/internships` - Create internship (admin)
- `GET /api/internships/:id` - Get internship details
- `PUT /api/internships/:id` - Update internship (admin)
- `DELETE /api/internships/:id` - Delete internship (admin)

### Applications
- `POST /api/applications` - Submit application
- `GET /api/applications/:internshipId` - List applications (admin)
- `PUT /api/applications/:id/status` - Update application status
- `GET /api/applications/student/:userId` - Get student applications

### Tasks
- `POST /api/tasks` - Create task (mentor)
- `GET /api/tasks/:internshipId` - List tasks
- `PUT /api/tasks/:id` - Update task
- `PUT /api/tasks/:id/progress` - Update task progress
- `POST /api/tasks/:id/upload` - Upload task submission

### Feedback
- `POST /api/feedback` - Submit feedback
- `GET /api/feedback/:taskId` - Get feedback for task
- `GET /api/feedback/intern/:userId` - Get all feedback for intern
- `GET /api/feedback/evaluation/:internshipId` - Get final evaluation

## Database Schema

### User Model
```javascript
{
  name, email, password, phone, 
  role: ['student', 'admin', 'mentor'],
  profilePicture, resume, bio,
  skills: [], experience: [],
  createdAt, updatedAt
}
```

### Internship Model
```javascript
{
  title, description, company,
  skills: [], duration, stipend,
  startDate, endDate, deadline,
  maxInterns, createdBy: adminId,
  status: ['open', 'closed'],
  applications: [{ ref: Application }],
  mentors: [{ ref: User }],
  createdAt, updatedAt
}
```

### Application Model
```javascript
{
  internshipId: ref, studentId: ref,
  resumeLink, statement, coverLetter,
  status: ['pending', 'selected', 'rejected'],
  appliedAt, updatedAt,
  feedback: String
}
```

### Task Model
```javascript
{
  internshipId: ref, assignedTo: ref,
  title, description, dueDate,
  status: ['todo', 'in-progress', 'completed'],
  priority: ['low', 'medium', 'high'],
  submissions: [{ file, link, submittedAt }],
  createdAt, updatedAt
}
```

### Feedback Model
```javascript
{
  taskId: ref, internId: ref, mentorId: ref,
  ratings: { communication, quality, punctuality },
  comment, overallScore,
  isFinal: Boolean,
  createdAt, updatedAt
}
```

## Deployment

### Deploy Frontend (Vercel)
```bash
cd frontend
npm run build
# Connect to Vercel via CLI or GitHub integration
```

### Deploy Backend (Render)
1. Push code to GitHub
2. Connect repository to Render
3. Set environment variables
4. Deploy

## Contributing

This is an academic project. Feel free to fork and submit pull requests.

## License

MIT License

## Author

**riyaz157** - Computer Science Student, KLU

## Contact

For questions or collaboration, reach out via GitHub.
