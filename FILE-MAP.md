# FILE-MAP — what will exist after the 72h build
# This is a PLAN, not code. No implementation files exist yet (Rule 07).
# Each file is created during the event per PLAN-72H.md.

```
fridaybrief/                      # repo root (public, MIT)
├── README.md                    # exists (scaffold) — finalized at hour 40-52
├── PLAN-72H.md                  # exists — hour-by-hour build plan
├── SAFETY.md                    # exists (design) — finalized with file+line refs
├── AGENT.md                     # exists (template) — model + stack filled in
├── CHECKLIST-PRE-23NOV.md       # exists — this file's sibling
├── FILE-MAP.md                  # this file
├── demo-video-outline.md        # exists — ≤3 min video plan
├── LICENSE                      # MIT
├── .gitignore                   # runs/ (except committed examples), .env
├── .env.example                 # optional keys only (LLM, Keenable)
├── config.yaml                  # CREATED hour 0-4: topics, sources, budgets
├── fridaybrief/
│   ├── __main__.py              # CREATED hour 12-20: CLI (--once/--watch/--mock/--kill)
│   ├── config.py                # CREATED hour 0-4: config load + validate
│   ├── watcher.py               # CREATED hour 0-4: RSS + arXiv fetch (stdlib)
│   ├── search.py                # CREATED hour 20-30: Keenable plug (optional)
│   ├── dedupe.py                # CREATED hour 4-12: URL + title fingerprints
│   ├── firewall.py              # CREATED hour 20-30: injected-instruction scan
│   ├── summarizer.py            # CREATED hour 4-12 + 20-30: extractive + LLM
│   ├── library.py               # CREATED hour 4-12: Markdown notes + index
│   ├── brief.py                 # CREATED hour 12-20: Friday brief generator
│   ├── trace.py                 # CREATED hour 4-12: JSONL audit trail
│   ├── killswitch.py            # CREATED hour 12-20: STOP file + SIGINT + deadline
│   └── monitor.py               # CREATED hour 12-20: runs/status.json
├── fixtures/                    # CREATED hour 0-4: mock feeds (MOCK=1 mode)
├── tests/                       # CREATED during build: dedupe/firewall/summarizer/trace
├── runs/                        # GENERATED at runtime (gitignored, except examples)
│   └── trap-pack/results.md     # CREATED hour 30-40: committed trap results
└── library/                     # GENERATED at runtime: the reference library
```
