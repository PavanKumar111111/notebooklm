# Deployment Instructions

## Quick Start Deployment Guide

### Prerequisites
- GitHub account (optional but recommended)
- Render account (free)
- Netlify account (free)

## Option 1: Deploy Without GitHub (Manual Upload)

### Backend (Render)

1. Go to [Render Dashboard](https://dashboard.render.com/)
2. Click "New +" → "Web Service"
3. Select "Build and deploy from a Git repository" OR "Deploy an existing image/code"
4. If uploading manually:
   - Zip the `backend` folder
   - Upload via Render CLI or connect via Git
5. Configure:
   ```
   Name: notebooklm-backend
   Environment: Node
   Build Command: npm install
   Start Command: npm start
   Instance Type: Free
   ```
6. Click "Create Web Service"
7. **IMPORTANT**: Copy the deployment URL (e.g., `https://notebooklm-backend.onrender.com`)

### Frontend (Netlify)

1. Open terminal in the `frontend` directory
2. Build the project:
   ```bash
   npm install
   npm run build
   ```
3. Go to [Netlify](https://app.netlify.com/)
4. Drag and drop the `dist` folder to deploy
5. After deployment, go to Site Settings → Environment Variables
6. Add variable:
   ```
   Key: VITE_BACKEND_URL
   Value: https://notebooklm-backend.onrender.com (your Render URL)
   ```
7. Go to Deploys → Trigger deploy → Deploy site

## Option 2: Deploy With GitHub (Recommended)

### Setup Repository

1. Create a new GitHub repository
2. Upload both `frontend` and `backend` folders
3. Push to GitHub

### Backend (Render)

1. Go to [Render Dashboard](https://dashboard.render.com/)
2. Click "New +" → "Web Service"
3. Connect your GitHub repository
4. Configure:
   ```
   Name: notebooklm-backend
   Root Directory: backend
   Environment: Node
   Build Command: npm install
   Start Command: npm start
   Instance Type: Free
   ```
5. Click "Create Web Service"
6. Copy the deployment URL

### Frontend (Netlify)

1. Go to [Netlify](https://app.netlify.com/)
2. Click "Add new site" → "Import an existing project"
3. Connect to GitHub and select your repository
4. Configure:
   ```
   Base directory: frontend
   Build command: npm run build
   Publish directory: dist
   ```
5. Add environment variable:
   ```
   VITE_BACKEND_URL=https://notebooklm-backend.onrender.com
   ```
6. Click "Deploy site"

## Post-Deployment

### Update CORS Settings

After both services are deployed, update the backend CORS configuration:

1. Edit `backend/server.js`:
   ```javascript
   app.use(cors({
     origin: [
       'https://your-app.netlify.app',
       'http://localhost:5173'
     ]
   }));
   ```
2. Commit and push (if using GitHub) or redeploy on Render

### Test Your Application

1. Visit your Netlify URL
2. Upload a PDF file
3. Wait for processing
4. Ask questions in the chat interface
5. Click citation buttons to navigate to specific pages

## Troubleshooting

### CORS Errors
- Ensure backend CORS includes your frontend URL
- Check that `VITE_BACKEND_URL` is set correctly in Netlify

### Build Failures
- Frontend: Ensure `@vitejs/plugin-react` is in devDependencies
- Backend: Verify all dependencies are listed in package.json

### Backend Not Responding
- Check Render logs for errors
- Verify the service is running (Free tier may sleep after inactivity)
- First request might take 30-60 seconds to wake up

### PDF Upload Issues
- Check browser console for errors
- Verify backend URL is accessible
- Ensure file size is reasonable (under 10MB for free tier)

## Cost Considerations

Both Render and Netlify offer generous free tiers:
- **Render**: 750 hours/month free (sufficient for this project)
- **Netlify**: 100GB bandwidth/month free

Note: Render free tier services sleep after 15 minutes of inactivity. The first request after sleep takes 30-60 seconds to respond.

## Alternative Hosting Options

### Frontend Alternatives
- **Vercel**: Similar to Netlify with free tier
- **GitHub Pages**: Free static hosting
- **Cloudflare Pages**: Fast edge hosting

### Backend Alternatives
- **Railway**: Easy deployment with free tier
- **Fly.io**: Global deployment with free allowance
- **Heroku**: Classic option (limited free tier)

## Production Enhancements

For a production deployment, consider:

1. **Add real AI integration**: Replace mock responses with OpenAI/Gemini API
2. **Use vector database**: Implement Pinecone or Supabase Vector for better search
3. **Add authentication**: Protect uploads and chat history
4. **Implement rate limiting**: Prevent abuse of APIs
5. **Add file size limits**: Validate uploads on both frontend and backend
6. **Use CDN**: Serve static assets faster
7. **Add monitoring**: Use services like Sentry for error tracking
8. **Implement caching**: Speed up repeated queries

## Security Checklist

- [ ] CORS properly configured (not using '*' in production)
- [ ] Environment variables set correctly
- [ ] No API keys committed to repository
- [ ] File upload validation implemented
- [ ] Rate limiting added for API endpoints
- [ ] HTTPS enabled (automatic with Netlify/Render)
