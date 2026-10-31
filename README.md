# 👻 PhantomTrail

> **A local-first, privacy-preserving Second Brain powered by open-weight Gemma & dual-mode AI inference.**  
> *Built for Hacktoberfest 2026: AI Belongs to Everyone ("Ghost in the Machine" DEV Challenge).*

---

## 💡 Overview

Every day, developers and researchers leave behind a ghost trail of dozens of open tabs, fleeting thoughts, and unread bookmarks. 

**PhantomTrail** captures these ephemeral digital footprints, computes your reading scroll depth, and organizes everything into a local Markdown vault formatted into an interactive **Concept Tree**.

### ✨ Key Features
- **👻 Ephemeral Trace Ingestion:** 1-click capture from any active tab via a lightweight Manifest V3 Chrome Extension.
- **📍 Reading Depth Tracker:** Tracks the exact scroll percentage where you stopped reading.
- **📁 Local Markdown Vault:** Every captured resource is saved as a real `.md` file on your filesystem inside `vault/<concept>/` (100% Obsidian/Logseq compatible).
- **🌳 Interactive Concept Tree:** Automatic hierarchical taxonomy: `Concept ➔ #tags ➔ Saved Notes`.
- **💬 Vault AI Companion:** Multi-turn chat with an AI companion that navigates your local files and saves conversation history in the sidebar.
- **⚡ Dual-Mode AI Dispatcher:** Run **100% locally** via `llama.cpp` CUDA (tested on NVIDIA RTX 4050) or switch to **Cloud Gemini API** with zero GPU dependencies.

---

## 🛠️ Architecture

[ Active Web Tab ]
      │
      ▼ 
(Extension Popup)
[ Chrome Extension (Manifest V3) ]
      │
      ▼ 
POST /api/capture
[ FastAPI Vault Backend ]
      │
┌─────┴──────────────────────────────┐
    
[ Local GPU Mode ] [ Cloud API Mode ]
llama.cpp CUDA server Google Gemini / Gemma API
(gemma-4-E4B-it.gguf) (Zero setup fallback)

└─────┬──────────────────────────────┘ 
      ▼
[ Local Markdown Vault (vault/) ] ──► [ Interactive Dashboard ]


---

## 🚀 Quickstart Guide

### 1. Clone & Set Up Backend

```bash
git clone https://github.com/<your-username>/phantomtrail.git
cd phantomtrail/backend

# Create virtual environment
python3 -m venv venv
source venv/bin/activate.fish  # Or 'source venv/bin/activate' for bash

# Install dependencies
pip install fastapi uvicorn httpx pydantic


2. Choose Your AI Engine

Option A: 100% Local GPU (Recommended)
Run llama.cpp server with an open-weight Gemma model:

code
Bash
./llama-server -m path/to/gemma-4-E4B-it-Q4_K_M.gguf -ngl 99 -c 4096 --port 8080
Start the FastAPI backend:

code
Bash
python main.py

Option B: Cloud Gemini API (No GPU Required)

Start the FastAPI backend:

code
Bash
python main.py

In the Extension or Dashboard top bar, select ☁️ Cloud Gemini API and paste your free key.

3. Install Chrome Extension

1. Open chrome://extensions/ in Chrome.
2. Enable Developer mode (top-right toggle).
3. Click Load unpacked and select the phantomtrail/extension folder.
4. Open http://127.0.0.1:8000/dashboard to access your interactive knowledge graph!


🔓 Why Open Innovation Matters
Browsing history and unedited thoughts are the most private digital traces a human produces. Traditional bookmark managers upload this sensitive behavioral data to third-party clouds for surveillance and advertising.
With open-weight models (Gemma) and local inference engines (llama.cpp), PhantomTrail ensures not a single token or URL ever leaves your device.
