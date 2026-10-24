# Setting up sync (laptop ↔ iPad)

Takes about 10 minutes, free.

## 1. Put the app online (GitHub Pages)
1. On GitHub, open this repo → **Settings** → **Pages**.
2. Under **Build and deployment**, set Source to **Deploy from a branch**, branch **main**, folder **/ (root)**, then **Save**.
3. After a minute you'll get a link like `https://<your-username>.github.io/FOCUS-Clock/`. Use that link on both devices.

## 2. Create a Firebase project
1. Go to https://console.firebase.google.com and click **Create a project** (Google Analytics not needed).
2. **Build → Authentication → Get started → Email/Password → Enable → Save.**
3. **Authentication → Settings → Authorized domains → Add domain:** `<your-username>.github.io`
4. **Build → Firestore Database → Create database** → pick a location → **Start in production mode**.
5. In Firestore, open the **Rules** tab, replace everything with the contents of `firestore.rules` from this repo, and **Publish**.

## 3. Connect the app
1. In Firebase, click the ⚙️ next to **Project Overview → Project settings**.
2. Under **Your apps**, click the **</>** (Web) icon, give it any name, click **Register app**.
3. Copy the `firebaseConfig = { ... }` object it shows.
4. In `index.html`, find `const FIREBASE_CONFIG = null;` and replace `null` with that object, e.g.
   ```js
   const FIREBASE_CONFIG = { apiKey: "...", authDomain: "...", projectId: "...", storageBucket: "...", messagingSenderId: "...", appId: "..." };
   ```
   (These keys are safe to have in public code — the Firestore rules are what protect your data.)

## 4. Use it
- Laptop: open the app → ⚙️ → **Sync** → **Create account**.
- iPad: open the same link → ⚙️ → **Sync** → **Sign in** with the same email/password.
- If a device already has its own data when you sign in, it asks which copy to keep.

Changes show up on the other device within a few seconds. Without internet, everything keeps working and syncs once you're back online.
