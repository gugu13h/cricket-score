# cricket-score

## Firebase Firestore setup

This project is connected to Firebase Firestore from `index.html`. The Firebase config is intentionally blank so you can paste your own project values.

### 1. Get your Firebase web app keys

1. Go to <https://console.firebase.google.com/>.
2. Create a Firebase project, or open your existing project.
3. Click the gear icon next to **Project Overview**.
4. Open **Project settings**.
5. In the **General** tab, scroll to **Your apps**.
6. Add a **Web app** if one is not already listed.
7. Copy the `firebaseConfig` object Firebase shows for that web app.

Paste those values into the blank config block in `index.html`:

```js
const firebaseConfig = {
  apiKey: '',
  authDomain: '',
  projectId: '',
  storageBucket: '',
  messagingSenderId: '',
  appId: ''
};
```

If Firebase also gives you `measurementId`, you can add it under `appId`, but this scoreboard does not require it.

### 2. Create the Firestore database

1. In Firebase Console, open **Build > Firestore Database**.
2. Click **Create database**.
3. Choose a location close to your users.
4. Start in test mode while developing, or use the rules below manually.

The scoreboard saves one document here:

```text
matches/main-scoreboard
```

For quick testing, use these temporary Firestore rules:

```js
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /matches/{matchId} {
      allow read, write: if true;
    }
  }
}
```

These open rules are only for testing. Before sharing the app publicly, replace them with authenticated rules.

### 3. Run the app

Because this app imports Firebase with browser modules, run it through a local web server instead of opening the file directly:

```bash
python -m http.server 5500
```

Then open <http://localhost:5500/>.
