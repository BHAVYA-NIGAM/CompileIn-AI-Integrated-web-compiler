# CompileIN

CompileIN is an AI-assisted web compiler that combines a browser-based code editor, cloud code execution, and a lightweight authentication backend. It is built for students and beginner-friendly coding workflows, with support for writing, running, and improving code from a single interface.

## Project Summary

The project has two main parts:

- A React + Vite frontend for the landing page, authentication screens, and compiler workspace
- A Node.js + Express backend for user signup, login, and profile lookup

The compiler experience lets users write code in multiple languages, run it through an online execution API, and ask AI for code help directly inside the editor.

## Technologies Used

### Frontend

- React 19
- Tailwind CSS
- Monaco Editor via `@monaco-editor/react`

### Backend

- Node.js
- Express
- MongoDB
- Mongoose
## APIs and External Services Used

### 1. Judge0 API

CompileIN sends source code to the Judge0 execution service to compile and run programs in the cloud.

- Used for: online code execution
- Endpoint used in the frontend:
  - `https://ce.judge0.com/submissions/?base64_encoded=false&wait=true`

### 2. Google Gemini API

The AI assistant inside the compiler uses the Google Generative AI SDK.

- Package used: `@google/generative-ai`
- Model used in the code: `gemini-2.5-flash`
- Used for:
  - code suggestions
  - AI chat/code assistance
  - helping users improve or generate code snippets

### 3. MongoDB Atlas

The backend stores user account data in MongoDB through Mongoose.

- Used for:
  - user registration
  - login lookup
  - fetching the logged-in user profile

## Core Functionalities

- Multi-language code editor using Monaco Editor
- Supports JavaScript, C, C++, Java, and Python
- Run code online with compile output, runtime errors, and program output
- AI mode for asking coding questions and getting generated code
- File-style editor workflow with add, rename, switch, and delete actions
- Terminal/output panel for input and execution results
- Login and signup system with hashed passwords
- User profile display using stored login state
- Responsive landing page and animated authentication screens
- Theme toggle and interactive UI effects

## Backend Routes

The Express server currently exposes these routes:

- `POST /api/auth/signup`
- `POST /api/auth/login`
- `GET /api/find/getUser/:id`

## Project Structure

```text
CompileIN-main/
├── src/                 # React frontend
├── server/              # Express + MongoDB backend
├── public / assets      # Images and UI assets
├── package.json         # Frontend dependencies
└── server/package.json  # Backend dependencies
```

## How It Works

1. Users open the frontend and navigate to the compiler.
2. They select a language and write code in Monaco Editor.
3. On run, the frontend sends the code to Judge0 for execution.
4. Output, compile errors, or runtime errors are shown in the terminal panel.
5. If AI mode is enabled, users can ask questions and receive code help from Gemini.
6. Authentication is handled by the backend using MongoDB and bcrypt-based password hashing.

## Local Setup

### Frontend

```bash
npm install
npm run dev
```

### Backend

```bash
cd server
npm install
npm start
```

The backend runs on `http://localhost:8000` and the frontend expects that server for login/signup requests.

## Environment Notes

- The frontend expects a Gemini API key in `VITE_GEMINI_API_KEY`
- The backend currently connects to MongoDB through the connection string defined in `server/config/db.js`

## Recommended Improvements

- Move the MongoDB connection string into environment variables
- Add JWT/session-based authentication instead of only local storage flags
- Add code persistence per user
- Add proper formatter integration per language
- Add tests for frontend and backend flows
- Add deployment instructions for frontend and server separately
