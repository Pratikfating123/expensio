# 💰 Expensio — Full-Stack Daily Expense Tracker

A beautiful, full-featured expense tracking application built with React, Node.js, Express, and MongoDB.

---

## 🖼️ Features

- **Authentication** — JWT-based login/signup with bcrypt password hashing
- **Expense CRUD** — Add, edit, delete with categories, notes, and dates
- **8 Categories** — Food, Travel, Bills, Shopping, Entertainment, Health, Education, Others
- **Smart Dashboard** — Today/Monthly/All-time stats with budget alerts
- **3 Chart Types** — Pie (categories), Bar (monthly), Line (daily trends)
- **Budget Tracking** — Set monthly limits with color-coded alerts (warning at 80%, danger at 100%)
- **Search & Filter** — Filter by category, date range, keyword search
- **Export CSV** — Download your expense data any time
- **Dark Mode** — Full dark/light mode toggle, persisted per user
- **Glassmorphism UI** — Soft modern design with Framer Motion animations
- **Mobile Responsive** — Collapsible sidebar, touch-friendly
- **Quick Add FAB** — Floating button available on every page

---

## 🗂️ Project Structure

```
expense-tracker/
├── backend/
│   ├── config/
│   │   └── db.js                 # MongoDB connection
│   ├── controllers/
│   │   ├── authController.js     # signup, login, profile
│   │   ├── expenseController.js  # CRUD + filtering
│   │   ├── analyticsController.js# charts, summary, export
│   │   └── budgetController.js   # budget get/set
│   ├── middleware/
│   │   └── auth.js               # JWT protect middleware
│   ├── models/
│   │   ├── User.js               # User schema
│   │   ├── Expense.js            # Expense schema
│   │   └── Budget.js             # Budget schema
│   ├── routes/
│   │   ├── auth.js
│   │   ├── expenses.js
│   │   ├── analytics.js
│   │   └── budget.js
│   ├── server.js                 # Express app entry
│   ├── seed.js                   # Sample data seeder
│   ├── .env.example
│   └── package.json
│
└── frontend/
    ├── public/
    │   └── index.html
    ├── src/
    │   ├── components/
    │   │   ├── analytics/
    │   │   │   └── Charts.jsx    # Chart.js wrappers (Pie, Bar, Line)
    │   │   ├── dashboard/
    │   │   │   ├── SummaryCards.jsx
    │   │   │   └── BudgetProgress.jsx
    │   │   ├── expenses/
    │   │   │   ├── ExpenseModal.jsx
    │   │   │   ├── ExpenseRow.jsx
    │   │   │   └── ExpenseFilters.jsx
    │   │   └── shared/
    │   │       ├── AppLayout.jsx
    │   │       ├── Sidebar.jsx
    │   │       ├── TopBar.jsx
    │   │       ├── DarkModeToggle.jsx
    │   │       ├── QuickAddButton.jsx
    │   │       └── Skeleton.jsx
    │   ├── context/
    │   │   ├── AuthContext.jsx
    │   │   └── ExpenseContext.jsx
    │   ├── pages/
    │   │   ├── LandingPage.jsx
    │   │   ├── LoginPage.jsx
    │   │   ├── SignupPage.jsx
    │   │   ├── DashboardPage.jsx
    │   │   ├── ExpensesPage.jsx
    │   │   ├── AnalyticsPage.jsx
    │   │   └── ProfilePage.jsx
    │   ├── utils/
    │   │   ├── api.js            # Axios instance with JWT interceptors
    │   │   └── helpers.js        # formatCurrency, categories, export
    │   ├── App.jsx               # Routes + providers
    │   ├── index.js
    │   └── index.css             # Tailwind + custom CSS variables
    ├── tailwind.config.js
    ├── postcss.config.js
    └── package.json
```

---

## 🚀 Setup Instructions

### Prerequisites
- Node.js v18+
- MongoDB (local or [MongoDB Atlas](https://cloud.mongodb.com))
- npm or yarn

---

### 1. Clone / Download & Install

```bash
# Backend
cd expense-tracker/backend
npm install

# Frontend
cd ../frontend
npm install
```

---

### 2. Configure Backend

```bash
cd backend
cp .env.example .env
```

Edit `.env`:
```env
PORT=5000
MONGODB_URI=mongodb://localhost:27017/expense_tracker
JWT_SECRET=your_super_secret_key_here_change_me
JWT_EXPIRE=7d
NODE_ENV=development
CLIENT_URL=http://localhost:3000
```

> **MongoDB Atlas**: Replace `MONGODB_URI` with your Atlas connection string.

---

### 3. Seed Sample Data (Optional)

```bash
cd backend
npm run seed
```

This creates:
- Demo user: `demo@example.com` / `demo123`
- ~3 months of realistic expense data across all categories

---

### 4. Start Backend

```bash
cd backend
npm run dev       # Development (with nodemon)
# or
npm start         # Production
```

Backend runs at: `http://localhost:5000`

---

### 5. Start Frontend

```bash
cd frontend
npm start
```

Frontend runs at: `http://localhost:3000`

---

## 🌐 API Endpoints

### Auth
| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/auth/signup` | Register new user |
| POST | `/api/auth/login` | Login user |
| GET | `/api/auth/me` | Get current user |
| PUT | `/api/auth/profile` | Update profile |
| PUT | `/api/auth/password` | Change password |

### Expenses
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/expenses` | List expenses (with filters) |
| POST | `/api/expenses` | Create expense |
| PUT | `/api/expenses/:id` | Update expense |
| DELETE | `/api/expenses/:id` | Delete expense |

**Query params for GET `/api/expenses`:**
- `page`, `limit` — pagination
- `category` — filter by category
- `startDate`, `endDate` — date range (ISO strings)
- `search` — search in notes
- `sortBy`, `sortOrder` — sorting

### Analytics
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/analytics/summary` | Dashboard summary |
| GET | `/api/analytics/monthly?year=2024` | Monthly totals |
| GET | `/api/analytics/daily?month=1&year=2024` | Daily totals |
| GET | `/api/analytics/export?format=csv` | Export CSV |

### Budget
| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/budget?month=0&year=2024` | Get budget |
| POST | `/api/budget` | Set budget |

---

## 🎨 Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 18, React Router v6 |
| Styling | Tailwind CSS, CSS Variables |
| Animation | Framer Motion |
| Charts | Chart.js + react-chartjs-2 |
| Icons | Lucide React |
| HTTP | Axios |
| Backend | Node.js, Express.js |
| Database | MongoDB + Mongoose |
| Auth | JWT + bcryptjs |
| Notifications | react-hot-toast |

---

## 🔐 Security Notes

- Passwords are hashed with bcrypt (salt rounds: 10)
- JWT tokens expire after 7 days
- All expense routes are protected with auth middleware
- Users can only access their own data
- Change `JWT_SECRET` in production to a long random string

---

## 📱 Usage Tips

- **Quick Add**: Use the floating `+` button (bottom-right) on any page
- **Dark Mode**: Toggle in the sidebar bottom or Profile page
- **Budget Alert**: Set your monthly budget in Profile → appears in top bar
- **Export**: Expenses page → "Export CSV" button
- **Date Filter**: Use the date range pickers in Expenses page filters

---

## 🏗️ Production Deployment

### Backend (e.g., Railway, Render, Heroku)
1. Set environment variables in your hosting provider
2. Set `NODE_ENV=production`
3. Set `MONGODB_URI` to your Atlas URI
4. Set `CLIENT_URL` to your frontend domain

### Frontend (e.g., Vercel, Netlify)
1. Set `REACT_APP_API_URL=https://your-backend-url/api`
2. Build: `npm run build`
3. Deploy the `build/` folder

---

