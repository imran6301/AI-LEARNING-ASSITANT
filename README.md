# AI Learning Assistant

## Overview

AI Learning Assistant is a full-stack web application built with **React**, **Node.js**, and **MongoDB** that transforms the way students and lifelong learners engage with study material. Powered by **Google Gemini**, it enables users to upload documents, generate flashcards, take AI-evaluated quizzes, ask questions, and get concept explanations — all in one place.

The platform is designed for students, educators, and self-learners who want to study smarter using AI-generated insights from their own content.

---

## Features

- **Flashcard Generation**: Auto-generate flashcard sets from uploaded documents or topics using Gemini AI.
- **Interactive Quiz**: Take quizzes based on generated flashcards with real-time AI-evaluated feedback.
- **Document Summarization**: Upload PDFs and get concise, structured summaries with key points.
- **Q&A Chat**: Ask questions about your uploaded content and get contextual, AI-powered answers.
- **Concept Explanation**: Get plain-English explanations for complex topics with examples via AI Actions.
- **Progress Tracking**: Track quiz scores and study history across sessions via the progress system.
- **Authentication**: Secure login/register flow with JWT-based auth and protected routes.
- **Responsive Design**: Clean layout with sidebar navigation, reusable components, and markdown rendering.

---

## Pages and Their Functions

### Auth (`/login`, `/register`)
- `LoginPage.jsx` — User login with JWT authentication.
- `RegisterPage.jsx` — New user registration with form validation.
- `ProtectedRoute.jsx` — Guards all pages requiring authentication; redirects unauthenticated users.

### Dashboard (`/dashboard`)
- `DashboardPage.jsx` — Overview of study stats (flashcard sets, quizzes taken, documents uploaded, average score).
- Recent activity feed and quick-action buttons to start a new session, upload a document, or generate flashcards.

### Documents (`/documents`)
- `DocumentListPage.jsx` — Lists all uploaded documents with metadata and upload option.
- `DocumentDetailsPage.jsx` — View document summary, extracted key points, and Q&A chat for a specific document.
- `DocumentCard.jsx` — Card component displaying document title, date, and actions.

### Flashcards (`/flashcards`)
- `FlashcardsListPage.jsx` — Lists all flashcard sets organized by topic.
- `FlashcardPage.jsx` — Interactive 3D flip card view for studying a selected deck.
- `FlashCard.jsx` — Individual card component with front (question) / back (answer) flip animation.
- `FlashcardManager.jsx` — Manage decks: create, delete, star cards, with AI generation option.
- `FlashcardSetCard.jsx` — Card component showing deck name, card count, and actions.

### Quizzes (`/quizzes`)
- `QuizTakePage.jsx` — Take a quiz from a selected flashcard deck (timed/untimed modes).
- `QuizResultPage.jsx` — Score summary with correct/incorrect breakdown and AI explanations.
- `QuizCard.jsx` — Individual question component (multiple choice / short answer).
- `QuizManager.jsx` — Browse and manage past quiz sessions.

### Profile (`/profile`)
- `ProfilePage.jsx` — User profile, account settings, and study statistics.

### Not Found
- `NotFoundPage.jsx` — 404 fallback page for unmatched routes.

---

## Project Structure

```
AILEARNINGASSISTANT/
├── backend/
│   ├── config/
│   │   ├── db.js                      # MongoDB Atlas connection
│   │   └── multer.js                  # File upload config (PDF handling)
│   ├── controllers/
│   │   ├── aiController.js            # Gemini AI — summarization, Q&A, concept explanation
│   │   ├── authController.js          # Register, login, JWT issuance
│   │   ├── documentController.js      # Upload, list, fetch, delete documents
│   │   ├── flashcardController.js     # CRUD for flashcard sets and individual cards
│   │   ├── progressController.js      # Track and retrieve user study progress
│   │   └── quizController.js          # Quiz creation, submission, and result storage
│   ├── middleware/
│   │   ├── auth.js                    # JWT verification middleware
│   │   └── errorHandler.js            # Global error handling middleware
│   ├── models/
│   │   ├── chatHistory.js             # MongoDB schema for Q&A conversation history
│   │   ├── Document.js                # Schema for uploaded documents
│   │   ├── Flashcard.js               # Schema for flashcard sets and cards
│   │   ├── Quiz.js                    # Schema for quiz sessions and results
│   │   └── User.js                    # Schema for user accounts
│   ├── routes/
│   │   ├── aiRoutes.js                # Routes: /api/ai/*
│   │   ├── authRoutes.js              # Routes: /api/auth/*
│   │   ├── documentRoutes.js          # Routes: /api/documents/*
│   │   ├── flashcardRoutes.js         # Routes: /api/flashcards/*
│   │   ├── progressRoutes.js          # Routes: /api/progress/*
│   │   └── quizRoutes.js              # Routes: /api/quiz/*
│   ├── uploads/
│   │   └── documents/                 # Uploaded PDF files stored here
│   ├── utils/
│   │   ├── geminiService.js           # Gemini API integration (prompts, responses)
│   │   ├── pdfParser.js               # Extracts text from uploaded PDFs
│   │   └── textChunker.js             # Splits long text into chunks for AI processing
│   ├── .env                           # Environment variables (not committed)
│   ├── package.json
│   ├── server.js                      # Express app entry point
│   └── vercel.json                    # Vercel deployment config
│
└── frontend/ai-learning-assistant/
    ├── public/
    ├── src/
    │   ├── assets/
    │   ├── components/
    │   │   ├── ai/
    │   │   │   └── AIActions.jsx          # AI summarization + concept explanation modals
    │   │   ├── auth/
    │   │   │   └── ProtectedRoute.jsx     # Auth guard for private routes
    │   │   ├── chat/
    │   │   │   └── ChatInterface.jsx      # Document Q&A chat UI
    │   │   ├── common/
    │   │   │   ├── Button.jsx
    │   │   │   ├── EmptyState.jsx
    │   │   │   ├── MarkdownRenderer.jsx   # Renders Gemini markdown responses
    │   │   │   ├── Modal.jsx
    │   │   │   ├── PageHeader.jsx
    │   │   │   ├── Spinner.jsx
    │   │   │   └── Tabs.jsx
    │   │   ├── documents/
    │   │   │   └── DocumentCard.jsx
    │   │   ├── flashcards/
    │   │   │   ├── FlashCard.jsx          # 3D flip card component
    │   │   │   ├── FlashcardManager.jsx   # Deck management UI
    │   │   │   └── FlashcardSetCard.jsx
    │   │   ├── layout/
    │   │   │   ├── AppLayout.jsx          # Main layout wrapper
    │   │   │   ├── Header.jsx
    │   │   │   └── Sidebar.jsx
    │   │   └── quizzes/
    │   │       ├── QuizCard.jsx
    │   │       └── QuizManager.jsx
    │   ├── context/
    │   │   └── AuthContext.jsx            # Global auth state (React Context)
    │   ├── pages/
    │   │   ├── Auth/
    │   │   │   ├── LoginPage.jsx
    │   │   │   └── RegisterPage.jsx
    │   │   ├── Dashboard/
    │   │   │   └── DashboardPage.jsx
    │   │   ├── Documents/
    │   │   │   ├── DocumentDetailsPage.jsx
    │   │   │   └── DocumentListPage.jsx
    │   │   ├── Flashcards/
    │   │   │   ├── FlashcardPage.jsx
    │   │   │   └── FlashcardsListPage.jsx
    │   │   ├── Profile/
    │   │   │   └── ProfilePage.jsx
    │   │   ├── Quizzes/
    │   │   │   ├── QuizResultPage.jsx
    │   │   │   └── QuizTakePage.jsx
    │   │   └── NotFoundPage.jsx
    │   ├── services/
    │   │   ├── aiService.js               # Gemini API calls from frontend
    │   │   ├── authService.js             # Login, register, token management
    │   │   ├── documentService.js         # Document upload and fetch APIs
    │   │   ├── flashcardService.js        # Flashcard CRUD API calls
    │   │   ├── progressService.js         # Progress fetch API calls
    │   │   └── quizService.js             # Quiz submit and result API calls
    │   ├── utils/
    │   │   ├── apiPaths.js                # Centralized API endpoint constants
    │   │   └── axiosInstance.js           # Axios config with base URL + auth headers
    │   ├── App.jsx
    │   ├── index.css
    │   └── main.jsx
    ├── .env
    └── package.json
```

---

## Setup and Installation

### Prerequisites

- Node.js 18+
- MongoDB Atlas account (or local MongoDB instance)
- Google Gemini API key

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/ai-learning-assistant.git
cd ai-learning-assistant
```

### 2. Install Dependencies

```bash
# Backend
cd backend
npm install

# Frontend
cd ../frontend/ai-learning-assistant
npm install
```

### 3. Configure Environment Variables

Create a `.env` file in `backend/`:

```env
MONGO_URI=your_mongodb_atlas_connection_string
GEMINI_API_KEY=your_google_gemini_api_key
JWT_SECRET=your_jwt_secret_key
PORT=5000
```

Create a `.env` file in `frontend/ai-learning-assistant/`:

```env
VITE_API_BASE_URL=http://localhost:5000
```

### 4. Run the App

```bash
# Start the backend
cd backend
npm run dev

# Start the frontend (new terminal)
cd frontend/ai-learning-assistant
npm run dev
```

Open [http://localhost:5173](http://localhost:5173) in your browser.

---

## Usage

1. **Register / Login**: Create an account or log in — all routes are protected via JWT.
2. **Upload a Document**: Go to Documents, upload a PDF — Gemini auto-summarizes it on upload.
3. **Chat with your Document**: Open a document and ask questions in the chat interface.
4. **Generate Flashcards**: In Flashcard Manager, generate a deck from a topic or uploaded document.
5. **Study Flashcards**: Flip through cards with the 3D flip animation; star important ones.
6. **Take a Quiz**: Go to Quizzes, select a deck, and get AI-evaluated results with explanations.
7. **Track Progress**: View scores, history, and study stats on the Dashboard and Profile pages.

---

## Data Processing

- **Document Handling**: Uploaded PDFs are stored in `backend/uploads/documents/`, parsed with `pdfParser.js`, and chunked via `textChunker.js` before being sent to Gemini.
- **Flashcard Generation**: `geminiService.js` receives topic/document chunks and returns structured Q&A pairs saved to MongoDB via the `Flashcard` model.
- **Quiz Evaluation**: Answers are evaluated semantically by Gemini, not by exact string match, enabling short-answer formats.
- **Conversation History**: Q&A sessions are stored in the `chatHistory` MongoDB collection for multi-turn contextual responses.
- **Auth Flow**: Passwords are hashed server-side; JWT tokens are issued on login and verified by `auth.js` middleware on all protected routes.
- **API Communication**: Frontend uses a centralized `axiosInstance.js` with base URL and auth headers; all endpoint paths managed in `apiPaths.js`.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 18, Tailwind CSS, Lucide React |
| Backend | Node.js, Express |
| Database | MongoDB Atlas |
| AI / LLM | Google Gemini API |
| Auth | JWT (JSON Web Tokens) |
| File Upload | Multer |
| PDF Parsing | pdf-parse |
| HTTP Client | Axios |
| Deployment | Vercel (via `vercel.json`) |

---

## Potential Issues and Troubleshooting

- **MongoDB Connection Error**: Ensure your Atlas cluster allows your IP (or set `0.0.0.0/0` for development open access).
- **Gemini API Errors**: Verify `GEMINI_API_KEY` is valid and has quota remaining in Google AI Studio.
- **PDF Parsing Issues**: Ensure the uploaded file is not password-protected; `pdf-parse` requires readable PDFs.
- **JWT Errors**: If getting 401s, check that `JWT_SECRET` matches between `.env` and the token issued at login.
- **CORS Errors**: Ensure the backend CORS config allows `http://localhost:5173` (Vite dev server origin).
- **File Upload Fails**: Confirm `multer.js` config points to the correct `uploads/documents/` directory and it exists.

---

## Contributing

1. Fork the repository and create a feature branch.
2. Make changes and test on both frontend and backend.
3. Update this README if new pages, routes, or features are added.
4. Submit a pull request with a clear description of changes.

---

## License

This project is open-source. Feel free to use and modify for non-commercial and educational purposes.

For questions or feature requests, open an issue or extend `geminiService.js` and the relevant controllers for new AI capabilities.
