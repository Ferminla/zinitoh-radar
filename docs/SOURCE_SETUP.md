# RSS source setup

`radar_sources` is an installer-managed registry; source rows are not bundled with the exported workflow.

A documented source example (verify that the feed still works when installing):

| Field | Example |
| --- | --- |
| `source_id` | `techcrunch_ai` |
| `name` | `TechCrunch AI` |
| `category` | `AI` |
| `source_type` | `rss` |
| `url` | `https://techcrunch.com/category/artificial-intelligence/feed/` |
| `enabled` | `true` |
| `consecutive_failures` | `0` |
| `last_attempt_at`, `last_success_at`, `next_retry_at`, `last_error` | Empty String |

Create a stable unique `source_id` per RSS feed. Confirm URLs and timestamps with a standalone RSS Feed Read node before enabling. The author also validated OpenAI News and Hugging Face Blog, but their exact source URLs are not bundled in the public export. Do not invent endpoints. Avoid noisy changelog feeds until relevance qualification is verified.

Three AI feeds were validated in the author's installation; enabled Crypto and AI×Crypto coverage has not been demonstrated.
