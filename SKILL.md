# 束ねる作法 (Tabaneru) — File-Based Thread Orchestration

Run many disposable sub-threads ("糸", threads) without losing their work. The centre of the bundle is not chat management; it is file management. Threads are disposable reading-and-writing mouths. State, harvest and handover all live in files, so the next hand starts by reading files — never by hoping a chat context survived.

## When to use

- You delegate work to side chats or subagents and their results keep evaporating into chat history.
- Several threads run in parallel and their outputs mix, contradict or get lost.
- A thread ends (task done, context full, session replaced) and its successor must pick up exactly where it left off.

## Principles

- **Files are the centre.** A thread's chat context is not a record and not a memory store. If it is not in a file, it did not happen.
- **Threads are disposable.** A thread having a lifespan is not a defect. When it ends, it leaves a handover file; the work continues because the files remain.
- **One job, one folder.** Each thread gets exactly one workspace folder and writes only inside it. The coordinator (main) is the only one who writes across folders.
- **Never delete; fold.** （消さない。畳む。) Finished threads are marked folded in the index and left in place. Errors, dead ends and empty results stay on record; corrections are appended as new lines, never edited into old ones.
- **The canon is separate.** Thread folders hold working records and harvests. They become part of the user's long-term memory only when the coordinator verifies and promotes them.

## Layout

```
threads/
  INDEX.md            — one line per thread, in time order
  <thread-name>/
    状態.md (state)      — what this thread is doing now, progress, decisions waiting
    収穫.md (harvest)    — what the thread produced, appended at milestones
    引き継ぎ.md (handover) — written by the coordinator when the thread folds
    ...working files stay in the same folder
```

- Every file in a thread folder opens with a 4-line index: `date` / `time` (measured only; write "not measured" rather than guessing) / `people` (never inferred) / `tags`.
- INDEX.md lines carry only: date, thread name, job, state （稼働中 active / 畳んだ folded), and a pointer to the handover file. Folded lines are never removed.

## The handover file

Written by the coordinator when a thread folds, and at milestones for long-lived threads. Fields:

- **糸 (Thread)** — name and job, one line
- **期間 (Period)** — start and end, measured times only
- **済んだこと (Done)** — completed work and where the deliverables live
- **収穫 (Harvest)** — what this thread produced and where it was placed in the house
- **未済・持ち越し (Carried over)** — unfinished items the next hand must pick up
- **判断待ち (Waiting on decisions)** — open branch points, and whose decision each one is
- **逐語 (Verbatim)** — only words that serve as evidence: decisions, permissions, verifications, choices — each with its source (who, when)
- **次の手へ (For the next hand)** — warnings: phrasings that failed, things not to touch, the other party's state
- **不在の開示 (Disclosed absences)** — what was lost, what could not be obtained, where the harvest is zero

A successor thread starts by reading: (1) the relevant pages of the canon, (2) the handover file, (3) then opens a fresh state file and begins.

## Harvest rules

- Append to 収穫.md at milestones, before reporting. File first, report second.
- Granularity: what the next decision needs — not a play-by-play.
- Verbatim is reserved for evidence (decisions, permissions, verifications, choices). Everything else is summary, with sources named.
- Zero is a result: if a thread produced nothing, write one line saying so. An absence of inheritance is a state to disclose, not a failure to hide.

## Reporting

A thread reports to the coordinator at four milestones only: (1) the job is complete, (2) a branch point needs a decision, (3) an anomaly (stopped, something is wrong, a permission is needed), (4) a harvest contradicts an existing page of the canon. No play-by-play progress reports.

Threads do not talk to each other directly. They may read each other's folders; exchange happens through files and the coordinator.

## Notes

This method grew out of the Yohaku alliance's continuity practice: an orchestrator running side threads whose contexts are compacted or replaced, where the only continuity that survives is what was written down. It pairs with a verification step (see the kenpin skill) before a harvest is promoted into the canon.
