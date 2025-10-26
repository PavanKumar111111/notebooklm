# Deployment Checklist for NotebookLM Clone

## Pre-Deployment Verification

### Local Testing
- [x] Backend runs successfully on localhost:5000
- [x] Frontend builds without errors
- [x] Environment variables configured correctly
- [ ] Test PDF upload locally
- [ ] Test chat functionality locally
- [ ] Test citation navigation locally

### Code Review
- [x] All environment variables use proper fallbacks
- [x] CORS is configurable
- [x] Error handling implemented
- [x] No hardcoded URLs (uses env variables)
- [x] .gitignore configured properly

### Documentation
- [x] README.md updated with full instructions
- [x] DEPLOYMENT.md created with step-by-step guide
- [x] SETUP.md created with technical details
- [x] All configuration files included

## Deployment Steps

### Step 1: Backend Deployment (Render)
- [ ] Create Render account
- [ ] Create new Web Service
- [ ] Upload or connect backend code
- [ ] Configure build command: `npm install`
- [ ] Configure start command: `npm start`
- [ ] Set instance type to Free
- [ ] Deploy service
- [ ] Copy deployment URL
- [ ] Test backend health: `curl https://your-backend.onrender.com`

### Step 2: Frontend Deployment (Netlify)
- [ ] Create Netlify account
- [ ] Build frontend locally: `cd frontend && npm run build`
- [ ] Deploy via drag-and-drop or Git
- [ ] Add environment variable `VITE_BACKEND_URL`
- [ ] Set to backend URL from Step 1
- [ ] Trigger deployment
- [ ] Copy frontend URL

### Step 3: CORS Configuration
- [ ] Update `backend/server.js` CORS config
- [ ] Add frontend URL to allowed origins
- [ ] Redeploy backend on Render
- [ ] Wait for deployment to complete

### Step 4: Testing
- [ ] Visit frontend URL
- [ ] Upload a PDF file
- [ ] Verify PDF processes successfully
- [ ] Ask a question in chat
- [ ] Verify response is received
- [ ] Click a citation button
- [ ] Verify page navigation works
- [ ] Test on different browsers
- [ ] Test on mobile device

### Step 5: Final Verification
- [ ] Backend accessible via public URL
- [ ] Frontend accessible via public URL
- [ ] No CORS errors in console
- [ ] File upload works
- [ ] Chat responses work
- [ ] Citations work
- [ ] No console errors

## Post-Deployment

### Documentation
- [ ] Document backend URL
- [ ] Document frontend URL
- [ ] Update README if needed
- [ ] Note any issues encountered

### Packaging for Submission
- [ ] Remove node_modules folders
- [ ] Remove dist/build folders
- [ ] Remove .env files (keep .env.example)
- [ ] Create zip file with both frontend and backend
- [ ] Verify zip contains all source code
- [ ] Test extracting zip and running locally

### Submission Package Contents
Required files:
- [x] backend/ folder with all source code
- [x] frontend/ folder with all source code
- [x] README.md with installation instructions
- [x] DEPLOYMENT.md with deployment guide
- [x] SETUP.md with technical documentation
- [x] Configuration files (package.json, vite.config.js, etc.)
- [x] .gitignore file
- [x] netlify.toml for frontend deployment
- [x] render.yaml for backend deployment

Should NOT include:
- [ ] node_modules/ folders
- [ ] dist/ or build/ folders
- [ ] .env files with secrets
- [ ] uploads/ folder
- [ ] .git/ folder

## URLs to Document

```
Backend URL: ____________________________________
Frontend URL: ____________________________________
```

## Notes
- Render free tier may sleep after 15 minutes of inactivity
- First request after sleep takes 30-60 seconds
- Netlify deployments are instant
- Check logs if something doesn't work

## Optional Enhancements (Future)
- [ ] Add real OpenAI/Gemini integration
- [ ] Implement vector database (Pinecone/Supabase)
- [ ] Add user authentication
- [ ] Add rate limiting
- [ ] Improve PDF rendering with react-pdf
- [ ] Add file size validation
- [ ] Add progress indicators
- [ ] Implement chat history
