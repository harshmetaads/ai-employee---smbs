# AI Employee: Lead Qualifier Automation (n8n, free setup)

Flow: Chat/website -> Webhook -> Score (HOT/WARM/COLD) -> Google Sheet row -> Telegram alert if HOT -> reply.

## 1. Google Sheet (2 min)
1. Create a Google Sheet, rename the first tab to `Leads`.
2. Put these headers in row 1, exactly:
   `Time | Name | Phone | Need | Budget_Lakh | Timeline_Months | Payment | Site_Visit | Score | Class | Reason | Next_Action`
3. Copy the Sheet ID from the URL (the long text between `/d/` and `/edit`).

## 2. Telegram alert (3 min, free)
1. In Telegram, open @BotFather, send `/newbot`, copy the bot token.
2. Send any message to your new bot, then open `https://api.telegram.org/bot<TOKEN>/getUpdates` and copy `chat.id`.
3. WhatsApp alerts need the WhatsApp Cloud API (business verification), so use Telegram for the demo.

## 3. n8n
1. Use n8n Cloud free trial, or run it free yourself: `npx n8n`.
2. Workflows -> Import from File -> choose `n8n/ai-employee-lead-workflow.json`.
3. Open "Save to Google Sheet": connect your Google account, paste the Sheet ID.
4. Open "Alert Salesperson (Telegram)": add the bot token credential, paste the chat id.
5. Activate the workflow and copy the Production URL of "Lead Webhook".

## 4. Test it
Run this (replace the URL):

```
curl -X POST "YOUR_WEBHOOK_URL" -H "Content-Type: application/json" \
  -d '{"name":"Demo Customer","phone":"9000000000","bhk":2,"budget_lakh":55,"timeline_months":1,"finance":"Loan pre-approved","visit":true}'
```

Expected: a new row in the sheet, class HOT, score 100, and a Telegram message.

## 5. Connect the chat
The demo page collects the same six answers. For the real bot, make the chat (or a Tally/Google Form) POST those fields to the webhook above.

## Notes
- Scoring rules are in the "Score Lead" node and match the demo page. Edit them there.
- The workflow is untested against your accounts; credentials are placeholders you fill in.
- Next upgrade: add an AI node (Gemini free tier or OpenAI) so the chat itself is AI-driven instead of scripted.
