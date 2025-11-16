# eVote — Election Management System (single-file prototype)

A compact, single-file HTML prototype for a simple election / class representative voting system. The UI offers separate admin and student flows, candidate and student management, election scheduling, and results publishing. The file in this workspace is `eVote.html`.
# 🗳️ eVote — Election Management System (Single-File Prototype)

## What's included
**eVote** is a compact, single-file web prototype for managing simple elections such as class representative voting.
It offers both **Admin** and **Student** roles, allowing you to add candidates and students, start or schedule elections, record votes, and publish results — all within one HTML file.

- `eVote.html` — the single-file application (UI + client-side logic). It expects two SDKs to be available at `/ _sdk/data_sdk.js` and `/_sdk/element_sdk.js` (referenced inside the HTML).
- `README.md` — this file.
---

## Features
## 📁 Project Structure

- Role selection: Student login and Admin portal.
- Student management: Add/remove students (stored via the provided data SDK).
- Candidate management: Add/remove candidates and limit checks.
- Election controls: Start, stop, schedule elections, countdown timer.
- Voting UI for students, with published-results display.
- Uses an expected `window.dataSdk` to persist and react to data changes.
| File         | Description                                                                                                          |
| ------------ | -------------------------------------------------------------------------------------------------------------------- |
| `eVote.html` | Main application file (UI + client-side logic). References two SDKs: `/_sdk/data_sdk.js` and `/_sdk/element_sdk.js`. |
| `README.md`  | This documentation file.                                                                                             |

## Quick start (local)
---

Because the app references SDKs using absolute paths and includes async behavior, run it from a local static server rather than opening the file directly to ensure relative routing and fetch behavior work as expected.
## 🚀 Features

Open a PowerShell terminal in the project folder (`e:\eVote`) and run a simple HTTP server (Python is commonly available):
* **Role Selection:** Choose between *Admin Portal* and *Student Login*.
* **Student Management:** Add, edit, and remove students using the Data SDK.
* **Candidate Management:** Add/remove candidates with built-in validation.
* **Election Control:** Start, stop, and schedule elections; includes countdown timer.
* **Voting System:** Students can cast votes during active elections.
* **Results Management:** Admin can view live results and choose when to publish them.
* **Persistence Layer:** Designed to work with `window.dataSdk` for saving and reacting to data changes.

---

## 🧩 Quick Start (Local)

Because the app references SDKs via absolute paths and relies on asynchronous data fetching, you should run it from a local server — **not by double-clicking the file**.

### 1️⃣ Run a local HTTP server

Open PowerShell (or terminal) inside the project folder, e.g. `E:\eVote`, and run:

```powershell
# serve current directory on port 8000
# Serve current directory on port 8000
python -m http.server 8000
# or if you prefer PowerShell's built-in server (PowerShell 6+), use:
# Start-Process -NoNewWindow -FilePath "dotnet" -ArgumentList "-c"  # (example placeholder)
```

Then open http://localhost:8000/eVote.html in your browser.
Then open your browser and visit:

👉 **[http://localhost:8000/eVote.html](http://localhost:8000/eVote.html)**

> **Note:**
> The app expects the SDK files at `/_sdk/data_sdk.js` and `/_sdk/element_sdk.js`.
> Make sure to place them there or update their paths in the HTML `<script>` tags.

---

## 🧑‍💻 How to Use

### 🧭 For Students

1. Click **Student Login**.
2. Sign in with your registered **email** and **password**.
3. If the election is active, the voting form will appear.
4. Submit your vote for your chosen candidate.

Note: The app references `/_sdk/data_sdk.js` and `/_sdk/element_sdk.js`. For local testing you will need to provide those files at `/_sdk/` on your server or adjust the paths in `eVote.html` to match where you place the SDKs.
### ⚙️ For Admins

## How to use
1. Click **Admin Portal**.
2. Log in with admin credentials (see `defaultConfig` in `eVote.html`).
3. Manage:

- Student:
  - Click "Student Login" and sign in with a registered student email and password.
  - If the election is active, the voting form appears.
   * Students
   * Candidates
   * Election scheduling
   * Result visibility
4. Start or stop elections as needed.

- Admin:
  - Click "Admin Portal" and sign in with admin credentials. By default, some credentials are included in `defaultConfig` inside `eVote.html` for prototyping — see Security below.
  - Manage students and candidates, start/stop/schedule elections, and publish results.
---

## Configuration pointers
## ⚙️ Configuration Guide

Open `eVote.html` and look for the `defaultConfig` object. It contains UI text, default admin credentials, and color/visual settings. For production or shared demos, change or remove default credentials and provide credentials/config via a secure mechanism.
Inside `eVote.html`, locate the `defaultConfig` object. It defines:

## Security & production recommendations (important)
* Default admin credentials (for demo use only)
* UI labels and colors
* Behavior settings

This project is a prototype and has a few important security gaps you should address before any real deployment:
> 🔐 **Important:**
> Default credentials should be removed before deploying or sharing publicly.

1. Do NOT keep plaintext passwords in `defaultConfig` or student records. Store and compare password hashes instead (e.g., SHA-256 or better with a salt and a proper PBKDF such as bcrypt/Argon2 on the server side).
2. Do not perform sensitive authentication or authorization purely in client-side JavaScript. Admin authentication should be validated by a server. The single-file approach is only suitable for demos.
3. Serve the site over HTTPS when deployed publicly.
4. Sanitize all user inputs before storing or rendering (candidate names, student names/emails, free text) to avoid injection/XSS.
5. Ensure `/_sdk/data_sdk.js` implements server-side persistence and access controls; client-side SDK usage alone cannot enforce security.
---

## Development notes & suggested next steps
## 🔒 Security & Production Recommendations

- Replace plaintext student passwords with hashed passwords when creating student records and compare hashes on login. The app already includes a suggested client-side SHA-256 helper in notes, but prefer server-side hashing with salts.
- Convert the `election_config` to a singleton pattern (store/lookup by a stable config ID) to avoid accidental multiple configs.
- Improve error handling and surfacing of SDK errors to the UI.
- Add unit or integration tests for critical flows (login, add student, add candidate, voting logic, publish results).
This is a **prototype** for demonstration purposes.
Before any real-world deployment, please implement the following:

## Files to edit
1. **Never store passwords in plain text.**
   Use salted and hashed passwords (e.g. SHA-256, bcrypt, or Argon2) — ideally server-side.
2. **Do not rely on client-side authentication.**
   Validate logins and privileges on a secure backend.
3. **Serve over HTTPS** when deployed publicly.
4. **Sanitize all user inputs** to prevent XSS or injection attacks.
5. **Enforce backend-side access control** in your `data_sdk.js` implementation.

- `eVote.html` — UI, logic and configuration. Edit `defaultConfig` for labels/colors and wire up SDK settings.
---

## Troubleshooting
## 🧠 Development Notes & Next Steps

- If the page reports missing SDK files, place `data_sdk.js` and `element_sdk.js` under a `_sdk` directory at the server root or edit the `<script>` tags to point to valid local copies.
- If votes or students don't persist, confirm `window.dataSdk` is implemented and connected to a backend.
Recommended improvements:

## License
* Replace plain-text passwords with hashed values.
* Convert `election_config` to a singleton to prevent duplicates.
* Add proper error handling and user feedback for SDK operations.
* Implement unit/integration tests for:

This repository contains sample/prototype code. Add a LICENSE file or change licensing as needed for your project.
  * Login
  * Adding students
  * Adding candidates
  * Voting logic
  * Result publishing

## Next steps I can do for you
---

- Implement password hashing (client-side helper + store hashed values) and/or wire a recommended server-side approach.
- Add input sanitization helpers and integrate them into the forms.
- Implement a stable singleton election config record pattern.
## 🧾 Troubleshooting

If you'd like, I can implement the password-hashing changes directly in `eVote.html` now. Would you like me to do that?
| Problem                       | Possible Fix                                                              |
| ----------------------------- | ------------------------------------------------------------------------- |
| Missing SDK files             | Place `data_sdk.js` and `element_sdk.js` under `/_sdk/`, or update paths. |
| Votes/students not persisting | Ensure `window.dataSdk` connects properly to backend.                     |
| Login not working             | Check credential setup in `defaultConfig`.                                |
