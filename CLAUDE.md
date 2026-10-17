# CLAUDE.md

Context for Claude Code working in this repo.

## What this project is

A personal morning-brief assistant. It reads overnight activity from connected
sources (Gmail, WhatsApp, and other apps exposed through an MCP server) and
produces a short summary each morning. Planned follow-ons: creating calendar
events from things mentioned in those messages, and answering questions about
news and current events.

Current state: **Sarvam setup only.** One script that makes one API call. Nothing
else is built yet.

## Stack

- Python 3
- `sarvamai` — Sarvam AI Python SDK
- `python-dotenv` — loads `.env`

Install: `pip install -r requirements.txt`

## Sarvam API conventions

```python
from sarvamai import SarvamAI

client = SarvamAI(api_subscription_key=os.environ["SARVAM_API_KEY"])

response = client.chat.completions(
    model="sarvam-105b-conversations",
    messages=[{"role": "user", "content": "..."}],
)
print(response.choices[0].message.content)
```

Models and endpoints:

| Model | Endpoint | Context | Use for |
| --- | --- | --- | --- |
| `sarvam-105b` | `/v1` and `/v2` | 128K | reasoning, agentic work, tool calling, `wiki_grounding` |
| `sarvam-105b-conversations` | `/v1` only | 32K | real-time dialogue, voice agents |

Open-source models (e.g. `glm5.2`, `gemma4`) go through
`client.open_source_models.chat_completions_v2(...)` on `/v2` — `/v1` does not
accept them.

Docs: https://docs.sarvam.ai/api/getting-started/welcome
Machine-readable index: append `/llms.txt` to any docs URL, or `.md` to any page.

## Rules

- Never hardcode, log, or print `SARVAM_API_KEY`. Read it from the environment.
- `.env` is gitignored. `.env.example` is the committed template — keep it in
  sync with any new variables.
- Keep dependencies minimal. Don't add a framework, logging setup, or test
  harness unless asked.
- Don't invent dummy API keys or stub out calls to get past a missing key. If a
  credential is missing, stop and say so.

## Files

```
hello_sarvam.py    one chat completion call, prints the reply
requirements.txt   dependencies
.env               real key (gitignored)
.env.example       template
```
