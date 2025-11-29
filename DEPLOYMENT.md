# Deployment Guide

Complete step-by-step guide to deploy the Internship Management System to Vercel (Frontend) and Render (Backend).

## Frontend Deployment (Vercel)

### Prerequisites
- GitHub account with repository
- Vercel account (free tier available)

### Steps

1. **Push Code to GitHub**
   ```bash
   git add .
   git commit -m "Ready for production deployment"
   git push origin main
   ```

2. **Connect to Vercel**
   - Go to [vercel.com](https://vercel.com)
   - Click "Import Project"
   - Select "Import Git Repository"
   - Choose "GitHub" and authenticate
   - Select `internship-management-system` repository

3. **Configure Vercel Project**
   - **Root Directory**: Select `frontend`
   - **Framework Preset**: React
   - **Build Command**: `npm run build`
   - **Output Directory**: `build`

4. **Add Environment Variables**
   - In Vercel dashboard, go to Settings → Environment Variables
   - Add:
     ```
     REACT_APP_API_URL=https://your-backend-url.onrender.com
     REACT_APP_ENVIRONMENT=production
     ```

5. **Deploy**
   - Click "Deploy"
   - Wait for deployment to complete
   - Your frontend URL: `https://internship-management-system.vercel.app`

## Backend Deployment (Render)

### Prerequisites
- Render account (free tier available)
- MongoDB Atlas cluster (free tier: 512MB)
- GitHub repository

### MongoDB Atlas Setup

1. **Create MongoDB Cluster**
   - Go to [mongodb.com/cloud/atlas](https://mongodb.com/cloud/atlas)
   - Create free account
   - Create M0 (free) cluster
   - Create database user with password
   - Get connection string: `mongodb+srv://username:password@cluster.mongodb.net/internship`

### Deploy on Render

1. **Connect GitHub to Render**
   - Go to [render.com](https://render.com)
   - Click "New +" → "Web Service"
   - Select "Deploy existing repository"
   - Connect GitHub and select repository

2. **Configure Web Service**
   - **Root Directory**: `backend`
   - **Runtime**: Node
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`

3. **Add Environment Variables**
   - In Render dashboard, go to Environment
   - Add:
     ```
     MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/internship
     JWT_SECRET=your-secret-key-min-32-chars
     JWT_EXPIRE=7d
     NODE_ENV=production
     PORT=5000
     ```

4. **Deploy**
   - Click "Create Web Service"
   - Render will auto-deploy from main branch
   - Your backend URL: `https://internship-api.onrender.com`

## Post-Deployment Configuration

1. **Update Frontend API URL**
   - Re-deploy frontend with correct backend URL in environment variables

2. **Test Endpoints**
   ```bash
   # Test backend is live
   curl https://your-backend-url.onrender.com/api/auth/health
   
   # Test frontend
   Open https://your-frontend-url.vercel.app
   ```

3. **Enable Auto-Deployments**
   - Both platforms auto-deploy on git push to main
   - Check deployment status in Vercel & Render dashboards

## Troubleshooting

### Frontend Won't Build
- Check build logs in Vercel
- Ensure all dependencies are in package.json
- Verify environment variables are set

### Backend Crashes
- Check logs in Render dashboard
- Verify MongoDB connection string
- Ensure JWT_SECRET is set
- Check port configuration

### CORS Errors
- Add frontend URL to backend CORS config
- Update backend `.env` with frontend URL
- Redeploy backend

## Monitoring

- **Vercel**: Check Analytics tab for traffic, performance
- **Render**: Check Logs tab for errors, status page for uptime
- **MongoDB**: Monitor cluster in Atlas dashboard

## Cost Estimation

- Vercel Frontend: Free (with generous limits)
- Render Backend: Free tier (512MB RAM, auto-sleeps after 15min inactivity)
- MongoDB: Free tier (512MB storage)
- **Total Monthly Cost**: $0 (with limitations)

## Production Checklist

- [ ] Environment variables configured
- [ ] API endpoints tested
- [ ] CORS configured properly
- [ ] Authentication working
- [ ] Database connected
- [ ] Logs monitored
- [ ] SSL certificates (automatic)
- [ ] Custom domain configured (optional)
