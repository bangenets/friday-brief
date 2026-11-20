# Demo video outline — FridayBrief (max 3 minutes)
# Rule: one full unattended run, trigger to finish, no human touching the
# keyboard in the middle. Record the terminal + the produced files.

## 0:00–0:25 — The job (talking head or title cards)
"Researchers drown in new papers. FridayBrief watches your sources, files what
is new, and hands you a reading brief every Friday — while you do something
else. This is one full run, start to finish, with no one touching the keyboard."

## 0:25–1:30 — The run (screen recording, real time, lightly sped up)
- Terminal: `python3 -m fridaybrief --once`
- Show the status lines as they appear: watching 4 sources → 9 new items →
  2 duplicates skipped → 1 item quarantined by the firewall (show the flagged
  injection line) → 6 filed → brief written.
- Cut to the library folder: 6 new Markdown notes with summaries.
- Cut to `runs/<date>/brief.md`: the Friday brief, top 3 reads highlighted.

## 1:30–2:15 — The trace + the kill switch
- Open `runs/<date>/trace.jsonl`: "every step is logged — what it saw, what it
  decided, which tool it called."
- Start a second run, create the STOP file mid-run: "one action stops
  everything, immediately, mid-run." Show the clean shutdown line in the trace.

## 2:15–2:50 — Cost + close
- "Mock mode costs zero dollars and zero keys. With a key, each run is capped
  at ten cents. It only reads the internet and writes to its own folder — it
  cannot delete, message, or spend anything."
- End card: repo URL, track (T3 Research & Study), "built in 72 hours".

## Recording checklist
- [ ] One continuous take for the run itself (no cuts mid-run)
- [ ] Show the quarantined injection item on screen (proves the firewall)
- [ ] Show the kill switch working (STOP file → clean stop)
- [ ] Keep it under 3:00 (aim ~2:45)
- [ ] Upload unlisted to YouTube; link in the submission
