# CareerPilot ✈️

CareerPilot is an AI-powered mock interview strategy assistant and custom resume tailor designed to help job seekers land their dream roles. By analyzing target job descriptions against candidate profiles (via resumes or self-descriptions), CareerPilot generates custom-tailored interview strategies, questions, prep roadmaps, and optimized PDF resumes.

---

## 🚀 Features

### 1. AI Mock Interview Strategy & Analysis
* **Match Score:** Instantly see how well your profile aligns with the target job description (0-100%).
* **Technical Questions:** Get targeted technical questions likely to be asked, explaining the *interviewer's intent* and providing *model answers*.
* **Behavioral Questions:** Practice behavioral scenarios customized to the role, complete with answering strategies.
* **Skill Gap Analysis:** Identify specific areas where you might fall short compared to the job requirements, categorized by severity (`low`, `medium`, `high`).
* **Custom Preparation Roadmap:** A day-wise, step-by-step prep plan tailored to bridge your skill gaps and master key topics.

### 2. Tailored ATS-Friendly Resume PDF Generator
* Generates a tailored, ATS-friendly professional resume based on your profile and target job description using the Gemini API.
* Automatically compiles and renders high-quality resumes from HTML templates directly to a downloadable PDF via Puppeteer.

### 3. Secure Authentication & Session Management
* Secure registration and login using JWT (JSON Web Tokens) stored in secure HTTP-only cookies.
* Token blacklisting on logout to prevent unauthorized reuse.
* Protected routing on the frontend ensures your interview plans and resumes remain secure.

---

## 🛠️ Tech Stack

### Frontend
* **React 19** - Component-based user interface.
* **Vite** - High-performance frontend build tool.
* **Sass (SCSS)** - Modern, structured styling with smooth transitions and layout designs.
* **React Router v7** - Declarative routing and route protection.
* **Axios** - Promise-based HTTP client for API requests.

### Backend
* **Node.js & Express** - Scalable backend framework.
* **MongoDB & Mongoose** - Document database to store users, resumes, and interview reports.
* **Google Gemini API** (`@google/genai`) - Powered by `gemini-3-flash-preview` for intelligent schema-based text generation.
* **Puppeteer** - Headless browser for rendering and exporting resumes to PDFs.
* **pdf-parse** - Server-side PDF extraction to parse uploaded resumes.
* **Multer** - Middleware for handling file uploads.

---

## 📦 Project Structure

```text
CareerPilot/
├── Backend/                 # Express Server & DB Models
│   ├── src/
│   │   ├── config/          # DB Configuration
│   │   ├── controllers/     # Route Controllers
│   │   ├── middlewares/     # Authentication & File Upload Handling
│   │   ├── models/          # Mongoose Schemas (User, InterviewReport, Blacklist)
│   │   ├── routes/          # Express API Endpoints
│   │   └── services/        # Gemini AI Integration & PDF rendering
│   ├── server.js            # Server Entry Point
│   └── package.json
│
├── Frontend/                # Vite React App
│   ├── src/
│   │   ├── features/        # Auth and Interview feature components & pages
│   │   ├── hooks/           # Custom React hooks (useInterview, etc.)
│   │   ├── style/           # SCSS stylesheets
│   │   ├── App.jsx          # App wrapper
│   │   └── main.jsx         # App entry point
│   ├── index.html
│   └── package.json
│
├── package.json             # Root monorepo dev configuration
└── README.md                # Project documentation
```

---

## ⚙️ Installation & Setup

### Prerequisites
* **Node.js** (v18.x or higher)
* **MongoDB** (Local instance or MongoDB Atlas cluster)
* **Google Gemini API Key** (Get one from [Google AI Studio](https://aistudio.google.com/))

### 1. Clone the Repository
```bash
git clone https://github.com/AnuJaiswal2004/CareerPilot.git
cd CareerPilot
```

### 2. Install Dependencies
Install dependencies concurrently for the root, backend, and frontend:
```bash
# Install root workspace dependencies
npm install

# Install backend dependencies
cd Backend
npm install

# Install frontend dependencies
cd ../Frontend
npm install
```

### 3. Environment Variables Configuration
Create a `.env` file in the **`Backend`** directory:
```env
# Backend/.env
PORT=3000
MONGO_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/CareerPilot
JWT_SECRET=your_jwt_secret_key_here
GOOGLE_GENAI_API_KEY=your_google_gemini_api_key_here
```

### 4. Running the Application
From the **root directory**, you can start both the backend and frontend concurrently in development mode:
```bash
npm run dev
```
* **Backend** runs on: `http://localhost:3000`
* **Frontend** runs on: `http://localhost:5173`

---

## 🔗 API Endpoints

### Authentication Routes (`/api/auth`)
* `POST /api/auth/register` - Create a new account.
* `POST /api/auth/login` - Authenticate user and issue cookie token.
* `GET /api/auth/logout` - Clear token cookie and blacklist token.
* `GET /api/auth/get-me` - Fetch authenticated user details (Private).

### Interview Routes (`/api/interview`)
* `POST /api/interview/` - Generate a new interview report using uploaded resume PDF, self-description, and target job description (Private).
* `GET /api/interview/report/:interviewId` - Fetch a specific report by ID (Private).
* `GET /api/interview/` - List all reports created by the logged-in user (Private).
* `POST /api/interview/resume/pdf/:interviewReportId` - Compile and download a custom tailored resume PDF (Private).

---

## 📄 License

This project is licensed under the ISC License.
