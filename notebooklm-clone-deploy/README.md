# NotebookLM Clone — Take-Home Assignment (Scaffold)

This repository is a **ready-to-run scaffold** for the "Build a Google NotebookLM Clone" take-home assignment.
It provides a React frontend + Express backend and demonstrates:
- PDF upload and simple per-page text extraction
- Chat interface that queries a minimal in-memory "vector store"
- Citations that link to specific pages in the PDF viewer

> IMPORTANT: This scaffold is intentionally self-contained and does **not** call any paid LLM APIs.
It includes clear instructions where to plug in Gemini / OpenAI / your vector DB (Pinecone / Supabase / etc).

## What I included
- /backend — Express server (endpoints: /upload, /chat, /pdf/:page)
- /frontend — Vite + React app (PDF viewer + Chat UI)
- README with instructions
- This zip was generated in the execution environment and is ready to download.

## How to run locally

Prerequisites: Node.js (v18+ recommended), npm.

### Backend
```bash
cd backend
npm install
# Start server
npm run dev
# Server runs on http://localhost:5000
```

### Frontend
```bash
cd frontend
npm install
npm run dev
# Vite dev server runs (commonly at http://localhost:5173)
```

Open the frontend URL in your browser, select a PDF, click Upload. The backend will parse text (best-effort) and the chat will operate over a simple keyword-match index.

## Where to plug an LLM and Vector DB
- Backend `server.js` calls `createVectorStore` and `queryVectorStore` in `utils/vectorStore.js`.
  Replace that file's logic with:
  1. Generate embeddings for each page (Gemini/OpenAI embeddings).
  2. Store them in Pinecone / Supabase / Weaviate.
  3. Query nearest neighbors for the question embedding and pass top-k contexts into a prompt to Gemini/LLM.
- In `server.js` replace the "Pretend-LLM response" block with a real call to Gemini or OpenAI to generate final answers.

## Deployment suggestions
- Frontend: Netlify, Vercel, or Netlify (build static site).
- Backend: Render, Railway, Fly, or Heroku (for a simple free tier).
- Vector DB: Pinecone or Supabase Vector.

## Notes / Limitations
- PDF text extraction may not preserve exact page boundaries for complex PDFs. For precise page extraction use `pdfjs-dist` or `pdf-lib`.
- This project intentionally keeps dependencies minimal to make it easy to run locally and extend.

Good luck — if you'd like, I can:
- Add real Gemini/OpenAI integration (you must provide API keys),
- Swap the demo vector store for Pinecone/Supabase and add code for embeddings,
- Improve PDF rendering with `react-pdf` and `pdfjs`.


---

## 🌍 Deployment Guide

This application is ready to deploy to free cloud providers. Follow these steps:

### Step 1: Deploy Backend to Render

1. Create a free account at [Render](https://render.com)
2. Click "New +" and select "Web Service"
3. Connect your repository or upload the `backend` folder
4. Configure the service:
   - **Name**: notebooklm-backend (or your choice)
   - **Environment**: Node
   - **Build Command**: `npm install`
   - **Start Command**: `npm start`
   - **Instance Type**: Free
5. Click "Create Web Service"
6. Wait for deployment to complete
7. Copy your backend URL (e.g., `https://notebooklm-backend.onrender.com`)

**Alternative**: You can also use Railway, Fly.io, or Heroku for backend hosting.

### Step 2: Deploy Frontend to Netlify

1. Create a free account at [Netlify](https://netlify.com)
2. Click "Add new site" > "Deploy manually" or connect your repository
3. If deploying manually, build locally first:
   ```bash
   cd frontend
   npm install
   npm run build
   ```
   Then drag and drop the `dist` folder to Netlify
4. If connecting repository:
   - **Base directory**: `frontend`
   - **Build command**: `npm run build`
   - **Publish directory**: `dist`
5. Add environment variable:
   - Go to Site settings > Environment variables
   - Add: `VITE_BACKEND_URL` = `https://your-backend.onrender.com`
6. Trigger a new deployment
7. Your app will be live at your Netlify URL

**Alternative**: You can also use Vercel for frontend hosting.

### Step 3: Update CORS (Important!)

After deploying, update the backend to allow requests from your frontend domain:

1. Edit `backend/server.js`
2. Update the CORS configuration:
   ```javascript
   app.use(cors({
     origin: ['https://your-netlify-app.netlify.app', 'http://localhost:5173']
   }));
   ```
3. Redeploy the backend

### Deployment Checklist

- [ ] Backend deployed and accessible via URL
- [ ] Frontend environment variable `VITE_BACKEND_URL` set correctly
- [ ] Frontend built and deployed
- [ ] CORS configured to allow frontend domain
- [ ] Test PDF upload and chat functionality
- [ ] Share URLs with others to verify public access

### Local Development

For testing locally before deployment:

```bash
# Terminal 1 - Backend
cd backend
npm install
npm run dev

# Terminal 2 - Frontend
cd frontend
npm install
npm run dev
```

The frontend will be available at `http://localhost:5173` and backend at `http://localhost:5000`.
