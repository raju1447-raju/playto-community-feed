# Playto Community Feed

This project is a Community Feed prototype built as part of the Playto Engineering Challenge.

## Tech Stack
- Backend: Django, Django REST Framework
- Frontend: React, Tailwind CSS
- Database: SQLite (local), PostgreSQL (production)

## Features
- Posts with likes
- Threaded (nested) comments
- Karma system
- Leaderboard (Top 5 users in last 24 hours)

## How to Run Locally

### Backend
```bash
cd backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
http://127.0.0.1:8000
cd frontend
npm install
npm run dev
http://localhost:5173


