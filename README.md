# Birthday Survey System

A complete survey system with a public survey form and an admin dashboard with real-time charts. Hosted free on GitHub Pages with Firebase Firestore for data storage.

## Features

- **Public Survey** (`index.html`) - 10 questions, beautiful UI, progress tracking
- **Admin Dashboard** (`admin.html`) - Real-time statistics, charts, response table
- **No Server Required** - Runs entirely on GitHub Pages + Firebase (free tier)
- **Real-time Updates** - Admin dashboard updates instantly as responses come in

## Quick Setup

### 1. Create Firebase Project
1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Create a new project (or use existing)
3. Enable **Firestore Database** → Start in **test mode** (for development)
4. Go to Project Settings → General → Your apps → Add Web App (</> icon)
5. Copy the `firebaseConfig` object

### 2. Configure Firebase
Edit both `index.html` and `admin.html`, replace the `firebaseConfig` object:

```javascript
const firebaseConfig = {
    apiKey: "YOUR_API_KEY",
    authDomain: "YOUR_PROJECT.firebaseapp.com",
    projectId: "YOUR_PROJECT_ID",
    storageBucket: "YOUR_PROJECT.appspot.com",
    messagingSenderId: "YOUR_SENDER_ID",
    appId: "YOUR_APP_ID"
};
```

### 3. Deploy to GitHub Pages
1. Push this repo to GitHub
2. Go to Settings → Pages
3. Source: "Deploy from a branch" → Branch: `main` → Folder: `/ (root)`
4. Your survey will be at: `https://YOUR_USERNAME.github.io/REPO_NAME/`
5. Admin dashboard at: `https://YOUR_USERNAME.github.io/REPO_NAME/admin.html`

### 4. Firestore Security Rules (for production)
In Firebase Console → Firestore → Rules, replace with:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /responses/{doc} {
      allow read: if true;  // Admin dashboard reads
      allow create: if true; // Survey submissions
      allow update, delete: if false;
    }
  }
}
```

## Customizing Questions

Edit the `questions` array in `index.html`:

```javascript
const questions = [
    { id: 'q1', type: 'text', label: 'Your question?', required: true, placeholder: '...' },
    { id: 'q2', type: 'select', label: 'Choose one:', required: true, options: ['A', 'B', 'C'] },
    { id: 'q3', type: 'radio', label: 'Pick one:', required: true, options: ['X', 'Y', 'Z'] },
    { id: 'q4', type: 'rating', label: 'Rate 1-5:', required: true, min: 1, max: 5 },
    { id: 'q5', type: 'textarea', label: 'Long answer:', required: false, placeholder: '...' },
    // ... add more
];
```

Then update `admin.html` to match - add the new field to the table headers and `questionLabels` object.

## Question Types

| Type | Description |
|------|-------------|
| `text` | Single-line text input |
| `email` | Email input with validation |
| `select` | Dropdown select |
| `radio` | Card-style radio buttons |
| `rating` | Star rating (1-5) |
| `textarea` | Multi-line text |

## Local Testing

```bash
# Simple HTTP server
npx serve .
# or
python -m http.server 8000
```

Then open `http://localhost:8000` and `http://localhost:8000/admin.html`

## Cost

- **GitHub Pages**: Free for public repos
- **Firebase Firestore**: Free tier includes 50K reads, 20K writes, 1 GB storage/day
- **Total**: $0/month for typical usage

## Tech Stack

- **Frontend**: Vanilla HTML/CSS/JS (no build step)
- **Charts**: Chart.js via CDN
- **Database**: Firebase Firestore (real-time)
- **Hosting**: GitHub Pages

## License

MIT - Feel free to use for your birthday celebration!