# JXXVAN Portfolio — Full Stack Setup Guide

## Project Structure
```
jxxvan-portfolio/
├── backend/           ← Node.js API + SQLite database
│   ├── server.js      ← Main server
│   ├── package.json
│   └── .env.example   ← Copy to .env and fill in
└── frontend/
    └── public/
        └── index.html ← Your complete portfolio site
```

---

## Step 1 — Setup Backend

```bash
cd backend
npm install
cp .env.example .env
```

Edit `.env` with your real values:
```
PORT=3001
EMAIL_USER=your_gmail@gmail.com
EMAIL_PASS=your_app_password_here   # NOT your real password!
NOTIFY_EMAIL=your_gmail@gmail.com
FRONTEND_URL=http://localhost:5500
```

### Getting a Gmail App Password:
1. Go to https://myaccount.google.com/security
2. Turn on 2-Step Verification (required)
3. Search "App Passwords" in your Google Account
4. Create one for "Mail" → copy the 16-character code
5. Paste it as EMAIL_PASS in .env

### Start backend:
```bash
npm start
# → Running on http://localhost:3001
```

---

## Step 2 — Open Frontend

Open `frontend/public/index.html` in your browser.

**For live server (recommended):**
- Install VS Code extension "Live Server"
- Right-click index.html → "Open with Live Server"
- It opens on http://localhost:5500

---

## Step 3 — Test Contact Form

1. Fill out the form on your site
2. You get an email notification instantly
3. The person who contacted you gets a confirmation email
4. All messages saved to `backend/portfolio.db`

---

## View All Messages (Admin)

```bash
# All messages
curl http://localhost:3001/api/admin/messages

# Stats
curl http://localhost:3001/api/admin/stats
```

Or open the DB directly:
```bash
cd backend
npx better-sqlite3  # or use DB Browser for SQLite (free app)
```

---

## Deploy to the Internet (Free)

### Backend → Railway.app
1. Push backend/ to a GitHub repo
2. Go to railway.app → New Project → Deploy from GitHub
3. Add your .env variables in Railway dashboard
4. Railway gives you a URL like: https://jxxvan-api.railway.app

### Frontend → Netlify (free)
1. Go to netlify.com → drag and drop your frontend/public/ folder
2. Update the `API` variable in index.html to your Railway backend URL:
   ```js
   const API = "https://jxxvan-api.railway.app";
   ```

---

## Database Location
Messages are stored in: `backend/portfolio.db`

Use **DB Browser for SQLite** (free) to view them visually:
https://sqlitebrowser.org/

---

## Tech Stack
- **Frontend**: HTML, CSS, Vanilla JS
- **Backend**: Node.js + Express
- **Database**: SQLite (via better-sqlite3)
- **Email**: Nodemailer + Gmail SMTP
- **Rate limiting**: express-rate-limit (5 messages / 15 min per IP)
- **Validation**: express-validator
