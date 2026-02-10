# DoLess-Agents
A  chrome extension and application that will perform computer use and will be able to produce and use generated functions and workflows which automate processes partially allowing for lower costs and time delays.


# Beginner Setup Guide

This is a beginner-friendly quick start for the main GitHub page.

## What This Project Is

This is a Chrome extension that lets you:

- record browser actions
- replay them later
- generate reusable automation functions with AI
- run tasks with cloud AI (Gemini) or local AI (Ollama)

## Quick Start (First 10 Minutes)

### 1) Prerequisites

- Google Chrome
- A Gemini API key (for AI generation and cloud features)
- Optional: Ollama (for local AI)
- Optional: Docker (for the function backend)

### 2) Load the Extension in Chrome

1. Download or clone this repository.
2. Open `chrome://extensions/`.
3. Turn on **Developer mode** (top right).
4. Click **Load unpacked**.
5. Select this folder:
6. Pin the extension if needed, then open it.

### 3) Open Settings

1. Open the extension UI.
2. Click the gear icon (`Settings`).
3. Keep this panel open for the next steps.

### 4) Add Your Gemini API Key

1. In Settings, find **Gemini API Key**.
2. Paste your key from Google AI Studio:
   https://aistudio.google.com/
3. Click outside the input box so the value is saved.

Notes:

- Many AI features depend on this key.
- If "Generate Function from Recording" is disabled, the key is usually missing.

### 5) Enable Ollama (Local AI, Optional)

### Install and run Ollama

1. Install Ollama from https://ollama.com/
2. Start Ollama:

```bash
ollama serve
```

3. Pull at least one local model:

```bash
ollama pull gemma3:4b
```

4. Optional but recommended for local embeddings:

```bash
ollama pull embeddinggemma
```

### Connect Ollama in the extension

1. In Settings -> **Local AI (Ollama)**:
   - **Ollama URL**: `http://localhost:11434`
   - **Ollama Model**: choose your pulled model
   - **Embedding Engine**: `gemini` (default) or `ollama` (local)
2. Confirm the status badge shows **ON**.

### If Ollama shows OFF, ERR, or HTTP 403

1. Make sure `ollama serve` is running.
2. Check the URL is exactly `http://localhost:11434`.
3. If you see a 403 error, allow the Chrome extension origin in `OLLAMA_ORIGINS` and restart Ollama.

PowerShell example:

```powershell
$env:OLLAMA_ORIGINS="chrome-extension://YOUR_EXTENSION_ID"
ollama serve
```

macOS/Linux example:

```bash
export OLLAMA_ORIGINS="chrome-extension://YOUR_EXTENSION_ID"
ollama serve
```

You can find `YOUR_EXTENSION_ID` at `chrome://extensions/` under this extension.

### 6) Optional: Start the Function Backend (Docker)

Use this if you want shared function search/import and optional upload of verified functions.

1. Open a terminal in `function-backend/`
2. Run:

```bash
docker compose up --build
```

3. Verify:
   - UI: `http://localhost:8787`
   - API health: `http://localhost:8787/api/health`

4. In extension Settings -> **Function Backend**:
   - Enable **Use backend search/import for missing local functions**
   - Keep URL as `http://localhost:8787`
   - Optional: enable **Send tested + verified functions to backend (opt-in)**

### 7) First Run Checklist

1. Go to a test website.
2. In **Record** tab, click **Start Recording** and do a few actions.
3. Save the task.
4. In **Playback** tab, run it.
5. Click **Generate Function from Recording** to create a reusable function.

If this works, your setup is complete.

## Quick Troubleshooting

- AI buttons disabled: Gemini API key is missing.
- Ollama model dropdown says "No models found": run `ollama pull <model>`.
- Ollama still OFF: verify `ollama serve` is active and URL is correct.
- Backend OFF: check Docker container is running on port `8787`.
