# FU FOIA — Anonymous

**FU FOIA** is the Follow-Up FOIA system: it takes a reason for contact, keeps it **verbatim** (hash-locked), and follows up on a **60-minute escalation ladder** across email, internet fax, and certified hard mail — records officer first, director's office CC'd top-down, replies parsed to chain to the actual human.

This repo is the **Anonymous** edition, for investigators and users of the **OsintNeoAi user workspace**:

- Sends as the **OsintNeoAi Public Records & Journalism Legal Unit** (`records@osintneoai.org`). No personal name, phone, or address appears on anything.
- Nothing is sent without the operator approving the exact copy (approval is bound to the hash of the approved text).

> **MAINTAINERS — OWNER RULE:** This repo is worked on **only by agy and IntelliJ IDEA**, the same as the OsintNeoAi website itself. Neo set it up on 2026-11-18 at the owner's order and does not work in this repo after setup. Core updates arrive by deliberate pull from the Public edition's tagged core versions (see `SYNC.md`) — never automatically, never by another agent's push.

The other edition is [FUFOIA-Public](https://github.com/Tonypost949/FUFOIA-Public) — the owner's signed personal edition.

## Run it

```
python3 core/outreach_engine.py --case cases/template_case.json --channel-check
python3 core/outreach_engine.py --case cases/<case>.json --all-levels --dry-run
python3 core/outreach_engine.py --parse-reply "<reply text>"
```

Dry-run is the default; the engine builds approval-ready drafts and sends nothing itself. Fax (FaxBetter) and certified mail (Lob) return an honest `skipped_no_key` until an operator wires their own paid account — no confirmation or tracking number is ever fabricated, and no recipient address is ever invented (unverified recipients block the draft).

## Layout

- `core/outreach_engine.py` — the FU FOIA core (see `CORE_VERSION`)
- `settings.json` — the Anonymous settings (unit identity + ladder + channels)
- `cases/` — start from `cases/template_case.json`
- `original/` — the 2026 original engines (Omni-Channel Legal Service & Outreach Engine, Anonymous FOIA Dispatch Engine, fax_hardmail_dispatch_v2), preserved byte-for-byte with their graded defects in `original/LINEAGE.md`
- `ARCHITECTURE.md`, `SYNC.md`
