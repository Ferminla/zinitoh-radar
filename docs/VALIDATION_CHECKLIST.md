# Pre-publication validation checklist

## Validated in the author's instance

- [x] RSS ingestion from three configured AI sources
- [x] Local RC3 v2.2 relevance gate against real events
- [x] Controlled manual full pipeline queued its own digest and sent to Telegram
- [x] All three selected event records confirmed `delivery_status: sent`
- [x] Isolated repeated real-news test blocked the same digest ID
- [x] Manual test disarmed
- [x] Main workflow timezone corrected to `Africa/Lagos`
- [x] One unattended recovery heartbeat observed
- [x] MIT license and private-identifier-free public workflow candidate included

## Not yet validated — do not silently claim success

- [ ] A fresh n8n **2.27.3** installation of all 28 blank-selector Data Table nodes
- [ ] Main organic scheduled scan → pending outbox → unattended heartbeat delivery
- [ ] Two successive 15-minute heartbeat executions
- [ ] Later live scan verifies already-sent events are not selected
- [ ] Actual source failure, backoff and recovery in main workflow
- [ ] Genuinely empty RSS response, skipped retry, ambiguous `sending` state
- [ ] n8n host restart, laptop sleep/resume and Docker auto-start
- [ ] Public repository manual review and no secrets in **any commit history**
- [ ] Broader Crypto and AI×Crypto sources before claiming that scope

Release only with limitations visible in README and [release status](RELEASE_STATUS.md). Keep the private n8n export, test JSONs and execution traces out of GitHub.
