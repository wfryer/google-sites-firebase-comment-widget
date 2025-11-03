# 🧩 Google Sites Firebase Comment Widget (Secure Template Version)

This project provides a **simple, secure, and teacher-friendly commenting system** that connects static HTML pages (such as Google Sites embeds) to a **Firebase Firestore database**.  
It allows students, participants, or community members to post comments — and teachers or moderators to view and delete them — **without running any backend code**.

---

## 🎯 Overview

- **index.htm** → Public comment form (for embedding on a class or project page)  
- **comments.htm** → Teacher/moderator dashboard with secure deletion controls  
- **Firestore Rules** enforce password security server‑side (no visible credentials in the HTML)  
- **GitHub Pages** hosting supported — no special server setup required  

This system was designed and field‑tested by [**Wes Fryer**](https://ai.wesfryer.com) and is ideal for teachers exploring “vibe coding” and AI‑assisted development.

---

## 🧠 Features

| Role | Page | Description |
|------|------|--------------|
| Student / Participant | `index.htm` | Submit name, location/section, and a password‑protected comment stored in Firestore |
| Teacher / Admin | `comments.htm` | View all comments, grouped by projectId, and securely delete inappropriate or duplicate comments |
| Firebase | Rules | Validates passwords on the server — keeping credentials out of public code |

---

## 🚀 Quick Start Setup

### 1️⃣ Create a Firebase Project
1. Go to [Firebase Console](https://console.firebase.google.com/) and create a new project.  
2. Click **Add App → Web App** and choose a name (e.g. `myclass-comments`).  
3. When asked to “Add Firebase SDK,” select **Use a `<script>` tag**, not npm.  
4. Copy your **Firebase Config** — it looks like this:

```js
const firebaseConfig = {
  apiKey: "AIza...",
  authDomain: "myclass-comments.firebaseapp.com",
  projectId: "myclass-comments",
  storageBucket: "myclass-comments.appspot.com",
  messagingSenderId: "1234567890",
  appId: "1:1234567890:web:abcdefgh12345"
};
```

You’ll paste that into both HTML files later.

---

### 2️⃣ Enable Firestore Database
1. In the Firebase Console, go to **Build → Firestore Database → Create Database**.  
2. Choose **Start in Production Mode** (recommended).  
3. Accept the default region and click **Enable**.  

---

### 3️⃣ Set Firestore Rules (Secure Version)

Paste the following in your **Firestore → Rules** editor:

```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /comments/{document=**} {
      allow read: if true;
      allow write: if request.resource.data.accessCode == "CLASS_PASSWORD";
      allow update: if request.resource.data.accessCode == "ADMIN_PASSWORD";
      allow delete: if resource.data.markedForDeletion == true && request.auth == null;
    }
  }
}
```

Replace `"CLASS_PASSWORD"` and `"ADMIN_PASSWORD"` with your chosen values (for example: `"easter"` and `"easteradmin"`).

Then click **Publish**.

---

### ✏️ 3.5 Add Your Firebase Config to Both HTML Files

After publishing your rules, open both **`index.htm`** and **`comments.htm`** in a text editor (VS Code, Notepad++, etc.)  
and find this line:

```js
const firebaseConfig = YOUR_FIREBASE_CONFIG_HERE;
```

Replace it with your Firebase config object from **Project Settings → Web App**, for example:

```js
const firebaseConfig = {
  apiKey: "AIzaSy...yourKey...",
  authDomain: "yourproject.firebaseapp.com",
  projectId: "yourproject",
  storageBucket: "yourproject.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abcd1234"
};
```

⚠️ You must paste this config in **both** `index.htm` and `comments.htm` before uploading them to GitHub Pages.

---

### 4️⃣ Host on GitHub Pages (Free)

1. Create a new GitHub repository — for example:  
   `google-sites-firebase-comment-widget`
2. Upload both HTML files (`index.htm` and `comments.htm`).  
3. In **Settings → Pages**, set:
   - **Source:** Deploy from branch  
   - **Branch:** main  
   - **Folder:** /(root)  
4. Save. GitHub will show a green banner with your site URL.

Example URLs:
```
https://yourusername.github.io/google-sites-firebase-comment-widget/index.htm?projectId=example1
https://yourusername.github.io/google-sites-firebase-comment-widget/comments.htm
```

---

### 5️⃣ Embed in Google Sites (or any webpage)

Use an `<iframe>` block like this:

```html
<iframe
  src="https://yourusername.github.io/google-sites-firebase-comment-widget/index.htm?projectId=01"
  width="100%"
  height="800"
  style="border:none;"
  title="Class Comments">
</iframe>
```

Each unique `projectId` creates a separate comment thread.

---

## 🧩 Folder Structure Example

```
/
├── index.htm               # Public comment form
├── comments.htm            # Secure teacher dashboard
├── examples/
│   └── aceclass-02nov2025/ # Example project from live class demo
└── README.md
```

---

## 🧑‍🏫 Live Classroom Example

**ACE Class Comments on Book Quotations (Nov 2, 2025)**  
Deployed via GitHub Pages for this lesson (A Google Sites website - HTML pages hosted via GitHub pages:  
[https://followjesus.wesfryer.com/classes/2022-present-ace-sunday-school/budde-chapter1](https://followjesus.wesfryer.com/classes/2022-present-ace-sunday-school/budde-chapter1)

---

## 🧠 Troubleshooting

| Issue | Likely Cause | Solution |
|-------|---------------|----------|
| “Submit Feedback” doesn’t work | Firestore Rules not published | Double‑check you saved and published your rules |
| Comments don’t appear | Wrong projectId | Ensure the `?projectId=` value matches your test comments |
| Delete button fails | Rules not updated for secure delete | Copy the latest rules block from this README |

---

## ⚖️ License

This project is licensed under the **MIT License**.  
You may freely use, modify, and share it for educational or personal projects.

---

## 🙌 Credit and Collaboration

This project was created by **[Wes Fryer](https://www.wesfryer.com/)** of Charlotte, NC.  
Developed collaboratively through a “vibe coding” process with **ChatGPT‑5 (OpenAI)** and **Google Gemini**, combining iterative design, debugging, and documentation.  

Learn more and find related resources at **[ai.wesfryer.com](https://ai.wesfryer.com)**.

---

*Version: November 2025 — Secure Classroom Template Edition*
