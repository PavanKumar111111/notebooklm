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

## 🌍 Deployment (Ready Configuration)

### Frontend (Netlify)
- Environment Variable: `VITE_BACKEND_URL=https://your-backend.onrender.com`
- Build Command: `npm run build`
- Publish Directory: `dist`
- Framework: Vite (auto-detected)

### Backend (Render)
- Build Command: `npm install`
- Start Command: `npm start`
- Environment Variables:
  - `PORT=10000` (Render default)
  - `GEMINI_API_KEY=your_key` (if using Gemini API)

After deployment, update your frontend `.env` with:
```
VITE_BACKEND_URL=https://your-backend.onrender.com
```
and rebuild.
