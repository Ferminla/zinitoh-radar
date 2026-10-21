# Publishing the private staging repository

Repository: `Ferminla/zinitoh-radar`.

1. Keep the repository **Private** while reviewing files.
2. Confirm root contains `README.md`, `LICENSE`, `.gitignore`, `workflow/`, `docs/`, and `examples/`.
3. Open [the public workflow template](../workflow/Zinitoh_Radar_RC3_v2_2_PUBLIC_ALPHA_TEMPLATE_INACTIVE.json) and verify that it contains no private Telegram ID, credentials, original Data Table IDs or execution data.
4. Attempt fresh installation in a separate n8n profile if time permits; otherwise clearly disclose it as untested alpha behavior.
5. Do not publish the private n8n export or manual test workflows.
6. Before publishing, inspect **git history**, not just visible files. Deleting a secret in a later commit does not make earlier public commits safe.
7. To make public: repository **Settings → General → Danger Zone → Change repository visibility → Public**. GitHub will ask for confirmation.
8. Add repository topics: `n8n`, `ai`, `rss`, `telegram-bot`, `automation`, `self-hosted`, `developer-tools`.
9. Optionally tag a release `v0.1.0-alpha`, add sanitized screenshots, and pin the repo on your profile only after the public-files review.

This release is a portfolio demonstration. Do not claim unattended reliability or broad coverage that has not yet been verified.
