# Birthday Survey System (GitHub-Only)

A complete survey system with a public survey form and an admin dashboard with real-time charts. **No Firebase, no external services** — uses GitHub Issues in a private repo as the database.

## Features

- **Public Survey** (`index.html`) - 10 questions, beautiful UI, progress tracking
- **Admin Dashboard** (`admin.html`) - Statistics, charts, response table, CSV export
- **100% GitHub Native** - Stores responses as Issues in a private GitHub repo
- **No Server, No Firebase** - Runs entirely on GitHub Pages
- **Free Forever** - Uses GitHub's free tier (unlimited private repos, Issues API)

## Quick Setup

### 1. Create a Private Repo for Data
1. Go to GitHub → New Repository
2. Name: `birthday-survey-data` (or whatever you prefer)
3. **Private** ✓
4. Initialize with README ✓
5. Create repository

### 2. Create a Personal Access Token
1. GitHub Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Generate new token (classic)
3. Name: "Birthday Survey"
4. Expiration: 90 days (or longer)
5. Scopes: **`repo`** (full control of private repositories)
6. Generate → **Copy the token immediately** (you won't see it again)

### 3. Configure the Survey
Edit `index.html` - update these constants at the top of the script:
```javascript
const GITHUB_OWNER = 'YOUR_GITHUB_USERNAME';
const GITHUB_REPO = 'birthday-survey-data';  // Your private repo name
const GITHUB_LABEL = 'survey-response';       // Label for survey issues
```

### 4. Deploy to GitHub Pages
1. Push this repo to GitHub (public or private)
2. Go to Settings → Pages
3. Source: "Deploy from a branch" → Branch: `main` → Folder: `/ (root)`
4. Your survey will be at: `https://YOUR_USERNAME.github.io/REPO_NAME/`
5. Admin dashboard at: `https://YOUR_USERNAME.github.io/REPO_NAME/admin.html`

### 5. Use It
- **Guests**: Open the survey link, enter their GitHub token (or you can pre-fill it), answer questions, submit
- **Admin**: Open admin.html, enter your GitHub token in the config panel, click Refresh → see live charts!

## How It Works

| Component | Technology |
|-----------|------------|
| Survey Form | GitHub Pages (static HTML) |
| Data Storage | GitHub Issues (in private repo) |
| Admin Dashboard | GitHub Pages + GitHub Issues API |
| Charts | Chart.js (client-side) |
| Auth | Personal Access Token (stored in browser localStorage) |

## Security Notes

- **Tokens are stored in browser localStorage only** — never sent to any server except GitHub API
- **Private repo** — only people with the token can read/write
- **Token scope: `repo`** — allows reading/writing issues in private repos
- **For guests**: They need a GitHub account and token. For a birthday party, you can:
  - Pre-create a token with limited scope and share it (less secure)
  - Or have guests submit and you collect responses manually
  - Or use the "pre-filled token" approach below

## Simpler Guest Access (Optional)

If you don't want guests to create tokens, edit `index.html` and hardcode a token:

```javascript
// In index.html, replace the token input logic:
let githubToken = 'YOUR_TOKEN_HERE';  // Hardcoded token
// Remove or hide the token input field
```

Then only you (admin) need a token for the dashboard.

## Customizing Questions

Edit the `questions` array in `index.html`:

```javascript
const questions = [
    { id: 'q1', type: 'text', label: 'Your question?', required: true, placeholder: '...' },
    { id: 'q2', type: 'select', label: 'Choose one:', required: true, options: ['A', 'B', 'C'] },
    { id: 'q3', type: 'radio', label: 'Pick one:', required: true, options: ['X', 'Y', 'Z'] },
    { id: 'q4', type: 'rating', label: 'Rate 1-5:', required: true, min: 1, max: 5 },
    { id: 'q5', type: 'textarea', label: 'Long answer:', required: false, placeholder: '...' },
];
```

Then update `admin.html` - add the new field to `questionLabels` object.

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
npx serve .
# or
python -m http.server 8000
```

Open `http://localhost:8000` and `http://localhost:8000/admin.html`

## Cost

- **GitHub Pages**: Free for public repos, free for private repos on GitHub Pro/Team/Enterprise
- **GitHub Issues API**: Free (5000 requests/hour per token)
- **Total**: $0/month

## Tech Stack

- **Frontend**: Vanilla HTML/CSS/JS (no build step)
- **Charts**: Chart.js via CDN
- **Database**: GitHub Issues (via REST API)
- **Hosting**: GitHub Pages
- **Auth**: GitHub Personal Access Token (classic)

## License

MIT - Feel free to use for your birthday celebration!