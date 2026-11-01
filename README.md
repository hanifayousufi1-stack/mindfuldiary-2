# 🌿 MindfulDiary 2.0 — Wellness Edition

A responsive personal journaling application built with **React + Vite**, with mood tracking, insights, searchable entries, local backups, and optional AI-powered reflections.

## Features

- Calming sage-green wellness interface with responsive desktop/mobile navigation
- Create, edit, and delete journal entries; choose a mood and date
- Search entries and filter by mood/date
- Dashboard with entry count, words, streaks, and daily inspiration
- Mood charts for 7, 14, and 30 days; progress insights
- Light/dark themes and personalized greeting
- JSON export/import backups
- Optional OpenRouter AI reflections via a **Netlify serverless function**

## Run locally

Install Node.js 20.19+ (or 22+), then:

```bash
npm install
npm run dev
```

Open the localhost URL shown by Vite. Build with `npm run build`.

**Note:** `npm run dev` runs the frontend only. `/api/reflect` needs Netlify Functions. To test the AI function locally, install Netlify CLI (`npm install -g netlify-cli`), set `OPENROUTER_API_KEY` in your local environment (never in frontend source), then run `netlify dev`.

## GitHub upload

### Recommended: new repository

1. Extract this ZIP. Do **not** upload the ZIP itself as your deployed website.
2. Create a new repository named `mindfuldiary-2` on GitHub.
3. In a terminal inside the extracted folder, run:

```bash
git init
git add .
git commit -m "Build MindfulDiary 2.0 wellness edition"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/mindfuldiary-2.git
git push -u origin main
```

Replace `YOUR_USERNAME` with your GitHub username. If GitHub requests authentication, use the browser sign-in or an appropriate credential manager.

### Replace the old repository instead

Back up your old repository first. Then copy the new files into your existing clone, remove obsolete old application files, review `git status`, commit, and push. **Do not delete user data before exporting a backup.**

## Deploy to Netlify

1. Log in to [Netlify](https://app.netlify.com/).
2. Choose **Add new project → Import an existing project → GitHub**.
3. Select your repository and authorize access if prompted.
4. Build command: `npm run build`; publish directory: `dist` (also defined in `netlify.toml`).
5. Deploy. Netlify will give you a live `*.netlify.app` URL.
6. Optionally customize the site name under domain management.
7. Future pushes to your main branch automatically trigger new builds if continuous deployment is enabled.

### Enable AI reflections (optional)

1. Create an API key at [OpenRouter](https://openrouter.ai/).
2. In Netlify open **Project configuration / Site configuration → Environment variables** (menu wording may differ).
3. Add `OPENROUTER_API_KEY` as a secret server-side environment variable.
4. Optionally add `OPENROUTER_MODEL`, e.g. `openai/gpt-4o-mini` (confirm that model is currently available and check provider pricing).
5. Redeploy your site. The `netlify/functions/reflect.mjs` function handles AI requests at `/api/reflect`.
6. In the editor, write at least 15 characters, check the consent box, then click **Generate reflection**.

**Important:** OpenRouter may charge for API usage. Never add your key to `src/`, a `VITE_` environment variable, or GitHub commits. Without an API key, the app still works, but AI reflection requests show a configuration message.

## Data & privacy

Journal entries and saved AI responses are stored in **browser localStorage** only. There is **no account login, cloud sync, end-to-end encryption, or password protection** in this release. Anyone with access to your unlocked browser profile may read the entries. Browser storage can be cleared. Export backups regularly, and keep those files private.

Only when the user explicitly requests an AI reflection (after checking the consent box), the entry text and selected mood are sent to the serverless function, then to OpenRouter and its model provider. Review the provider's privacy policy before entering sensitive information. The AI assistant is not a mental-health professional.

The serverless function is a starter implementation, not a hardened public API. Before significant public use, add per-user rate limits, abuse prevention, monitoring, and stronger security controls to avoid unwanted API costs.

## Migration from MindfulDiary 1.0

This is a **new application** and does not automatically import the previous application's localStorage data. If the old app contains entries, export or copy them before replacing the deployment. The v2 import feature expects a v2 JSON backup format. Do not overwrite your old deployment until you have verified your data is safe.

## Tech stack

React 18 · Vite 6 · CSS · Lucide React · Recharts · Netlify Functions · OpenRouter (optional)

## Project layout

```
src/
  App.jsx          # Pages, components, storage and journal workflows
  styles.css       # Design system and responsive layouts
  main.jsx         # React entry point
netlify/functions/
  reflect.mjs       # Server-side AI request handler
netlify.toml        # Netlify build and routing configuration
```

Built with care for mindful moments. 🌱
