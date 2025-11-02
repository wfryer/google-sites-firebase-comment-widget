# Google Sites Comment Widget (Firebase + HTML)

A simple, copy-and-paste comment system you can embed in **Google Sites** (or any website) using only HTML and Firebase Firestore.  
Perfect for teachers who want students to give feedback on digital projects — without needing WordPress, PHP, or paid hosting.

---

## 🎯 Project Overview

This widget lets students:
- Enter their **name**, **class section**, and **comment**
- Submit feedback that is stored in a **Firestore NoSQL database**
- See all comments live under the form (for that specific project)

Teachers can view and moderate all comments using the **comments dashboard page**.

---

## 🧰 What You’ll Need
1. A free [Google account](https://accounts.google.com/)
2. A [Firebase](https://firebase.google.com/) account (also free)
3. Two HTML files from this project:
   - `index.htm` → for student comments
   - `comments.htm` → for teachers to review feedback
4. Optional free hosting (explained below) such as **GitHub Pages**

---

## 🪜 Step-by-Step Setup

### 1️⃣ Create a Firebase Project
1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click **Add project** → give it a name (e.g. `student-comments`)
3. Disable Google Analytics for simplicity → click **Create Project**

---

### 2️⃣ Add a Web App
1. Inside your new Firebase project, click **</> Add app**.
2. Name it (e.g. `comments-widget`) and click **Register app**.
3. Click **Continue to console**.
4. Under “Your apps,” copy the **Firebase config snippet** — it looks like:

```js
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  projectId: "YOUR_PROJECT",
  storageBucket: "YOUR_PROJECT.appspot.com",
  messagingSenderId: "###########",
  appId: "APP_ID"
};
