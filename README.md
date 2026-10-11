# AI Employee for SMBs

A prototype of an AI employee for small businesses. It reads a customer enquiry, extracts the details, scores the lead as HOT, WARM or COLD, saves a CRM row and drafts an alert for the owner.

**Status:** working prototype. No customers or revenue are claimed.

## What is in this repo

- `index.html`: the pipeline demo page (single file, no build step). Open it in a browser to run the recorded demo for four business types (real estate, clinic, coaching, salon).
- `n8n/ai-employee-lead-workflow.json`: a starter n8n workflow (Webhook, scoring Code node, Google Sheets append, IF, Telegram alert, response). Credentials are placeholders. It is a reference, not a tested production workflow.
- `docs/automation-setup.md`: setup steps for the Sheet, Telegram bot and n8n import.

## Lead scoring (out of 100)

| Signal | Points |
| --- | --- |
| Budget stated | 25 |
| Timing: within 7 days / 30 days / later | 30 / 20 / 10 |
| Readiness: ready / exploring | 20 / 10 |
| Agrees to a visit, demo or appointment | 25 |

HOT is 70 or more, WARM is 40 or more, otherwise COLD.

## Live mode

The same page, published as a Claude artifact, can call a live AI to read any message and, with the Google Sheets and Gmail connectors allowed, write a real Sheet row and send a real email alert. Outside Claude only the recorded demo runs. To use your own sheet, replace `YOUR_GOOGLE_SHEET_ID` in `index.html`.

## n8n tip

If the IF node always goes to false after a Google Sheets node, read the field from the scoring node explicitly, for example `{{ $('Score Lead').item.json.Class }}`, because the Sheets node replaces the item data.

## Author

Harsh Pratap Singh
