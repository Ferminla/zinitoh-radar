# Required n8n Data Tables

Create all five tables before importing or binding the workflow. Timestamps and error fields use **String** (ISO-8601 values); `event_uids` is a JSON array encoded as a String. These types came from tested workflow mappings, not a fresh install.

| Table | Columns (type) |
| --- | --- |
| `radar_sources` | `source_id` String, `name` String, `category` String, `source_type` String, `url` String, `enabled` Boolean, `last_attempt_at` String, `last_success_at` String, `consecutive_failures` Number, `next_retry_at` String, `last_error` String |
| `radar_runs` | `run_id` String, `run_type` String, `intended_slot` String, `started_at` String, `status` String, `claim_token` String, `completed_at` String, `error_summary` String, `sources_attempted` Number, `sources_succeeded` Number, `sources_failed` Number, `sources_skipped` Number, `items_found` Number, `items_new` Number, `events_created` Number, `signals_selected` Number |
| `radar_items` | `item_uid`, `source_id`, `external_id`, `title`, `url`, `canonical_url`, `excerpt`, `published_at`, `fetched_at`, `content_hash`, `status`, `filter_reason`, `filtered_at`, `category`, `event_uid`: all String |
| `radar_events` | `event_uid`, `canonical_title`, `title_fingerprint`, `category`, `first_seen_at`, `last_seen_at`, `primary_source_url`, `status`, `delivery_status`, `radar_reason`, `why_it_matters`, `what_happened`: String; `source_count`: Number |
| `radar_outbox` | `digest_uid`, `run_slot`, `digest_text`, `event_uids`, `status`, `next_retry_at`, `created_at`, `sent_at`, `last_error`, `telegram_message_id`: String; `attempts`: Number |

The four legacy run metrics `items_found`, `items_new`, `events_created`, and `signals_selected` were observed as null and must not be represented as populated analytics.

**Binding:** The public JSON intentionally has blank selectors for all **28 Data Table nodes**. Select the table corresponding to each node's named operation, then recheck filter and mapping fields. Never import the author's private source, event, or outbox rows.
