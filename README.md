# ✍️ The Draft Desk — MCP Chief of Staff

An AI "chief of staff" that triages an inbox, drafts replies in your voice, and gates every send behind human approval — with a full audit log as proof.

Built around a **Model Context Protocol (MCP)** style workflow: the agent proposes actions (triage → draft → approve → export), and a person confirms each one before anything is sent.

## Workflow
1. **Inbox & Triage** — classify each thread (urgency, category, suggested action) with Gemini.
2. **Draft Generation** — generate a reply in your tone from `tone_profile.json` + past replies.
3. **Approval Gate** — review, edit, and approve/reject each draft. Nothing sends without approval.
4. **Export Proof** — every action is written to an audit log (`action_log.json`).

## Two data sources
- **Sample threads** (default) — runs fully on the bundled JSON, no Google setup needed. Use this for the live demo.
- **Gmail via engine.py** (optional) — connects to a real inbox via Gmail OAuth (`credentials.json` / `token.json`). Not available on the hosted demo.

## Tech
Python · Streamlit · Google Gemini (`gemini-3.6-flash`) · MCP-style approval workflow

## Run locally
```bash
pip install -r requirements.txt
cp .env.example .env      # then add your GEMINI_API_KEY
streamlit run app.py
```

## Deploy free (Streamlit Community Cloud)
1. Push this repo to GitHub (done).
2. Go to **share.streamlit.io** → **New app** → pick this repo → main file `app.py`.
3. In **Advanced settings → Secrets**, paste:
   ```toml
   GEMINI_API_KEY = "your_gemini_api_key"
   ```
4. **Deploy**, then use **Sample threads** mode to try the full flow.

## Secrets
- `GEMINI_API_KEY` — required for triage/draft (free at https://aistudio.google.com/app/apikey). Set it in Secrets (Streamlit exposes it as an env var).
- `credentials.json` / `token.json` — only for the optional live-Gmail mode; never committed.
