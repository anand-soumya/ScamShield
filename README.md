# ScamShield

Paste a text, email, or DM and get an AI-powered risk score before you click
anything. Built with React, Vite, Ant Design, and the Gemini API.

## Requirements

- [Node.js](https://nodejs.org) 18 or newer (`node -v` to check)
- A free Gemini API key from [Google AI Studio](https://aistudio.google.com/app/apikey)

## Setup

```bash
# 1. Install dependencies
npm install

# 2. Add your API key
cp .env.example .env
# then open .env and paste your key after GEMINI_API_KEY=
```

## Run it

You need **two terminals** open at the same time — one for the frontend, one
for the backend that talks to Gemini:

```bash
# Terminal 1 — the API backend (port 4173)
npm run server

# Terminal 2 — the app itself (port 5173)
npm run dev
```

Open **http://localhost:5173** in your browser. Paste a suspicious message
into the scanner and click "Run Scan".

If the backend isn't running (or the API key is missing/invalid), the scanner
still works using a built-in offline keyword check as a fallback — you just
won't get real AI reasoning.

## Project structure

```
index.html        Vite entry point
src/               React app (App.jsx, Scanner.jsx, theme, animations)
api/scan.js        Serverless function that calls Gemini (used by both
                   the local dev server and Vercel in production)
server.js          Local stand-in for api/scan.js during development
```

## Deploying

This is set up to deploy to [Vercel](https://vercel.com) with zero config:

```bash
npx vercel
```

Then set `GEMINI_API_KEY` as an environment variable in your Vercel project
settings (Project → Settings → Environment Variables) — never commit your
real key to `.env`, only `.env.example` is tracked in git.
