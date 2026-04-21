# 🧳 TripNest — Smart Travel Planner

> A full-featured, Firebase-powered travel planning web app built with React + Vite + Tailwind CSS. Plan trips, manage itineraries, track budgets, organize packing lists, and store travel documents — all in one place.

**Live Demo:** [VeerdhawalYadav12.github.io/TripNest_SmartTravelPlanner](https://VeerdhawalYadav12.github.io/TripNest_SmartTravelPlanner)

---

## ✨ Features

- **Dashboard** — Overview of all trips with search, status filters (upcoming / ongoing / completed), and at-a-glance stats (total trips, days traveled, budget totals)
- **Itinerary Planner** — Day-by-day activity scheduling per trip
- **Budget Tracker** — Log expenses by category with real-time totals and per-category breakdowns
- **Packing List** — Manage packing checklists with packed/unpacked status
- **Documents Vault** — Store and reference travel documents (passport, visa, bookings, etc.)
- **Authentication** — Email/password signup & login, plus Google Sign-In via Firebase Auth
- **Protected Routes** — All planner pages require authentication
- **Persistent Storage** — All data stored in Cloud Firestore per user, per trip

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Framework | React 18 + Vite 5 |
| Routing | React Router DOM v6 (HashRouter for GitHub Pages) |
| Styling | Tailwind CSS v3 |
| Backend / DB | Firebase v10 (Auth + Firestore) |
| Notifications | react-hot-toast |
| Icons | lucide-react |
| Date utilities | date-fns |
| Deployment | GitHub Pages via `gh-pages` / GitHub Actions |

---

## 📁 Project Structure

```
src/
├── App.jsx                   # Root component — routing & providers
├── main.jsx                  # Entry point
├── index.css                 # Global styles
│
├── context/
│   ├── AuthContext.jsx        # Auth state (user, login, signup, Google login, logout)
│   └── TripContext.jsx        # Active trip selection across pages
│
├── hooks/
│   ├── useTrips.js            # CRUD for trips
│   ├── useItinerary.js        # CRUD for itinerary items
│   ├── useBudget.js           # CRUD + stats for budget items
│   ├── usePacking.js          # CRUD for packing list items
│   └── useDocuments.js        # CRUD for travel documents
│
├── pages/
│   ├── LoginPage.jsx
│   ├── SignupPage.jsx
│   ├── DashboardPage.jsx
│   ├── ItineraryPage.jsx
│   ├── BudgetPage.jsx
│   ├── PackingPage.jsx
│   └── DocumentsPage.jsx
│
├── components/
│   ├── auth/
│   │   └── ProtectedRoute.jsx
│   ├── layout/
│   │   ├── AppLayout.jsx
│   │   └── Sidebar.jsx
│   ├── dashboard/
│   │   ├── TripCard.jsx
│   │   └── TripForm.jsx
│   └── ui/
│       └── index.jsx          # Shared UI components (Button, Spinner, EmptyState, etc.)
│
├── services/
│   ├── firebase.js            # Firebase app init, auth & db exports
│   └── firestoreService.js    # All Firestore CRUD operations
│
└── utils/
    └── helpers.js             # Date formatting, trip duration helpers
```

---

## 🚀 Getting Started

### Prerequisites

- Node.js 18+
- A [Firebase](https://firebase.google.com/) project with **Authentication** and **Firestore** enabled

### 1. Clone the repository

```bash
git clone https://github.com/VeerdhawalYadav12/TripNest_SmartTravelPlanner.git
cd TripNest_SmartTravelPlanner
```

### 2. Install dependencies

```bash
npm install
```

### 3. Set up Firebase

1. Go to the [Firebase Console](https://console.firebase.google.com/) and create a new project.
2. Enable **Authentication** → Sign-in methods: **Email/Password** and **Google**.
3. Enable **Firestore Database** (start in test mode for development).
4. From Project Settings → Your apps → Web app, copy your Firebase config.

### 4. Configure environment variables

Create a `.env` file in the project root:

```env
VITE_FIREBASE_API_KEY=your_api_key
VITE_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
VITE_FIREBASE_PROJECT_ID=your_project_id
VITE_FIREBASE_STORAGE_BUCKET=your_project.firebasestorage.app
VITE_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
VITE_FIREBASE_APP_ID=your_app_id
```

> ⚠️ Never commit your `.env` file. It is already listed in `.gitignore`.

### 5. Run the development server

```bash
npm run dev
```

The app will be available at `http://localhost:5173`.

---

## 🏗️ Available Scripts

| Command | Description |
|---|---|
| `npm run dev` | Start local development server |
| `npm run build` | Build for production (outputs to `/dist`) |
| `npm run preview` | Preview the production build locally |
| `npm run lint` | Run ESLint across all JS/JSX files |
| `npm run deploy` | Deploy to GitHub Pages via `gh-pages` |

---

## ☁️ Deployment

### GitHub Pages (manual)

```bash
npm run build
npm run deploy
```

This builds the app and pushes the `/dist` folder to the `gh-pages` branch.

### GitHub Actions (automatic)

A workflow at `.github/workflows/deploy.yml` automatically builds and deploys to GitHub Pages on every push to `main`. No extra configuration is needed — just ensure GitHub Pages is set to deploy from **GitHub Actions** in your repository settings.

---

## 🗄️ Firestore Data Model

All data is scoped to the authenticated user.

```
trips (collection)
└── {tripId}
    ├── userId
    ├── name
    ├── destination
    ├── startDate
    ├── endDate
    ├── budget
    ├── createdAt
    ├── updatedAt
    │
    ├── itinerary (subcollection)
    │   └── {itemId} — { day, time, activity, notes, createdAt }
    │
    ├── budget (subcollection)
    │   └── {itemId} — { category, description, amount, createdAt }
    │
    ├── packing (subcollection)
    │   └── {itemId} — { name, category, packed, createdAt }
    │
    └── documents (subcollection)
        └── {docId} — { type, name, number, expiryDate, notes, createdAt }
```

---

## 🔐 Authentication Flow

- Users sign up with **email + password** or **Google OAuth**.
- Firebase Auth manages sessions; the `AuthContext` exposes `user`, `login`, `signup`, `loginWithGoogle`, and `logout`.
- All routes under `AppLayout` are wrapped with `ProtectedRoute`, which redirects unauthenticated users to `/login`.

---

## 🤝 Contributing

Contributions are welcome! Please open an issue first to discuss any significant change.

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/my-feature`
3. Commit your changes: `git commit -m "feat: add my feature"`
4. Push to the branch: `git push origin feature/my-feature`
5. Open a Pull Request

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).

---

<p align="center">Made with ❤️ by <a href="https://github.com/VeerdhawalYadav12">Veerdhawal Yadav</a></p>
