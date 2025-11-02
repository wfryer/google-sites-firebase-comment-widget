# Google Sites Comment Widget (Firebase + HTML)

A widget and commenting system that lets students and teachers interact around content on a Google Site (or any website) using Firebase. Simple, password-protected feedback for classrooms — no server required.

---

## 🎯 Project Overview

This widget lets students:
- Enter their **name**, **class section**, and **comment**
- Submit feedback stored in a **Firestore NoSQL database**
- See all comments live below the form (specific to each project)

Teachers can view and moderate all comments using the **comments.htm** dashboard.

---

## 🧰 What You’ll Need

1. A free [Google account](https://accounts.google.com/)
2. A free [Firebase](https://firebase.google.com/) account
3. The two HTML files in this project:
   - `index.htm` → for student comments  
   - `comments.htm` → for teachers to review feedback
4. Optional free hosting using **GitHub Pages**

---

## 🪜 Step-by-Step Setup

### 1️⃣ Create a Firebase Project

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click **Add project** → name it (e.g. `student-comments`)
3. Disable Google Analytics → click **Create project**

---

### 2️⃣ Add a Web App

1. Inside your Firebase project, click **</> Add app**
2. Name it (e.g. `comments-widget`) → click **Register app**
3. Click **Continue to console**
4. Under “Your apps,” copy your **Firebase config snippet** — it looks like:

```js
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT",
  storageBucket: "YOUR_PROJECT.appspot.com",
  messagingSenderId: "###########",
  appId: "APP_ID"
};
```
*(you’ll paste this later into both HTML files)*

---

### 3️⃣ Enable Firestore Database

1. In the Firebase Console, go to **Build → Firestore Database**
2. Click **Create database**
3. Choose **Start in test mode** (safe for classroom projects)
4. Click **Next** and accept the default region
5. Wait for Firestore to initialize  

You’ll now see an empty database with a “Start collection” button.

---

### 4️⃣ Set Firestore Rules (for testing)

Click the **Rules** tab and set the following for testing:

```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /comments/{document=**} {
      allow read, write: if true;
    }
  }
}
```

Click **Publish.**  
⚠️ This allows open read/write access (fine for classroom demos, not production).  
You can later restrict with passwords or authentication if desired.

---

### 5️⃣ Add Firebase Config to the Code

Open `index.htm` and `comments.htm` in a text editor (like VS Code).  
Find this section:

```js
// Replace with your own Firebase config
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT",
  storageBucket: "YOUR_PROJECT.appspot.com",
  messagingSenderId: "###########",
  appId: "APP_ID"
};
```

Replace those placeholder values with your Firebase project’s real config.

---

### 6️⃣ Customize Passwords

Inside both files you’ll see:

```js
if (password !== "CLASS_PASSWORD_HERE")
```

and

```js
if (confirmPwd !== "ADMIN_PASSWORD_HERE")
```

Replace these with your own class and admin passwords.  
They aren’t stored anywhere — they’re just checked in the browser before posting or deleting comments.

---

### 7️⃣ Host the Files

#### Option A — GitHub Pages (Free Hosting)

1. Create a [GitHub account](https://github.com/)
2. Create a new public repository named `google-sites-firebase-comment-widget`
3. Upload `index.htm` and `comments.htm`
4. In **Settings → Pages**, set the source to “Deploy from branch: main → /(root)”
5. After saving, GitHub Pages gives you a live URL such as:

```
https://yourusername.github.io/google-sites-firebase-comment-widget/
```

Your widget URLs will then be:

- Student page:  
  `https://yourusername.github.io/google-sites-firebase-comment-widget/index.htm?projectId=example1`
- Teacher page:  
  `https://yourusername.github.io/google-sites-firebase-comment-widget/comments.htm`

#### Option B — Other Hosting

You can also upload these files to your school website, cPanel hosting, or VPS server — any host that serves HTML will work.

---

### 8️⃣ Embed in Google Sites

In Google Sites:

1. Choose **Insert → Embed → Embed Code**
2. Paste this code (update your GitHub URL):

```html
<iframe src="https://yourusername.github.io/google-sites-firebase-comment-widget/index.htm?projectId=bravery-quote1"
width="100%" height="800" style="border:none;"></iframe>
```

✅ Each project page can use a different `projectId` (like `bravery-quote2`, `lesson3`, etc.).  
Comments stay organized by ID in Firestore.

---

## 👀 Teacher Dashboard

Visit your hosted `comments.htm` page to see all comments grouped by project name.  
Admins can delete comments after entering the admin password.

---

## 🧠 Tips and Troubleshooting

- If “Submit Feedback” does nothing, open your browser **Console** (`Right-click → Inspect → Console`) for errors.  
- Make sure your **Firestore Rules** allow writing.  
- Refresh the page after adding a comment to see updates.  
- Always test one project first before embedding multiple pages.

---

## 🧩 Credit and Collaboration

This project was created by [**Wes Fryer**](https://github.com/wfryer).  
You can explore more of his work and blog posts about AI and teaching at [ai.wesfryer.com](https://ai.wesfryer.com).

This script was developed in a **“vibe-coding” collaboration** with **ChatGPT-5** and **Google’s Gemini**, combining step-by-step debugging, documentation, and design guidance.

---

## ⚖️ License

This project is licensed under the **MIT License**.  
You are free to use, modify, and share this code for any purpose with attribution.
