# 🛡️ Cyber Shield — Cybersecurity Awareness Portal

A single-page, client-side web application that teaches everyday users (students, employees, families) to recognize phishing, social-engineering, and fraud attempts through interactive investigation cases, security checklists, practical tools, and an AI-style practice arena.

**Live demo:** _add your deployed URL here after Step 7 below_
**Screenshots:** see [`/screenshots`](./screenshots)

---

## ✨ Features

| Module | What it does |
|---|---|
| **Overview** | Cyber Score, current level, quick actions |
| **Investigation Lab** | 44 real-world phishing/scam cases across 6 categories (Email, SMS/WhatsApp, Website/URL, Social Media, AI/Deepfake, Public Wi-Fi). Tap suspicious phrases to reveal why they're red flags, then unlock the "safest move" for that case. 11 achievements track mastery. |
| **Safety Center** | 5 topic checklists (Mobile, Computer, Account, Privacy, Shopping) — 136 actionable checks in total |
| **Safety Tools** | Local URL safety checker, password strength analyzer, and an email phishing-risk analyzer — all rule-based, nothing leaves the browser |
| **Cyber Shorts** | Short, TikTok-style scripted dialogues that walk through a scam and its resolution |
| **AI Practice Arena** | Free-text response scoring against a rubric (verification habits, credential protection, reporting) with instant coaching |
| **Admin Dashboard** | Case-completion analytics, checklist engagement, and a live activity feed, gated to specific admin accounts |
| **Login** | Lightweight email-based session — each learner's progress is stored locally under their own email |

---

## 🧱 Technologies Used

- **HTML5 / CSS3** — semantic layout, CSS custom properties for theming, `prefers-color-scheme` + manual light/dark toggle
- **Vanilla JavaScript (ES6+)** — no framework, no build step, no external JS dependencies
- **SVG** — inline icons, charts (bar/donut) drawn by hand, and a procedurally generated triangulated-mesh background clipped to an eagle silhouette
- **Web Storage API** (`localStorage`) — per-user progress persistence, wrapped in `try/catch` for private-browsing resilience
- **Google Fonts (Inter)** — the only external network dependency

No backend, database, or build tooling is required — the entire app is one self-contained `index.html` file.

## 🏗️ System Architecture

```
┌──────────────────────────────────────────────┐
│                index.html                     │
│  ┌───────────────┐   ┌──────────────────────┐ │
│  │   HTML shell  │   │   Inline <style>      │ │
│  │  (nav, pages) │   │  (design tokens,      │ │
│  └───────────────┘   │   responsive rules)   │ │
│                       └──────────────────────┘ │
│  ┌────────────────────────────────────────┐    │
│  │            Inline <script>              │   │
│  │  • Data layer   : CASES[], CL[], KB[]   │   │
│  │  • State        : localStorage per email│   │
│  │  • Render layer : draw*() functions      │  │
│  │  • Event layer  : delegated click/input  │  │
│  └────────────────────────────────────────┘    │
└──────────────────────────────────────────────┘
                     │
                     ▼
            Browser localStorage
        (session + per-user progress)
```

There is no server round-trip: every module is a pure function of in-memory state, re-rendered into the DOM on each interaction.

## 📂 Repository Structure

```
cyber-shield/
├── index.html          # the entire application
├── README.md           # this file
├── LICENSE
├── docs/
│   └── DOCUMENTATION.md
├── presentation/
│   └── Cyber-Shield-Presentation.pptx
└── screenshots/
    └── (add PNGs exported from the running app)
```

## 🚀 Installation & Local Run

No build step, no dependencies to install.

```bash
git clone https://github.com/<your-username>/cyber-shield.git
cd cyber-shield
# open directly in a browser
open index.html        # macOS
xdg-open index.html     # Linux
start index.html        # Windows
```

Or serve it locally (recommended, avoids some browsers' `file://` restrictions on fonts):

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

## 🌐 Deployment

Because it is a single static file, it deploys to any static host in minutes:

| Host | Steps |
|---|---|
| **GitHub Pages** | Settings → Pages → Deploy from branch → `main` / root → save. Live at `https://<user>.github.io/cyber-shield/` |
| **Netlify** | Drag-and-drop the folder at [app.netlify.com/drop](https://app.netlify.com/drop), or connect the GitHub repo for auto-deploys |
| **Vercel** | `vercel` CLI or import the GitHub repo from the dashboard — no build command needed, output directory `/` |

## 🔐 Security Notes

- All rendered user input (login email, chat messages) is inserted via `textContent`, never `innerHTML`, so there is no reflected-XSS path from user-typed data.
- The login email is validated client-side with a format check before a session is created.
- There is no backend, database, or authentication secret in this build, so SQL injection and password storage do not apply — if you extend this into a full-stack app, hash passwords with `bcrypt`/`argon2` and parameterize every query.
- Serve over HTTPS in production; all static hosts above provide it by default.

## 🔭 Future Enhancements

- Real backend + database so progress syncs across devices instead of living in `localStorage`
- Real authentication (OAuth or email/password with hashing) instead of the current lightweight email-only session
- Server-backed AI (via an LLM API) for the email analyzer and practice-arena scoring, replacing the current rule-based heuristics
- PDF/Excel export of a learner's progress report
- Multi-language support
- Push/email notifications for weekly "scam of the day" reminders
- CI/CD with GitHub Actions (HTML/CSS/JS lint + automatic Pages deploy on push)

## 👤 Author

Vyshnavi — B.Tech, Computer Science Engineering (Data Science), Dhanekula Institute of Engineering & Technology, Vijayawada

## 📄 License

MIT — see [LICENSE](./LICENSE).
