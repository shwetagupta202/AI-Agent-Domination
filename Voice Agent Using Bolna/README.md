# AI Voice Calling Agent – n8n + Bolna + Google Sheets

This repository contains an **automated outbound AI voice calling workflow** built using **n8n**, **Bolna Voice AI**, **Google Sheets**, and **LLMs (Gemini / OpenRouter)**.

The system automatically:
- Reads pending leads from Google Sheets
- Triggers AI voice calls
- Fetches call transcripts
- Uses AI to summarize the conversation
- Updates the same Google Sheet with call status and summary

---

## 🧠 Use Case

This voice agent is ideal for:
- Webinar confirmations & follow-ups  
- Lead qualification calls  
- Workshop onboarding calls  
- Automated sales or support outreach  
- AI calling demos

---

## 🏗️ Architecture Overview

**Tech Stack**
- **n8n** – Workflow orchestration  
- **Bolna AI** – Voice calling & transcription  
- **Google Sheets** – Lead source & result storage  
- **LLMs**
  - OpenRouter (LLaMA-3) – Data extraction  
  - Google Gemini – Structured output parsing  

---

## 🔁 Workflow Flow

1. **Manual Trigger** – Start workflow from n8n  
2. **Google Sheets** – Fetch rows where `status = pending`  
3. **Limit Node** – Control call volume  
4. **Bolna API Call** – Initiates outbound voice call  
5. **Store Execution ID** – Saves call execution reference  
6. **Fetch Transcript** – Retrieves call transcript from Bolna  
7. **IF Logic** – Checks call status (completed / busy / dropped)  
8. **AI Agent** – Extracts structured summary from transcript  
9. **Update Sheet** – Writes status, execution ID, and summary back

---

## 📄 Google Sheet Structure

| Column Name   | Description |
|--------------|------------|
| First name | Lead name |
| phone number | Without country code |
| status | pending / completed / dropped |
| execution ID | Bolna execution ID |
| Summary | AI-generated call summary |
| row_number | Auto-generated |

---

## 🔐 Credentials Required

- Google Sheets OAuth
- Bolna API Key (HTTP Header Auth)
- OpenRouter API Key
- Google Gemini API Key

---

## 🌍 Webhooks

Bolna callback URL:
```
https://n8n.coachshwetagupta.com/webhook/bolna-callback
```

---

## ⚠️ Notes

- Designed for **sequential calling**
- Phone numbers must be valid
- Uses static execution ID storage in n8n
- Not intended for high-volume call blasting

---

## 🚀 Future Enhancements

- Retry logic for unanswered calls
- CRM integrations (Zoho / HubSpot / Salesforce)
- WhatsApp follow-ups
- Sentiment analysis
- Cost analytics dashboard

---

## 👩‍💻 Author

**Shweta Gupta**  
AI Automation & Voice Agent Coach  

---

## 📜 License

For educational and internal automation use.
