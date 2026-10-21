# Zinitoh Radar — Self-hosted RSS intelligence for AI builders

**Release status:** v0.1.0-alpha candidate. Manual end-to-end delivery validated on the creator’s instance; fresh-install compatibility and unattended delivery are still being tested. See [release status](docs/RELEASE_STATUS.md).

Zinitoh Radar is a self-hosted RSS intelligence workflow for builder-relevant developments. It collects news via RSS, normalizes and groups articles into events, qualifies events using a local rule-based relevance gate, generates a Telegram digest and persists delivery state for ordinary duplicate suppression and retry.

## Compatibility and scope

- **Observed testing environment:** n8n **2.27.3** in the creator's existing self-hosted instance. Other versions have **not** been validated.
- Built-in n8n nodes: Schedule Trigger, RSS Feed Read, Data Table, Code, If, Loop Over Items, Telegram; optional HTTP Request.
- Default cost: OpenAI scoring is **disabled**. Infrastructure, hosting, electricity and connectivity may still cost money.
- Six Lagos scan slots: 09:00, 12:00, 15:00, 18:00, 20:00, 23:00; heartbeat every 15 minutes while active and online.
- Covers **only the RSS sources the installer enables**. The creator validated three AI sources (OpenAI News, Hugging Face Blog, TechCrunch AI) in their own database. Broad crypto and AI×crypto coverage has **not** been demonstrated.
- Not X/Twitter trend measurement; no audience/social velocity data, Sheets watchlists or Content Intelligence integration.

## Installation — manual n8n Data Table binding required

1. Run n8n on a **supported, persistent host**, configure its timezone and clock. The included workflow sets `Africa/Lagos` explicitly, and uses Lagos clock calculations; verify actual schedule timing in your installation.
2. Create **five Data Tables** using [`docs/DATA_TABLE_SCHEMAS.md`](docs/DATA_TABLE_SCHEMAS.md): `radar_sources`, `radar_runs`, `radar_items`, `radar_events`, `radar_outbox`. Do not import personal execution records.
3. Import `workflow/Zinitoh_Radar_RC3_v2_2_PUBLIC_ALPHA_TEMPLATE_INACTIVE.json` **as a new inactive workflow**. It contains **76 nodes**.
4. Open each **Data Table node** and select the appropriate table, based on the node's operation/columns. **All Data Table IDs are intentionally blank** to avoid leaking the author's instance identifiers. There are 28 Data Table nodes, so this step must be completed before attempting a run.
5. Seed at least one verified, accessible RSS source in `radar_sources`. Use `source_id` unique stable String, `name`, category (e.g. `AI`), `source_type`=`rss`, public RSS `url`, `enabled` Boolean; initialize failure fields to `0` / empty String. See [`docs/SOURCE_SETUP.md`](docs/SOURCE_SETUP.md).
6. Configure a private Telegram bot credential on `Send Telegram Digest — CONFIGURE CREDENTIAL`. In `Radar Runtime Config`, set the recipient ID **privately in your instance** and only set `telegram_enabled: true` when intentional. **Never commit the edited private export.**
7. Keep `openai_enabled: false`. The optional OpenAI HTTP node is **disabled** by default because it has no Bearer Auth credential; enabling it requires deliberately configuring authentication, testing the branch, and accepting API costs.
8. While inactive, execute controlled manual tests. Verify `radar_runs`, `radar_outbox` and `radar_events` directly. Resolve all errors and avoid rerunning uncertain sends. See [`docs/VALIDATION_CHECKLIST.md`](docs/VALIDATION_CHECKLIST.md).
9. Activate **one** configured main workflow only when ready; observe scan and heartbeat execution over more than one slot. Ensure the host actually stays on and n8n restarts safely.

## Digest format

```text
ZINITOH RADAR | YYYY-MM-DD HH:MM WAT
Signals: N | Sources are linked for independent verification

1. [AI] <Verified relevant headline>
   Why it matters: <Builder-focused context> | 1 reporting source(s)
   <Source URL>

Automated prioritization; verify primary sources before acting.
```

Do not fabricate a minimum number of signals. Zero qualifying events is an acceptable result.

## Architecture

`Schedule/Heartbeat → Scan Guard → RSS Ingest → Article Store → Event Dedup/Clustering → Relevance Gate → Digest → Pending Outbox → Heartbeat Telegram Dispatch → Receipt/Event Updates`.

- Per-source first lookback 24 hours, successful overlap 2 hours, maximum catch-up 48 hours.
- Event fuzzy matching is title/token based and imperfect.
- Relevance v2.2 is predominantly headline-rule based; it does not independently research or validate article contents.
- A stable digest UID prevents ordinary repeated creation for the same scan slot; delivered events are marked `sent` and excluded by the normal candidate filter.
- Telegram send and receipt persistence are **not atomic**. Exactly-once delivery cannot be guaranteed. Do **not** blindly retry an ambiguous outbox `sending` record.
- Run-claim fencing is **not an atomic multi-worker lock**; avoid multiple active workflow copies against the same tables.
- Local host shutdown/sleep prevents unattended scans. Missed scan slots collapse to the latest due slot rather than generating all historical digests.

## Validation evidence (creator's existing instance only)

- Real 3-source RSS runs observed successful.
- Real RC3 v2.2 relevance run: 32 considered, 3 selected; excluded 29.
- Controlled manual full pipeline run: 31 considered, 3 selected, queued under a distinct test slot and dispatched to Telegram (message ID confirmed by the creator), receipt persisted; all three selected events observed `delivery_status=sent`.
- Controlled standalone duplicate-delivery test blocked repeat sending of the same test digest.
- One unattended recovery heartbeat has been observed in the main workflow. **Unattended scheduled scan-to-Telegram delivery, fresh-install setup, multi-worker safety, host restart recovery and cross-version portability remain unverified**. The controlled manual success is not proof of those behaviors.

## Release safeguards

This export contains **no bot token, Telegram chat ID, credential binding, instance ID, workflow ID, original Data Table IDs, or private project URLs**. Imported workflows are inactive, and Telegram/OpenAI scoring default off. The template still requires private credential and Data Table setup.

See [`docs/SECURITY_AND_LIMITATIONS.md`](docs/SECURITY_AND_LIMITATIONS.md), [`docs/VALIDATION_CHECKLIST.md`](docs/VALIDATION_CHECKLIST.md), and [`docs/RELEASE_STATUS.md`](docs/RELEASE_STATUS.md).

**License:** [MIT](LICENSE). Copyright (c) 2026 Ferminla.