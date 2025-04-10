# Srimanth-Voice-AI-Agent
Srimanth is a voice AI Agent that calls leads from the company database to enquire more about their requirements

Here’s a polished GitHub README.md tailored for your **n8n workflows** integrated with **VAPI.ai** and **Airtable**. You can copy this into your project’s README on GitHub:

---

# 📞 n8n + VAPI.ai Outbound Call Automation

This repository contains two `n8n` workflows:
- **My_workflow**: Periodically checks for customers with `"TBC"` status and triggers an outbound call via VAPI.ai.
- **My_workflow_2**: Listens to `end-of-call-report` webhooks from VAPI, stores call metadata in Airtable, evaluates if the call was successful, and conditionally retries or updates status accordingly.

---

## 🚀 Features

### ✅ Workflow 1: Periodic Call Trigger
- Triggered on a schedule (e.g., every few minutes).
- Pulls up to 10 leads from Airtable where `Status == "TBC"`.
- Calls them using VAPI.ai (Assistant ID & Phone ID configured).
- Updates status to `In Progress`.

### ✅ Workflow 2: Webhook & Post-Call Logic
- Triggered via VAPI.ai's `end-of-call-report` webhook.
- Logs full call data (duration, cost, recording, etc.) into Airtable.
- If call was answered:
  - Marks as `Called` with transcript summary.
- If voicemail or failed:
  - Waits 1 minute and retries (up to 2 times).
  - On repeated failure, marks as `#Unreachable`.

---

## 🔧 Setup Instructions

### Prerequisites
- [n8n](https://n8n.io) self-hosted or cloud instance
- [Airtable API Token](https://airtable.com/account)
- [VAPI.ai](https://vapi.ai) Assistant & API key

### Airtable Structure

You need **two tables** in your base or you can use the template given in the repo:
- `Table 1`: Stores lead/customer information
- `Table 2`: Stores raw call logs

Make sure the tables include the following fields:
- `Mobile`, `First Name`, `Status`, `Attempts`, `Summary`, `Date Time`, `id` (unique record identifier).

### VAPI Setup

- Create an Assistant on [VAPI.ai](https://app.vapi.ai).
- Retrieve:
  - `Assistant ID`
  - `Phone Number ID`
  - `API Token`

---

## 📂 Files

| File | Purpose |
|------|---------|
| `My_workflow.json` | Scheduled trigger + outbound call via VAPI |
| `My_workflow_2.json` | Webhook receiver + Airtable update logic |

---

## 🧩 How to Use

1. Import the JSON files into your n8n editor:
   - `Settings > Import Workflow`
2. Set credentials:
   - Airtable Personal Token
   - VAPI Authorization Bearer Token
3. Publish and activate the workflows.

---

## 📈 Use Cases

- Automated call campaigns
- Lead follow-ups
- Reminder calls with transcription
- Multi-attempt call retries with smart fallback

---

## 🛡️ Security Notes

- Make sure to secure your n8n instance and VAPI API keys.
- Use `.env` or secure credential storage for tokens.

---


## 🤝 Credits
Powered by `n8n`, `VAPI.ai`, and `Airtable`

---

Let me know if you'd like this exported as a `README.md` file or want a diagram for the workflow as well!
