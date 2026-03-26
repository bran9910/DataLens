# DataLens v3 — Intelligent Auto Report Generator

> A self-contained, single-file data analytics dashboard with an integrated AI assistant. No server, no dependencies to install — just open the HTML file in your browser.

---

## Overview

DataLens is a pure HTML/CSS/JavaScript dashboard that transforms raw CSV data into interactive charts, statistical summaries, and AI-powered insights. The entire application ships as a single `.html` file, making it trivially portable and easy to embed in any workflow.

This project was built as part of a portfolio to demonstrate end-to-end product thinking: from data ingestion and visualization to conversational AI integration with multiple provider strategies.

---

## Features

- **Drag & drop CSV import** — auto-detects column types (numeric, categorical, date)
- **Interactive charts** — bar, line, pie, scatter, and histogram views powered by Chart.js
- **Statistical summary** — min, max, mean, median, standard deviation per column
- **Correlation matrix** — highlights relationships between numeric variables
- **AI assistant** — conversational interface aware of your loaded dataset, with support for multiple AI backends
- **Report export** — generates a standalone HTML report you can share or print
- **Zero-install** — no Node.js, no Python, no build step; works from `file://` or any HTTP server

---

## Tech Stack

| Layer | Technology |
|---|---|
| UI & logic | Vanilla HTML / CSS / JavaScript (ES2020) |
| Charts | [Chart.js 4.5](https://www.chartjs.org/) |
| CSV parsing | [PapaParse 5.4](https://www.papaparse.com/) |
| Fonts | Inter (Google Fonts) |
| AI backends | Ollama · OpenRouter · Groq · Custom OpenAI-compatible |

---

## Getting Started

### Option A — Open directly (quickest)

```bash
# Clone the repo
git clone https://github.com/your-username/datalens.git
cd datalens

# Open in your browser
open Projet_2B_ReportGenerator/DataLens.html
```

> **Note:** Some AI providers (Ollama local) require the file to be served over HTTP due to browser CORS policies. Use Option B in that case.

### Option B — Serve locally

```bash
# Python (built-in)
python -m http.server 8080

# Then open
http://localhost:8080/DataLens.html
```

---

## AI Assistant Setup

The AI tab supports five provider modes. Switch between them using the **Provider** dropdown in the assistant panel.

### 🏠 Ollama Local / Cloud *(recommended for privacy & free usage)*

This mode connects to a locally running [Ollama](https://ollama.com) instance at `http://localhost:11434`. It supports two types of models:

#### Standard local models (run on your own GPU/CPU)

```bash
# Pull a model
ollama pull llama3.2
ollama pull mistral

# Start Ollama (allow browser access)
OLLAMA_HOST=0.0.0.0 OLLAMA_ORIGINS=* ollama serve
```

#### Cloud-offloaded models (computation on Ollama's servers, accessed via local client)

Ollama supports a special class of models tagged `-cloud` — these are pulled like any local model but the inference runs on Ollama's cloud infrastructure. Your local Ollama client acts as a transparent proxy. **No API key is needed in the dashboard** — authentication is handled entirely by the Ollama CLI.

```bash
# Step 1 — Sign in to your Ollama account (one-time setup)
ollama signin

# Step 2 — Pull a cloud model (tiny pointer file, ~346 bytes)
ollama pull qwen3.5:397b-cloud
ollama pull gemma3:27b

# Step 3 — Start Ollama with browser access enabled
OLLAMA_HOST=0.0.0.0 OLLAMA_ORIGINS=* ollama serve
```

Once signed in, the dashboard connects to `http://localhost:11434` exactly as it would for a local model — Ollama handles the routing to the cloud transparently. Cloud models appear in the model list with a ☁️ icon and are sorted to the top.

> **How `ollama signin` works:** running the command opens a one-time URL in your browser (`https://ollama.com/connect?...`). Log in to your ollama.com account on that page to link your machine. This is a device-auth flow — no token is stored in your shell environment.

**Running Ollama in WSL (Windows Subsystem for Linux)?**

WSL runs a separate Linux network stack. To make Ollama reachable from your Windows browser:

```bash
# Sign in first (if using cloud models)
ollama signin

# Start Ollama bound to all interfaces so Windows can reach it
OLLAMA_HOST=0.0.0.0 OLLAMA_ORIGINS=* ollama serve
```

Then open `http://localhost:11434` in your Windows browser — you should see `Ollama is running`. The dashboard auto-detects all installed models on load, including cloud ones.

---

### 🌐 OpenRouter *(free tier available)*

[OpenRouter](https://openrouter.ai) aggregates dozens of models from Google, Meta, Mistral, DeepSeek, and more. The free tier provides access to several capable models with no credit card required.

1. Create an account at [openrouter.ai](https://openrouter.ai)
2. Generate an API key at [openrouter.ai/keys](https://openrouter.ai/keys)
3. Paste the key (starts with `sk-or-v1-…`) into the **API Key** field
4. If you get a 404 error, go to [openrouter.ai/settings/privacy](https://openrouter.ai/settings/privacy) and enable **Allow all providers**

---

### ⚡ Groq *(fast inference, generous free tier)*

[Groq](https://groq.com) offers extremely fast inference (LPU hardware) with a free tier of 14,400 requests/day.

1. Create an account at [console.groq.com](https://console.groq.com)
2. Generate an API key at [console.groq.com/keys](https://console.groq.com/keys)
3. Paste the key (starts with `gsk_…`) into the **API Key** field

---

### ⚙️ Custom (any OpenAI-compatible endpoint)

Enter any base URL that follows the OpenAI API format (`/v1/chat/completions`). Works with self-hosted models (LM Studio, vLLM, llama.cpp server, etc.).

---

## Provider Comparison

| Provider | Cost | Privacy | Setup | Best for |
|---|---|---|---|---|
| Ollama Local | Free | ✅ 100% local | Ollama installed | Sensitive data, offline use |
| Ollama Cloud models | Free (account req.) | Data sent to Ollama | `ollama signin` + `ollama pull name-cloud` | Large models without local GPU |
| OpenRouter | Free tier | Data sent to provider | API key | Quick start, model variety |
| Groq | Free tier | Data sent to Groq | API key | Speed-critical use cases |
| Custom | Varies | Depends on endpoint | URL + key | Self-hosted or enterprise LLMs |

---

## Project Structure

```
Projet_2B_ReportGenerator/
├── DataLens.html       # Entire application (single file)
└── README.md           # This file
```

---

## Roadmap

- [ ] PDF export of reports
- [ ] Multi-file join support
- [ ] Persistent chat history per dataset
- [ ] Shareable dashboard URLs (via URL-encoded state)

---

## License

MIT — feel free to use, modify, and distribute.
