# Medical SaaS Application

A modern full-stack SaaS application for medical visit documentation with AI-powered summarization. Built with Next.js for the frontend and FastAPI for the backend.

## Project Structure

```
sasvercel/
├── frontend/              # Next.js React application
│   ├── pages/            # Next.js pages and routes
│   ├── public/           # Static assets
│   ├── styles/           # CSS and Tailwind styles
│   ├── package.json      # Frontend dependencies
│   ├── tsconfig.json     # TypeScript configuration
│   ├── next.config.ts    # Next.js configuration
│   ├── postcss.config.mjs
│   ├── eslint.config.mjs
│   └── .env.example      # Frontend environment template
│
├── backend/              # FastAPI Python application
│   ├── api/             # FastAPI routes and models
│   │   ├── index.py     # Main FastAPI application
│   │   └── __init__.py
│   ├── requirements.txt  # Python dependencies
│   ├── Dockerfile       # Docker image configuration
│   ├── .dockerignore    # Docker build exclusions
│   └── .env.example     # Backend environment template
│
├── vercel.json          # Vercel build configuration
├── .gitignore           # Git ignore rules
└── README.md            # This file
```

## Tech Stack

### Frontend
- **Framework:** Next.js (React)
- **Language:** TypeScript
- **Styling:** Tailwind CSS
- **Authentication:** Clerk
- **Package Manager:** npm

### Backend
- **Framework:** FastAPI
- **Language:** Python 3.11+
- **Authentication:** Clerk JWT validation
- **AI Integration:** OpenAI API
- **Server:** Uvicorn

## Prerequisites

### Frontend Development
- Node.js 18+ and npm
- Modern web browser

### Backend Development
- Python 3.11+
- pip or uv package manager

## Getting Started

### Frontend Setup

1. Navigate to the frontend directory:
```bash
cd frontend
```

2. Install dependencies:
```bash
npm install
```

3. Create `.env.local` from `.env.example`:
```bash
cp .env.example .env.local
```

4. Update environment variables in `.env.local`:
```env
NEXT_PUBLIC_API_URL=http://localhost:8000
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=your_clerk_key_here
```

5. Run development server:
```bash
npm run dev
```

6. Open [http://localhost:3000](http://localhost:3000) in your browser

### Backend Setup

1. Navigate to the backend directory:
```bash
cd backend
```

2. Create a Python virtual environment:
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

4. Create `.env` from `.env.example`:
```bash
cp .env.example .env
```

5. Update environment variables in `.env`:
```env
CLERK_JWKS_URL=https://your-clerk-domain.clerk.accounts.com/.well-known/jwks.json
OPENAI_API_KEY=sk-your_openai_api_key_here
HOST=0.0.0.0
PORT=8000
```

6. Run development server:
```bash
uvicorn api.index:app --reload --host 0.0.0.0 --port 8000
```

7. Access API documentation at [http://localhost:8000/docs](http://localhost:8000/docs)

## Environment Variables

### Frontend (.env.local)
- `NEXT_PUBLIC_API_URL` - Backend API URL
- `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY` - Clerk public key

### Backend (.env)
- `CLERK_JWKS_URL` - Clerk JWKS endpoint URL
- `OPENAI_API_KEY` - OpenAI API key
- `HOST` - Server host (default: 0.0.0.0)
- `PORT` - Server port (default: 8000)
- `ALLOWED_ORIGINS` - CORS allowed origins

## API Endpoints

### POST /api
Generates a medical visit summary with AI assistance.

**Request:**
```json
{
  "patient_name": "John Doe",
  "date_of_visit": "2024-01-15",
  "notes": "Patient presents with fever and cough..."
}
```

**Response:** Server-sent events stream with AI-generated summary

**Authentication:** Requires valid Clerk JWT token

## Deployment

### Frontend (Vercel)

1. Push code to GitHub
2. Import project in Vercel dashboard
3. Set environment variables in Vercel project settings:
   - `NEXT_PUBLIC_API_URL` - Production API URL
   - `NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY` - Clerk key
4. Deploy (automatic on push to main)

The `vercel.json` configuration is already set up for Next.js deployment.

### Backend (Docker)

1. Build Docker image:
```bash
docker build -t medical-saas-backend:latest .
```

2. Run container:
```bash
docker run -p 8000:8000 \
  -e CLERK_JWKS_URL="your_clerk_url" \
  -e OPENAI_API_KEY="your_api_key" \
  medical-saas-backend:latest
```

### Backend (Railway/Render)

1. Push code to GitHub
2. Create new service in Railway/Render
3. Connect GitHub repository
4. Set environment variables
5. Deploy

## Development Workflow

### Running Both Services Locally

**Terminal 1 - Frontend:**
```bash
cd frontend
npm run dev
```

**Terminal 2 - Backend:**
```bash
cd backend
source venv/bin/activate  # Or: venv\Scripts\activate on Windows
uvicorn api.index:app --reload
```

Then:
- Frontend: http://localhost:3000
- Backend API: http://localhost:8000
- Backend Docs: http://localhost:8000/docs

## Project Features

- **Medical Visit Documentation** - Structured data capture for patient visits
- **AI-Powered Summarization** - Automatic generation of visit summaries using OpenAI
- **Patient Email Draft** - Auto-generate patient-friendly email communications
- **Secure Authentication** - Clerk integration for user management
- **Streaming Responses** - Real-time AI output via server-sent events
- **API Documentation** - Auto-generated Swagger UI documentation

## Contributing

1. Create feature branches from main
2. Implement changes
3. Test locally before pushing
4. Create pull request with description

## License

Proprietary - All rights reserved
