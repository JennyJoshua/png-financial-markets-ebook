# Perplexity Research Automation Setup

This repository uses a manually triggered GitHub Actions workflow to ask Perplexity for research and save the result under `docs/research/`.

## Before the first run

1. **Check Perplexity API access and billing.** A Perplexity website subscription does not automatically include API credits. Review the current official API documentation and pricing before enabling API usage:
   - https://docs.perplexity.ai/
   - https://www.perplexity.ai/api-platform
2. In the GitHub repository, open **Settings → Secrets and variables → Actions → New repository secret**.
3. Add a secret named `PERPLEXITY_API_KEY` containing your Perplexity API key. Never put the key in a workflow file, report, issue, or chat.
4. To receive Discord notifications, add `DISCORD_WEBHOOK_URL` as another repository secret. Secrets in other repositories are not automatically shared. The workflow still runs if this secret is absent, but it skips Discord notification.
5. Open **Actions → Perplexity Research → Run workflow**.
6. Enter the research question, choose quick or detailed, and run it. Review the result in `docs/research/` and the Actions run log.

## What the workflow does

- Runs only when manually triggered; it does not run on a schedule.
- Uses Perplexity's Sonar API endpoint for web-grounded answers.
- Saves a timestamped Markdown report and commits that report to the repository.
- Sends a Discord success/failure notification if `DISCORD_WEBHOOK_URL` is configured.
- Does not edit eBook chapters, research masters, requirements, or other project files.
- Treats reports as unapproved research inputs. Important claims must be checked against their underlying sources before use.

## Cost and safety

The API may incur charges depending on the account, model, and request. Start with short, focused questions and the quick option. Do not run it until you have checked the account's API pricing and billing controls. The workflow limits the question to 2,000 characters and each run to 10 minutes.

## Troubleshooting

- **Missing API key:** add the `PERPLEXITY_API_KEY` repository secret.
- **HTTP 401/403:** verify API key and API access/billing.
- **HTTP 429:** check rate limits and available credits.
- **No Discord alert:** confirm `DISCORD_WEBHOOK_URL` exists as a secret in this repository and is a valid Discord webhook URL.
- **No report committed:** open the workflow run and read the failed step. A failed research request does not create or approve a report.
