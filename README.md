# ThanhAnn Info Page 🎨

A beautiful, interactive personal profile page with music player, achievements, leaderboard, and more!

## 🚨 Security Setup (IMPORTANT!)

### Firebase API Keys - REMOVED ✅
Firebase credentials were previously committed publicly. They have been removed and replaced with environment variables.

**Action Required:**
1. **Reset your Firebase API Key immediately:**
   - Go to [Firebase Console](https://console.firebase.google.com/)
   - Select your project `website-1c7a3`
   - Navigate to Settings → Service Accounts → API Keys
   - Delete the old key and create a new one

2. **Setup Environment Variables:**
   ```bash
   # Copy the template file
   cp .env.example .env.local
   
   # Edit .env.local and add your Firebase credentials:
   VITE_FIREBASE_API_KEY=your_new_api_key_here
   VITE_FIREBASE_AUTH_DOMAIN=website-1c7a3.firebaseapp.com
   VITE_FIREBASE_PROJECT_ID=website-1c7a3
   VITE_FIREBASE_STORAGE_BUCKET=website-1c7a3.firebasestorage.app
   VITE_FIREBASE_MESSAGING_SENDER_ID=504656783081
   VITE_FIREBASE_APP_ID=1:504656783081:web:dc793f9c9f9a8829fd3278
   ```

3. **Update your HTML loader** to use environment variables:
   - Modify the Firebase initialization script in `index.html` to load from `.env.local`
   - Example using Vite:
   ```javascript
   const firebaseConfig = {
     apiKey: import.meta.env.VITE_FIREBASE_API_KEY,
     authDomain: import.meta.env.VITE_FIREBASE_AUTH_DOMAIN,
     // ... etc
   };
   ```

## 🔧 Setup Instructions

### Prerequisites
- Node.js 16+ (if using a build tool)
- Firebase project setup
- Modern web browser

### Installation

```bash
# Clone the repository
git clone https://github.com/Eriolzz/info.git
cd info

# Install dependencies (if using npm/yarn)
npm install
# or
yarn install

# Create environment variables
cp .env.example .env.local

# Fill in your Firebase credentials in .env.local
```

### Running Locally

**Option 1: Direct (No Build Tool)**
- Simply open `index.html` in your browser
- Note: Firebase config will need to be manually updated

**Option 2: With Vite (Recommended)**
```bash
npm run dev
```

## 📁 Project Structure

```
info/
├── index.html              # Main page (contains all CSS & HTML)
├── data/
│   ├── config.json        # Firebase config (uses env vars)
│   ├── achievements.json  # Achievement definitions
│   ├── fortunes.json      # Fortune messages
│   ├── phrases.json       # Random phrases
│   └── playlist.json      # Music playlist
├── .env.example           # Environment variables template
└── .gitignore            # Git ignore rules
```

## ✨ Features

- 🎨 **Dark Theme with Accent Colors** - Customizable color scheme
- 🎵 **Music Player** - Play songs from playlist with controls
- 🎮 **Snake Game** - Interactive game with scoring
- 🎴 **Fortune Cards** - Random fortune messages
- ⭐ **Achievements** - Unlock badges by interacting with the page
- 🏆 **Leaderboard** - Real-time ranking synced with Firebase
- 📝 **Guestbook** - Visitor messages stored in Firestore
- 🎯 **Easter Eggs** - Hidden surprises to discover

## 🛡️ Data Security

- ✅ No sensitive data in Git
- ✅ Firebase keys in `.env.local` (not committed)
- ✅ `.gitignore` protects environment files
- ⚠️ Always sanitize user input from Firestore
- ⚠️ Setup Firestore security rules in Firebase Console

### Recommended Firestore Rules

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /leaderboard/{document=**} {
      allow read;
      allow write: if request.auth != null;
    }
    match /guestbook/{document=**} {
      allow read;
      allow create: if request.auth != null;
    }
  }
}
```

## 🚀 Deployment

### Deploy to GitHub Pages
```bash
# Push to main branch
git add .
git commit -m "Update site"
git push origin main
```

### Deploy to Vercel / Netlify
1. Connect your GitHub repo
2. Add environment variables in the hosting dashboard
3. Deploy automatically on push

## 📝 Customization

### Change Accent Color
Edit the CSS variables in `index.html`:
```css
:root {
  --accent: #6366f1;      /* Change to your color */
  --accent-2: #818cf8;
  --accent-rgb: 99,102,241;
}
```

### Add More Songs
Edit `data/playlist.json`:
```json
{
  "title": "Song Title",
  "artist": "Artist Name",
  "cover": "https://your-image-url.jpg",
  "audio": "https://your-audio-url.mp3"
}
```

### Add Achievements
Edit `data/achievements.json`:
```json
{
  "your_key": {
    "icon": "🎯",
    "title": "Achievement Name",
    "desc": "Description"
  }
}
```

## 🐛 Common Issues

**Issue: Firebase config not loading**
- ✅ Solution: Check `.env.local` exists and has correct values
- ✅ Check browser console for errors

**Issue: CSS looks broken**
- ✅ Hard refresh browser (Ctrl+Shift+R or Cmd+Shift+R)
- ✅ Clear browser cache

**Issue: Music won't play**
- ✅ Check audio URLs are accessible
- ✅ Check browser console for CORS errors
- ✅ Verify playlist.json is valid JSON

## 📄 License

Personal project - feel free to fork and customize!

## ⚠️ Security Checklist

Before deploying:
- [ ] Firebase API keys in `.env.local`, NOT in code
- [ ] `.gitignore` includes `.env.local`
- [ ] Old API keys are deleted from Firebase Console
- [ ] Firestore security rules are configured
- [ ] No console logs exposing sensitive data
- [ ] Input validation for user-generated content

---

**Last Updated:** July 2026  
**Status:** ✅ Security issues fixed - Ready to deploy
