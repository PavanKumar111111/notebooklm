# Quick Start Guide - NotebookLM Clone

## What is this?

A Google NotebookLM clone that lets you upload PDFs and chat about their content with citations linking back to specific pages.

## Run Locally (5 minutes)

### Terminal 1 - Backend
```bash
cd backend
npm install
npm run dev
```
Backend runs on http://localhost:5000

### Terminal 2 - Frontend
```bash
cd frontend
npm install
npm run dev
```
Frontend runs on http://localhost:5173

### Test It
1. Open http://localhost:5173
2. Upload a PDF
3. Ask "What is this document about?"
4. Click citation buttons to jump to pages

## Deploy Online (15 minutes)

### 1. Deploy Backend (Render)
- Go to https://render.com
- New Web Service
- Upload `backend` folder
- Build: `npm install`
- Start: `npm start`
- Copy your URL: `https://xxx.onrender.com`

### 2. Deploy Frontend (Netlify)
- Go to https://netlify.com
- New Site → drag `frontend` folder
- Set Environment Variable:
  - `VITE_BACKEND_URL` = your Render URL
- Redeploy

### 3. Update CORS
In `backend/server.js` change:
```javascript
app.use(cors({
  origin: ['https://your-app.netlify.app', 'http://localhost:5173']
}));
```
Redeploy backend.

Done! Your app is live.

## Files Overview

```
backend/
  server.js          → API endpoints
  utils/
    extractText.js   → Extract text from PDFs
    vectorStore.js   → Simple keyword search

frontend/
  src/
    App.jsx          → Main app
    components/
      ChatBox.jsx    → Chat interface
      PDFViewer.jsx  → PDF display
```

## Key Features

✅ PDF upload and parsing
✅ Chat interface
✅ Citations with page navigation
✅ Clean, responsive UI
✅ Ready to deploy

## Need Help?

- Full docs: [README.md](README.md)
- Deployment guide: [DEPLOYMENT.md](DEPLOYMENT.md)
- Technical details: [SETUP.md](SETUP.md)
- Checklist: [CHECKLIST.md](CHECKLIST.md)

## Common Issues

**Build fails?** 
```bash
rm -rf node_modules package-lock.json
npm install
```

**CORS errors?**
Check backend allows your frontend URL

**Upload fails?**
Verify backend is running and URL is correct
