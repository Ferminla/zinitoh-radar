# Security and operational limitations

This is an **inactive, sanitized workflow template**, not an export of the author's running instance. Table selectors are blank, the Telegram credential is not bundled, the recipient is a placeholder, and Telegram and optional paid model scoring start disabled.

- **Never commit your configured private export** after adding a chat ID or n8n credentials.
- The optional OpenAI HTTP Request node is **disabled**: enabling it needs a separate credential, cost approval, and runtime testing.
- The author tested ordinary serial duplicate suppression, not exactly-once delivery. A Telegram send and its Data Table receipt are not one atomic transaction. If a message may have arrived but the outbox is still `sending`, reconcile Telegram first; never blindly resend.
- Avoid activating several copies against the same tables. Run guards are not a proved atomic multi-worker lock.
- Relevance and event clustering are predominantly headline-based, with known false negatives and occasional split events.
- RSS is not social trend detection. A reporting-source count is not independent proof of a claim.
- Local laptop sleep or shutdown stops n8n. Recovery uses a maximum 48-hour RSS catch-up and chooses the most recent due scan slot, not all missed slots.
- Organic unattended scheduled delivery, new-instance portability, concurrency, crash recovery, true empty-feed behavior, and comprehensive Crypto and AI×Crypto feeds have not yet been validated.

Read [release status](RELEASE_STATUS.md) and [validation checklist](VALIDATION_CHECKLIST.md) before enabling the workflow.
