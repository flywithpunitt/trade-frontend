# TradingView Automation Platform

## Overview
This project is a full-stack platform for automating TradingView chart interactions, including drawing and customizing trendlines based on user/admin actions from a web frontend. It consists of three main parts:

- **Frontend:** React (Vite) app for user/admin interaction and chart visualization.
- **Backend (Python):** Playwright-based automation for TradingView, handling login, chart navigation, and trendline customization.
- **Node.js API:** Express.js backend for user management, authentication, and secure credential storage.

---

## Directory Structure

```
/
├── backend/              # Python Playwright automation backend
├── profilebackend/       # Node.js/Express user/auth API
├── vite-project/         # React (Vite) frontend
└── README.md             # This file
```

---

## 1. Frontend (vite-project)

- **Tech:** React, Vite, TailwindCSS
- **Location:** `vite-project/`
- **Main files:**
  - `src/App.jsx` — Main app logic, chart click handling
  - `src/context/AuthContext.jsx` — Auth/session management
  - `src/components/auth/` — Login, profile, modals
  - `src/components/dashboard/AdminDashboard.jsx` — Admin features

### Setup & Run
```bash
cd vite-project
npm install
npm run dev
```
- App runs on [http://localhost:5173](http://localhost:5173) by default.

### Features
- User/admin login and registration
- Chart visualization and interaction
- Sends trigger data (symbol, price, color, etc.) to backend for TradingView automation
- Admin dashboard for privileged users

---

## 2. Backend Automation (backend)

- **Tech:** Python, Playwright
- **Location:** `backend/`
- **Main files:**
  - `requirements.txt` — Python dependencies
  - `trigger_data.json` — Receives trigger data from frontend
  - `auth/` — Auth helpers (if needed)

### Setup & Run
```bash
cd backend
python -m venv env
source env/bin/activate  # or env\Scripts\activate on Windows
pip install -r requirements.txt
# Install Playwright browsers (first time only):
python -m playwright installs
```

### Features
- Logs into TradingView using credentials from Node.js API
- Navigates to the correct symbol, timeframe, and timestamp
- Draws a trendline and customizes:
  - **Color:** Based on frontend input
  - **Text:** Inferred from color/type and price
  - **Coordinates:** Sets both price fields to the selected price
- Fully automated UI steps (tab navigation, input, confirmation)

---

## 3. Node.js API (profilebackend)

- **Tech:** Node.js, Express, MongoDB (or similar)
- **Location:** `profilebackend/`
- **Main files:**
  - `index.js` — Entry point
  - `routes/` — API endpoints (profile, admin, auth)
  - `models/User.js` — User schema/model
  - `package.json` — Dependencies

### Setup & Run
```bash
cd profilebackend
npm install
node index.js
```
- Runs on [http://localhost:5000](http://localhost:5000) by default.

### Features
- User registration, login, and JWT authentication
- Admin/user role management
- Secure storage and retrieval of TradingView credentials
- API endpoints for frontend and Python backend

---

## User/Admin/Auth Flow

1. **User/Admin registers and logs in** via the frontend (handled by Node.js API).
2. **Frontend** manages session with JWT and provides UI for chart interaction.
3. **User clicks a chart bar** — frontend sends trigger data (symbol, price, color, etc.) to the Python backend.
4. **Python backend**:
   - Fetches credentials from Node.js API
   - Automates TradingView: login, chart navigation, trendline drawing, and customization
   - Uses Playwright to interact with the TradingView UI as a real user would
5. **Admin dashboard** provides extra features for privileged users.

---

## Environment Variables & Configuration

- **profilebackend/.env** (example):
  - `MONGO_URI` — MongoDB connection string
  - `JWT_SECRET` — Secret for JWT tokens
- **backend/trigger_data.json** — Receives trigger data from frontend (can be replaced with API call)
- **vite-project/.env** (optional):
  - `VITE_API_URL` — URL for backend API

---

## Development & Contribution
- Use separate terminals for each service (frontend, backend, Node.js API)
- Make sure Playwright browsers are installed for Python automation
- PRs and issues welcome!

---

## License
MIT (or your preferred license) 