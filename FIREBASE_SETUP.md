# 🔗 Firebase Setup for Shared Canvas Feature

## Quick Setup (5 minutes)

### Step 1: Create Firebase Project
1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click "Add Project"
3. Name it (e.g., "memory-diary")
4. Disable Google Analytics (optional)
5. Click "Create Project"

### Step 2: Enable Realtime Database
1. In your project, go to **Build** → **Realtime Database**
2. Click "Create Database"
3. Choose location (closest to you)
4. Start in **Test Mode** (for development)
   ```
   {
     "rules": {
       ".read": true,
       ".write": true
     }
   }
   ```
   ⚠️ **Note:** For production, set proper security rules!

### Step 3: Get Your Config
1. Go to **Project Settings** (gear icon)
2. Scroll to "Your apps" section
3. Click the **Web** icon (`</>`)
4. Register app (name it anything)
5. Copy the `firebaseConfig` object

### Step 4: Add Config to Your Code
1. Open `toolbar.html`
2. Find line ~1695 (search for "YOUR_API_KEY_HERE")
3. Replace the placeholder config with your actual config:

```javascript
const firebaseConfig = {
    apiKey: "AIzaSyXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
    authDomain: "your-project.firebaseapp.com",
    databaseURL: "https://your-project-default-rtdb.firebaseio.com",
    projectId: "your-project",
    storageBucket: "your-project.appspot.com",
    messagingSenderId: "123456789012",
    appId: "1:123456789012:web:abcdef123456"
};
```

### Step 5: Test Locally
1. Open `toolbar.html` in your browser
2. Click "🔗 share canvas"
3. Click "✨ create new shared canvas"
4. You should see a room code!

## How to Use

### Creating a Shared Canvas
1. Click "🔗 share canvas" button
2. Click "✨ create new shared canvas"
3. **Copy the shareable link** - it looks like: `https://your-site.com?room=A3X9K2`
4. **Send the link to friends** via text, email, Discord, etc.
5. When they click it, they'll automatically join your canvas!
6. Take photos - everyone sees them in real-time!

### Joining a Friend's Canvas
**Method 1: Click their link** (Easiest!)
- Friend sends you a link like `https://your-site.com?room=A3X9K2`
- Click it - you're instantly in their canvas!

**Method 2: Enter room code manually**
1. Get the room code from your friend (e.g., "A3X9K2")
2. Click "🔗 share canvas"
3. Enter the code
4. Click "🚪 join friend's canvas"

### Features
✨ **View & Edit Together**: Everyone can add photos and decorations
📸 **Real-time Updates**: See changes instantly
🔗 **Simple Sharing**: Just send a link - no accounts needed
💾 **Persistent Rooms**: Canvas stays active as long as someone is using it
👥 **Unlimited Friends**: Share with as many people as you want

### Leaving a Shared Canvas
1. Click "🔗 share canvas"
2. Click "🚪 leave shared canvas"
3. You're back to your private canvas

## Deploy to Vercel

### Option 1: Using Vercel CLI
```bash
npm install -g vercel
cd /Users/vynnie/Desktop/projects/2
vercel
```

### Option 2: Using Vercel Dashboard
1. Go to [vercel.com](https://vercel.com)
2. Sign up/Login
3. Click "Add New" → "Project"
4. Import your Git repository (or drag & drop folder)
5. Deploy!

Your app will be live at: `https://your-project.vercel.app`

## Security (Important for Production!)

Before sharing publicly, update Firebase rules:

```json
{
  "rules": {
    "rooms": {
      "$roomId": {
        ".read": true,
        ".write": true,
        ".validate": "newData.hasChildren(['createdAt', 'polaroids'])",
        "polaroids": {
          "$polaroidId": {
            ".validate": "newData.hasChildren(['imageUrl', 'x', 'y', 'rotation', 'timestamp'])"
          }
        }
      }
    }
  }
}
```

## Troubleshooting

**"Firebase not configured" error:**
- Make sure you replaced ALL placeholder values in `firebaseConfig`
- Check browser console for specific errors

**Room not found:**
- Double-check the room code (case-sensitive)
- Make sure Firebase Realtime Database is enabled

**Photos not syncing:**
- Check your internet connection
- Verify Firebase rules allow read/write
- Open browser console to see any errors

## Features

✅ Create shared canvas rooms
✅ Join with simple 6-character codes
✅ Real-time photo sharing
✅ Works with your existing diary feature
✅ Leave/rejoin anytime
✅ Copy room code to share

## Notes

- Each room can have unlimited photos
- Photos are stored as base64 in Firebase
- Free tier: 1GB storage, 10GB/month bandwidth
- For heavy use, consider Firebase paid plan
- Room codes are permanent until you delete them

## Support

If you need help:
1. Check browser console for errors
2. Verify Firebase config is correct
3. Make sure Realtime Database is enabled
4. Test with a friend on same network first

