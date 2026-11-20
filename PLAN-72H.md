# FridayBrief — 72-hour build plan
# Agentware 2026 · Nov 27, 18:00 UTC → Nov 30, 18:00 UTC
# Times in UTC (WIB = UTC + 7). "No code yet" rule: nothing in this plan is
# written before kickoff — this file is planning, which the rules allow.

## Rules that shape this plan (from agentwarehack.com)
- All project code written during the 72h window. Planning / prompt sketching /
  stack-picking beforehand is fine. Code committed before kickoff disqualifies.
- Judge must be able to run it in < 15 min from the README + .env.example.
  Free tiers, mock mode, or a recorded trace for expensive paths are all fine.
- Public repo, OSI license (MIT chosen). Demo video ≤ 3 min: one full
  unattended run, trigger to finish, no human touching the keyboard mid-run.
- Every run leaves a trace (saw / decided / tools called / results).
- Trap Pack released at kickoff: run the agent against it, commit the results.
  Judges will run it too. Passing everything is not required — knowing what
  happens on failure is.
- Safety bonus +4: Guardrails, Live Monitoring, Kill Switch, Audit Trail.
- No secrets in the repo (disqualification). No spam / no unsolicited messages /
  no real money without hard limits. No rebrand of an existing agent.

## Hour 0–4 — Fri Nov 27, 18:00–22:00 UTC (Sat 01:00–05:00 WIB)
- [ ] Read the full brief + scoring rubric (published Nov 26) and the Trap Pack.
- [ ] Init public repo `bangenets/fridaybrief` (MIT). Push README + this plan.
- [ ] Config schema: `config.yaml` (topics, RSS/arXiv sources, budgets).
- [ ] `watcher.py`: RSS + arXiv fetch with stdlib only (urllib + xml.etree).
- [ ] `fixtures/`: 6 mock feed items (incl. 1 with an injected instruction, for
      the firewall test) so MOCK mode works from hour 4.

## Hour 4–12 — Fri 22:00 → Sat 06:00 UTC (Sat 05:00–13:00 WIB)
- [ ] `dedupe.py`: URL + normalized-title fingerprints vs `library/index.json`.
- [ ] `library.py`: one Markdown note per item + index; never overwrites.
- [ ] `summarizer.py` (extractive): TF-IDF sentence ranking, no key needed.
- [ ] `trace.py`: JSONL trace writer (saw / decided / called / returned).
- [ ] First end-to-end mock run: fixtures → library + trace. Commit.

## Hour 12–20 — Sat 06:00–14:00 UTC (13:00–21:00 WIB)
- [ ] `__main__.py`: CLI (`--once`, `--watch`, `--mock`, `--kill`).
- [ ] `killswitch.py`: STOP file + SIGINT handler + per-run deadline.
- [ ] `monitor.py`: `runs/status.json` updated at every step (live monitoring).
- [ ] `brief.py`: Friday brief generator from the week's filed notes.
- [ ] Second mock run: full loop, trigger → brief, zero human input. Commit.

## Hour 20–30 — Sat 14:00 → Sun 00:00 UTC (21:00–07:00 WIB)
- [ ] `search.py`: Keenable web-search plug (free credits from Discord).
- [ ] `summarizer.py` (abstractive): optional OpenAI-compatible LLM call;
      falls back to extractive when no key is set. Cost logged per run.
- [ ] `firewall.py`: injected-instruction scanner (imperatives + "ignore
      previous instructions" patterns + URL exfiltration attempts). Quarantines
      the item, logs it, never executes it.
- [ ] Live run against 3 real RSS feeds + 1 arXiv category. Fix what breaks.

## Hour 30–40 — Sun 00:00–10:00 UTC (07:00–17:00 WIB)
- [ ] Run the agent against the Trap Pack. Commit `runs/trap-pack/results.md`
      with per-item outcome (blocked / flagged / passed-through + why).
- [ ] Fix the worst firewall miss; re-run. Document what still fails, honestly.
- [ ] `SAFETY.md` final: every guardrail as enforced-in-code, with file + line.
- [ ] `AGENT.md`: model + stack declaration (required by the rules).

## Hour 40–52 — Sun 10:00–22:00 UTC (17:00–05:00 WIB)
- [ ] Record the demo video (≤ 3 min): one full unattended run, trigger to
      brief, no keyboard mid-run. Show the trace and the kill switch working.
- [ ] Judge-run test: fresh clone on a clean machine, README only, time it
      (target < 15 min, mock mode, zero keys).
- [ ] README polish: exact run commands, cost statement ("$0 in mock mode").

## Hour 52–64 — Sun 22:00 → Mon 10:00 UTC (Mon 05:00–17:00 WIB)
- [ ] Buffer: fix whatever broke in the judge-run test.
- [ ] Re-run the Trap Pack once more; commit results.
- [ ] Sleep at least once. Tired code ships bugs.

## Hour 64–70 — Mon 10:00–16:00 UTC (17:00–23:00 WIB)
- [ ] Final video upload, repo public, submission form filled, every link verified.

## Hour 70–72 — Mon 16:00–18:00 UTC (23:00–01:00 WIB)
- [ ] Submit (target hour 70). Then stop touching the code. Code freeze is
      Mon Nov 30, 18:00 UTC.

## After freeze (optional, no effect on main score)
- [ ] Near Miss write-up (closes Dec 7, 18:00 UTC): the best "agent almost went
      rogue" story from the build — publish on X / Dev.to / blog, tag Hackathon
      Raptors. 3 × $100.

## Definition of done (judge's 3 checks)
1. Judge can run it: clone → README → `.env.example` → working agent < 15 min.
2. Judge can watch it work: demo video shows a real task, trigger to finish.
3. Judge can read what it did: every run leaves a trace; trap-pack results
   are committed; SAFETY.md names what is enforced in code.
