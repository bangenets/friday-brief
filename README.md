# FridayBrief — a research agent you can walk away from

**Agentware 2026 (Hackathon Raptors) — Track T3: Research & Study.**
**72-hour build: Nov 27, 18:00 UTC → Nov 30, 18:00 UTC. This repo is a SCAFFOLD:
planning, architecture, safety design and checklists only. No project code exists
here yet — writing it before kickoff disqualifies the submission (Rule 07:
"All project code written during the 72-hour window"). The code gets written
during the event, following `PLAN-72H.md`.**

## The job

A researcher picks topics and sources once. FridayBrief does the legwork every
day on its own:

1. **Watches** the sources you care about (RSS feeds, arXiv categories, and —
   with free Keenable credits — web search).
2. **Pulls in** what is new, deduplicates against what you already hold.
3. **Reads** each item, scores relevance to your topics, and summarizes it.
4. **Files** it in a local Markdown reference library, with notes and a link.
5. **Hands you a Friday brief**: what arrived this week, what matters, what to
   read first, and which deadlines are coming.

Trigger: a schedule (cron) or a single command. No human in the chair.

## Why this track, why this agent

- **It is a real job, narrowly scoped.** One input (new papers/posts), one output
  (a filed library + a weekly brief). A narrow agent that finishes the job beats
  an ambitious one that half-does it.
- **A judge can run it in under 15 minutes with zero cost.** `MOCK=1` runs the
  whole loop on bundled fixture feeds — no network, no API key. With keys, the
  same loop runs live; without an LLM key it falls back to extractive
  summarization (TF-IDF sentence ranking), so the agent never depends on a
  paid call to work.
- **Its safety story is the product, not a slide.** The agent reads untrusted
  web content every run — exactly the input the Trap Pack attacks with prompt
  injections. The input firewall, the read-only default, and the audit trail are
  core features, not afterthoughts (see `SAFETY.md`).
- **It fits the builder's existing skill:** research, summarization, filing,
  briefs — the same loop already run daily by hand.

## Architecture (to be built during the 72h)

```
fridaybrief/
  fridaybrief/
    __main__.py        CLI: run once / watch mode / --kill / --mock
    config.py          topics + sources from config.yaml (validated)
    watcher.py         RSS + arXiv fetch (urllib + xml.etree, stdlib only)
    search.py          Keenable web search plug (optional, free credits)
    dedupe.py          URL + title fingerprinting vs library index
    firewall.py        Input firewall: strips/flags injected instructions
    summarizer.py      Extractive (TF-IDF, no key) / abstractive (LLM, optional)
    library.py         Markdown notes + index.json, one file per item
    brief.py           Friday brief generator (Markdown)
    trace.py           JSONL audit trail: saw / decided / called / returned
    killswitch.py      STOP file + SIGINT handler + per-run deadline
    monitor.py         Live status file (runs/status.json) per step
  config.yaml          topics, sources, budgets (example included at build time)
  fixtures/            Mock feeds + mock trap-pack items (MOCK=1 mode)
  runs/                Traces + briefs (gitignored except committed examples)
  library/             The reference library the agent builds
  tests/               Unit tests for dedupe, firewall, summarizer, trace
  AGENT.md             Model + stack declaration (required by the rules)
  SAFETY.md            Guardrails enforced in code
  .env.example         Optional keys only (LLM, Keenable)
```

**Stack:** Python 3.12, standard library only, zero dependencies. LLM access (if
any) through an OpenAI-compatible HTTP endpoint — provider-agnostic, key optional.

## Safety, in one paragraph

FridayBrief only ever **reads** the internet and **writes** to its own library
folder. It cannot delete, message, post, or spend anything. Any action beyond
that requires a human approval step that does not exist yet — by design. Every
run writes a full JSONL trace, stops on a `STOP` file or Ctrl-C, and dies on a
per-run deadline and budget cap. Fetched content is treated as untrusted data:
the firewall scans for injected instructions before any of it reaches the model.
Full design: `SAFETY.md`.

## How a judge runs it (target: < 15 minutes)

```bash
git clone <repo> && cd fridaybrief
cp .env.example .env   # leave keys empty — mock mode needs none
python3 -m fridaybrief --mock --once
# then read: library/ (filed notes), runs/<date>/brief.md, runs/<date>/trace.jsonl
```

## Prizes (as published on agentwarehack.com)

$1,800 pool: 1st $800 · 2nd $400 · 3rd $200 · Best Kill Switch $100 ·
Near Miss $300 (3 × $100 write-ups, closes Dec 7, 18:00 UTC).
Judging Nov 30–Dec 10, winners announced Dec 11. Safety bonus up to +4
(Guardrails +1, Live Monitoring +1, Kill Switch +1, Audit Trail +1).

## Pre-event checklist

See `CHECKLIST-PRE-23NOV.md` — the short version: join the Hackathon Raptors
Discord and register (team formation closes **Nov 23**; solo is welcome), read
the full brief + scoring rubric when it is published **Nov 26**, and claim the
free partner credits (Keenable, Solari, Treg, akta.pro) on Discord before kickoff.

## License

MIT — see `LICENSE`.
