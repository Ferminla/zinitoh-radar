# Release status — 2026-10-21

**Version:** v0.1.0-alpha candidate (not yet tagged).  
**Environment observed:** locally hosted n8n **2.27.3**, main workflow timezone corrected to `Africa/Lagos`.  
**Scope:** self-hosted RSS-to-Telegram AI intelligence alpha, not a production-grade always-on service.

## Observed and confirmed

- Three AI RSS sources successfully ingested in earlier runs.
- RC3 v2.2 relevance test: 32 considered / 3 selected / 29 excluded.
- Controlled genuine manual full-pipeline test: 31 considered / 3 selected, RSS → clustering → relevance → outbox → Telegram message #8. Author saw it arrive and verified all three relevant events marked `sent`.
- Separate real-news manual outbox test: one message delivered and receipt persisted, second same-UID execution blocked.
- One autonomous heartbeat observed at 04:45 WAT on October 21; `Recovery Wake` returned `wake_type: heartbeat`.

## Still unverified

- Clean installation of the blank-table public template and full rebinding in n8n 2.27.3.
- Organic unattended scheduled RSS scan plus Telegram dispatch, repeated heartbeat cadence.
- Later real scan excluding all previously sent events.
- Restart/retry/concurrency behavior and ambiguous `sending` recovery.
- Comprehensive Crypto or AI×Crypto feed coverage.

These limitations are deliberate, explicit alpha disclosures.
