# Lineage — the original engines (preserved, not shipped behavior)

These three files are the 2026 originals this repo descends from, kept
byte-for-byte as history. The shared core in `../../core/` is the fixed,
settings-driven successor — do not run these as the live system.

| File | What it was |
|---|---|
| `omnichannel_legal_service_55cfacb.py` | Omni-Channel Legal Service & Outreach Engine for OsintNeoAi — full Sep 5, 2026 version (205 lines) from commit 55cfacb: TopDownRouter, EmailCascade with reply parsing, InternetFax, CertifiedMail (Lob/Click2Mail). |
| `foia_dispatch_engine_55cfacb.py` | Anonymous FOIA Dispatch Engine for OsintNeoAi & TaxFunded — full Sep 5, 2026 version (218 lines): FOIA queue, statutory deadlines, legal-notice generation, dispatch stubs. Its dashboard face was the Centralized Public FOIA & Records Engine. |
| `fax_hardmail_dispatch_v2.py` | The one real dispatch file (21,216 B): real FaxBetter, Lob, and SMTP endpoints, BigQuery dispatch log. |

## Graded defects in the originals (fixed in the core, kept here for the record)

Documented 2026-11-16/17 by claim-by-claim grading against the repo itself:

1. **Nothing ever sent.** EmailCascade built messages and never fired them
   (smtplib imported, unused). Fax/mail "dispatches" returned success
   without touching a network.
2. **Fabricated confirmations.** Fax and mail IDs were `FAX-{md5(number)}`
   and `USPS-{md5(address)}` — invented numbers dressed as provider proof.
3. **Skipped channels in v2.** `fax_hardmail_dispatch_v2.py` is real, but
   with no `FAXBETTER_API_KEY` / `LOB_API_KEY` / SMTP env wired, every
   channel returned `skipped`. The keys were never wired in any generation.
4. **Invented recipients.** TopDownRouter guessed `director@` / `foia@` /
   `records@{agency}.gov` addresses. The core refuses unverified recipients.
