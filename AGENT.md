# AGENT.md — Model & stack declaration
# Required by the Agentware rules: "Name what you used in AGENT.md."
# Fill in the exact model + versions during the 72h build. Nothing here is
# final until kickoff week — this is the template.

## Agent
- Name: FridayBrief
- Track: T3 — Research & Study
- Job: watch research sources → dedupe → summarize → file into a local
  Markdown library → produce a Friday reading brief. Fully unattended.

## Model
- Primary (abstractive summaries, optional): [FILL IN AT BUILD TIME —
  e.g. provider + model name + why]
- Fallback (default, no key needed): extractive summarization, TF-IDF sentence
  ranking, implemented in `summarizer.py`. The agent works fully without any
  LLM key; the key only improves summary quality.
- No model call ever happens before `firewall.py` has scanned the input.

## Stack
- Language: Python 3.12, standard library only (urllib, xml.etree, json,
  hashlib, re). Zero third-party dependencies.
- Search (optional): Keenable web search API (free credits from Discord).
- No framework, no database, no server. State = files (`library/`, `runs/`).

## What a judge needs to run it
- Nothing but Python 3.12. Mock mode (`--mock`) needs no network and no keys.
- Optional keys (all in `.env`, never in git): `LLM_API_KEY`,
  `LLM_BASE_URL`, `LLM_MODEL`, `KEENABLE_API_KEY`.
- Cost of a mock test run: $0. Cost of a live run without an LLM key: $0.
  With a key: capped at $0.10/run by default (see SAFETY.md G3).

## How it is tested
- Unit tests: `tests/` (dedupe, firewall, summarizer, trace).
- Trap Pack: run at kickoff, results committed at `runs/trap-pack/results.md`.
- Demo video (≤ 3 min): one full unattended run, trigger to brief.
