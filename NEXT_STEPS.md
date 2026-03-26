# DataLens — Next Steps

## Where we are
100% front-end. Single HTML file, no backend, no database.
AI calls go directly from the browser to external APIs (Ollama, Groq, OpenRouter).

## Path A — Static deployment (portfolio-ready, no backend needed)

1. Push project to GitHub
2. Enable GitHub Pages (Settings → Pages → branch main → / root)
3. Live at `https://your-username.github.io/datalens/`
4. Groq and OpenRouter work out of the box — user brings their own API key
5. Ollama local works only if the visitor has Ollama installed on their machine (documented in README)

```bash
git init
git add .
git commit -m "feat: DataLens v3 — initial release"
git remote add origin https://github.com/your-username/datalens.git
git push -u origin main
```

## Path B — Full-stack (if we want persistence, sharing, user accounts)

| Layer | Suggested tech | Role |
|---|---|---|
| Back-end | Node.js + Express or Python + FastAPI | REST API, AI proxy, auth |
| Database | PostgreSQL or SQLite | Save reports / chat history |
| Auth | Clerk or Auth.js | User accounts |
| Back-end hosting | Railway or Render (free tier) | Always-on server |
| Front-end hosting | Vercel or Netlify | Serve the HTML |

## Recommended order

1. Finish remaining features (see Roadmap in README)
2. Add 1–2 demo CSV screenshots to README
3. Record a short GIF demo for README (very effective for portfolios)
4. Deploy via Path A (GitHub Pages)
5. Path B only if we want to go further (report saving, shareable links, user accounts)
