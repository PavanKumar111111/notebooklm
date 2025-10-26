# NotebookLM Clone - Setup & Deployment Guide

## Project Overview

This is a fully functional Google NotebookLM clone that allows users to:
- Upload PDF documents
- View PDFs in an integrated viewer
- Ask questions about the PDF content through a chat interface
- Get citations that link directly to specific pages in the PDF

## Technology Stack

### Frontend
- React 18.2
- Vite 5.0 (build tool)
- Modern CSS

### Backend
- Node.js with Express
- Multer (file upload handling)
- pdf-parse (PDF text extraction)
- Simple in-memory vector store (can be replaced with Pinecone/Supabase)

## Project Structure

```
notebooklm-clone-deploy/
├── backend/
│   ├── server.js              # Express server with API endpoints
│   ├── package.json           # Backend dependencies
│   ├── render.yaml           # Render deployment config
│   └── utils/
│       ├── extractText.js    # PDF text extraction logic
│       └── vectorStore.js    # Simple keyword-based search
├── frontend/
│   ├── index.html            # Entry HTML file
│   ├── package.json          # Frontend dependencies
│   ├── vite.config.js        # Vite configuration
│   ├── netlify.toml          # Netlify deployment config
│   ├── .env.example          # Environment variable template
│   └── src/
│       ├── App.jsx           # Main application component
│       ├── main.jsx          # React entry point
│       ├── styles.css        # Global styles
│       └── components/
│           ├── ChatBox.jsx   # Chat interface component
│           └── PDFViewer.jsx # PDF viewer component
├── README.md                 # Project documentation
├── DEPLOYMENT.md            # Detailed deployment guide
└── .gitignore               # Git ignore rules
```

## Local Development Setup

### Prerequisites
- Node.js v18+ installed
- npm installed

### Step 1: Backend Setup

```bash
cd backend
npm install
npm run dev
```

The backend will start on `http://localhost:5000`

### Step 2: Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

The frontend will start on `http://localhost:5173`

### Step 3: Test the Application

1. Open `http://localhost:5173` in your browser
2. Upload a PDF file
3. Wait for processing
4. Ask questions in the chat interface
5. Click citation buttons to navigate to specific pages

## Features Implemented

### ✅ PDF Upload and Viewing
- Drag-and-drop or file picker upload
- PDF processing and text extraction
- Page-by-page text parsing

### ✅ Chat Interface
- Clean, intuitive chat UI
- Question/answer flow
- Loading states and error handling

### ✅ Citation & Navigation
- Citations displayed as clickable buttons
- Direct navigation to referenced pages
- Page number tracking

### ✅ Responsive Design
- Works on desktop and tablet
- Clean, modern interface
- Smooth interactions

## Environment Variables

### Frontend (.env)
```
VITE_BACKEND_URL=http://localhost:5000
```

For production, update to your deployed backend URL:
```
VITE_BACKEND_URL=https://your-backend.onrender.com
```

### Backend
No environment variables required for basic functionality. Optional:
```
PORT=5000
GEMINI_API_KEY=your_key_here  # If integrating real AI
```

## Deployment

See [DEPLOYMENT.md](./DEPLOYMENT.md) for complete deployment instructions.

### Quick Deploy Summary

1. **Backend to Render**:
   - Create web service
   - Set build command: `npm install`
   - Set start command: `npm start`
   - Copy deployment URL

2. **Frontend to Netlify**:
   - Build: `npm run build`
   - Deploy `dist` folder
   - Set `VITE_BACKEND_URL` environment variable
   - Redeploy

3. **Update CORS**:
   - Add frontend URL to backend CORS config
   - Redeploy backend

## API Endpoints

### POST /upload
Uploads and processes a PDF file.

**Request**: multipart/form-data with file field
**Response**:
```json
{
  "ok": true,
  "pages": 10
}
```

### POST /chat
Sends a question and receives an answer with citations.

**Request**:
```json
{
  "question": "What is the main topic?"
}
```

**Response**:
```json
{
  "answer": "The main topic is...",
  "citations": [1, 3, 5]
}
```

### GET /pdf/:page
Retrieves raw text for a specific page.

**Response**: Plain text content of the page

## Enhancements & Future Improvements

### Current Implementation
The current version uses:
- Simple keyword matching for retrieval
- Mock LLM responses (no real AI calls)
- In-memory storage (resets on restart)

### Recommended Upgrades

1. **Real AI Integration**:
   - Add OpenAI or Google Gemini API
   - Replace mock responses with actual LLM completions
   - Implement proper context injection

2. **Vector Database**:
   - Replace keyword search with embeddings
   - Use Pinecone, Supabase Vector, or Weaviate
   - Generate embeddings for each page
   - Perform similarity search for better retrieval

3. **Authentication**:
   - Add user accounts
   - Save chat history per user
   - Manage multiple documents per user

4. **Enhanced PDF Handling**:
   - Use `react-pdf` for better rendering
   - Support more file formats
   - Extract images and tables
   - Better page boundary detection

5. **Production Features**:
   - Rate limiting
   - File size validation
   - Virus scanning
   - CDN for static assets
   - Error tracking (Sentry)
   - Analytics

## Code Quality & Best Practices

### Backend
- Modular code structure with utils folder
- Error handling on all endpoints
- CORS configuration for security
- Multer for secure file uploads

### Frontend
- Component-based architecture
- Props and refs for component communication
- Environment variable support
- Clean separation of concerns

## Testing

### Manual Testing Checklist
- [ ] Upload PDF successfully
- [ ] View PDF content in viewer
- [ ] Send chat message
- [ ] Receive response with citations
- [ ] Click citation to navigate to page
- [ ] Upload different PDF
- [ ] Test error scenarios (no file, server down)

### Automated Testing (Future)
- Unit tests for extraction logic
- Component tests for React components
- E2E tests for full user flow
- API endpoint tests

## Troubleshooting

### Common Issues

**PDF Upload Fails**:
- Check file size (keep under 10MB)
- Verify backend is running
- Check network tab for errors

**Chat Not Responding**:
- Ensure PDF is uploaded first
- Check backend logs
- Verify CORS settings

**Build Fails**:
- Clear node_modules and reinstall
- Check Node.js version (use v18+)
- Verify all dependencies installed

**Citations Not Working**:
- Check that PDFViewer ref is properly passed
- Verify page numbers are being returned
- Check console for JavaScript errors

## Support & Documentation

- Main README: [README.md](./README.md)
- Deployment Guide: [DEPLOYMENT.md](./DEPLOYMENT.md)
- Assignment Spec: [example_assignment_spec.pdf](./example_assignment_spec.pdf)

## License

This project is created as a take-home assignment and is for educational purposes.

## Credits

Built with React, Express, and modern web technologies as a demonstration of PDF interaction and chat interface capabilities.
