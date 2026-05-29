# 📧 AI Email Classifier & Triage Automation

> Real-time Gmail monitoring — every incoming email is automatically classified by GPT-4 into Refund or Inquiry, then logged to Google Sheets for team action.

## What It Does

1. Monitors Gmail inbox every minute for new emails
2. GPT-4 reads the email and classifies it as **Refund** or **Inquiry**
3. Extracts: customer name, subject, category, and a 2-3 sentence summary
4. Logs everything automatically to a Google Sheet dashboard

## Workflow Architecture

```
Gmail Trigger (polls every minute)
      │
      ▼
GPT-4 Classification
      │  Prompt: "Classify as Refund or Inquiry"
      │  Returns JSON: { name, subject, category, summary }
      ▼
Parse & Structure Fields
      │
      ▼
Google Sheets → Append Row ✅
(name | subject | category | summary)
```

## Classification Logic

| Category | Trigger Keywords | Action |
|---|---|---|
| **Refund** | Cancel order, get refund, return product | Logged → Support team notified |
| **Inquiry** | Product info, beauty/makeup questions | Logged → Sales team notified |

## Nodes Used

| Node | Purpose |
|---|---|
| Gmail Trigger | Polls inbox every minute |
| OpenAI (GPT-4) | Classify + extract structured data |
| Set Fields | Parse JSON response |
| Google Sheets | Append classified row to dashboard |

## Setup Instructions

1. Import `email_classifier.json` into your n8n instance
2. Connect your **Gmail account** via OAuth2
3. Connect your **Google Sheets account** via OAuth2
4. Create a Google Sheet with columns: `name`, `subject`, `category`, `summary`
5. Update the Sheet ID in the Google Sheets node
6. Add your **OpenAI API key**
7. Activate the workflow

## Google Sheets Output Example

| name | subject | category | summary |
|---|---|---|---|
| Sarah M. | Order #4521 | Refund | Customer wants to cancel and get a refund for a foundation that caused irritation. |
| Unknown | Question about serums | Inquiry | Customer asking about the difference between Vitamin C and retinol serums. |

## What I Learned
- Building event-driven automations with polling triggers
- Structured JSON extraction from unstructured email text using LLMs
- Integrating Google Workspace APIs (Sheets, Gmail) in n8n
- Designing prompts that return consistent, parseable output

## Tech Stack
`n8n` · `OpenAI GPT-4` · `Gmail API` · `Google Sheets API`
