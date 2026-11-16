# job-tracker
Personal job tracker to keep up with 2026's tough IT marketplace

## Project Status
Current development: Milestone M0 (Backend and frontend initialization complete)

## Requirements
- Python 3.12+
- Node.js 26.13.0
- npm 12.2.2

## Backend Setup
1. Create virtual environment: `python -m venv backend/.venv`
2. Activate: `source backend/.venv/bin/activate`
3. Install requirements: `pip install -r backend/requirements.txt`
4. Start server: `uvicorn backend.app.main:app --reload`
5. Test: `curl http://localhost:8000/health`

## Frontend Setup
1. Install dependencies: `npm install`
2. Start development server: `npm run dev`
3. Build production: `npm run build`
