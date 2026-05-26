# SCG Mentorship Platform — Complete Guide

## What's included

### Features
- ✅ Email/password login (mentees get invited by admin)
- ✅ Role-based routing (admin → admin panel, mentee → dashboard)  
- ✅ Mentee dashboard with progress overview
- ✅ Assignment submissions: file upload, image, LinkedIn link, text response
- ✅ LinkedIn engagement assignments (post + like/comment/repost matrix)
- ✅ Admin dashboard with stats, tabs (assignments/members/submissions)
- ✅ Admin assignment detail view with all submissions
- ✅ Feedback system (admin comments on submissions)
- ✅ Close/reopen assignments (only admin)
- ✅ Bulk member upload (paste CSV of names and emails)
- ✅ Export assignment reports
- ✅ PWA ready (install to home screen)
- ✅ Mobile responsive

### File structure
```
scg-platform/
├── index.html          ← The entire app (SPA)
├── css/app.css          ← Stylesheet
├── sw.js                ← Service worker (PWA)
├── manifest.json        ← PWA manifest
├── firebase.json        ← Firebase Hosting config
├── firestore.rules      ← Security rules
├── .firebaserc          ← Firebase project link
├── icons/
│   ├── icon-192.png     ← App icon 192px
│   └── icon-512.png     ← App icon 512px
└── SETUP.md             ← This file
```

---

## Deployment Steps

### 1. Enable Firestore Database
1. Go to https://console.firebase.google.com
2. Open project: **sgc-checkin-2d966**
3. Left sidebar → **Firestore Database** → **Create database**
4. Start in **test mode**
5. Region: **europe-west1**

### 2. Enable Firebase Storage
1. Left sidebar → **Storage** → **Get started**
2. Start in **test mode**
3. Same region

### 3. Deploy Firestore Rules
The `firestore.rules` file is included. Deploy via CLI (step 5) or paste manually:
- Go to Firestore → **Rules** tab → paste contents of `firestore.rules` → Publish

### 4. Add yourself as the first admin
In Firebase Console → Firestore → **Start collection** → Collection ID: `members`

Add a document with these fields:
| Field     | Type    | Value              |
|-----------|---------|--------------------|
| name      | string  | Your Full Name     |
| email     | string  | you@example.com    |
| role      | string  | admin              |
| activated | boolean | false              |
| uid       | string  | (leave empty)      |

### 5. Add mentee emails
Same collection (`members`), add one document per mentee:
| Field     | Type    | Value              |
|-----------|---------|--------------------|
| name      | string  | Mentee Name        |
| email     | string  | mentee@example.com |
| role      | string  | mentee             |
| activated | boolean | false              |
| uid       | string  | (leave empty)      |

Or use the **Bulk Upload** feature in the admin panel after your first login.

### 6. Deploy to Firebase Hosting
```bash
# Install Firebase CLI if you haven't
npm install -g firebase-tools

# Login
firebase login

# Deploy (from this project folder)
firebase deploy
```

Your site will be live at: `https://sgc-checkin-2d966.web.app`

### Alternative: Deploy to Vercel
1. Push this folder to a GitHub repo
2. Go to vercel.com → Import Project → select the repo
3. Framework: Other
4. Output directory: . (root)
5. Deploy

---

## First Login

1. Visit your deployed site
2. Click **"First time?"** tab
3. Enter the admin email you added to Firestore
4. Create a password (min 6 characters)
5. You'll be redirected to the **Admin Panel**

### Then add mentees:
- Go to **Members** tab → **+ Add** (one by one)
- Or click **Bulk upload emails** → paste lines like:
  ```
  Akosua Mensah, akosua@example.com
  Kofi Owusu, kofi@example.com
  ```

### Then create assignments:
- Go to **Assignments** tab → **+ New**
- Fill in title, deadline, and check the submission types
- For LinkedIn engagement assignments, check **"LinkedIn engagement"**

---

## How it works

### For mentees:
1. They visit the site and enter their pre-registered email
2. Create a password → they're in
3. They see their assignments with progress
4. They tap an assignment → submit files, links, or text
5. For engagement assignments: post their link first, then engage with others
6. They see admin feedback on reviewed submissions

### For admin:
1. Same login page, auto-redirected to admin panel
2. Create assignments with any combination of submission types
3. View all submissions, download files, click LinkedIn links
4. Leave feedback on each submission
5. See the engagement matrix for LinkedIn engagement assignments
6. Close/reopen assignments
7. Export reports

---

## Still TODO (future enhancements)
- [ ] Push notifications via Firebase Cloud Messaging
- [ ] Email notifications via Cloud Functions
- [ ] Admin can set custom notification schedules
- [ ] Analytics dashboard (submission trends over time)
- [ ] Leaderboard for mentees
