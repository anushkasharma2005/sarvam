# morning-brief

A personal assistant that reads overnight Gmail and WhatsApp activity (via an
MCP server) and gives you a morning summary. Sarvam AI does the language work.

Right now this repo contains only the Sarvam setup — one working API call.

## Setup

```bash
pip install -r requirements.txt
cp .env.example .env     # then paste your key into .env
python hello_sarvam.py
```

Get an API key at https://dashboard.sarvam.ai

Expected output: a one-sentence greeting from `sarvam-105b-conversations`.

## Notes

`.env` is gitignored. The key is read from the environment and never printed.

See [CLAUDE.md](CLAUDE.md) for API conventions and model choices.

## Web app

1. In Google Cloud Console: create a project, enable the Gmail API and Google Calendar API,
   configure the OAuth consent screen (add yourself as a test user), then create an
   OAuth client ID of type **Web application** with redirect URI
   `http://localhost:5000/oauth2callback`.
2. Put `GOOGLE_CLIENT_ID` and `GOOGLE_CLIENT_SECRET` in `.env`.
3. `python app.py`, open http://localhost:5000, click **Connect Google**.
4. Optional: add WhatsApp chat exports (.txt) on the page.
