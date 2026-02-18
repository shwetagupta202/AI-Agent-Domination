# 🤖 Telegram Lead Qualification AI Agent (n8n)

This workflow turns your **Telegram bot into an intelligent lead qualification assistant** using **AI + memory + BANT framework**, and automatically stores qualified leads in **Google Sheets**.

---

## 🚀 What This Workflow Does

1. Listens to incoming Telegram messages  
2. Collects lead details conversationally  
3. Qualifies leads using **BANT (Budget, Authority, Need, Timeline)**  
4. Scores the lead automatically  
5. Stores qualified leads in Google Sheets  
6. Sends intelligent replies back to the user  

---

## 🧩 Workflow Architecture

```
Telegram User
   ↓
Telegram Trigger
   ↓
AI Agent (Gemini / OpenRouter)
   ↓
Memory (Conversation Context)
   ↓
IF Lead Complete?
   ├─ Yes → Save to Google Sheets + Confirmation
   └─ No  → Ask Next Question
```

---

## 🛠️ Prerequisites

- n8n (Cloud or Self-hosted)
- Telegram Bot Token
- Google Sheets OAuth
- Google Gemini API or OpenRouter API

---

## 📥 Import Workflow

1. Open n8n  
2. Go to **Workflows → Import**  
3. Upload `SG_Telegram18FebOptimized.json`  
4. Save and activate the workflow  

---

## 🔐 Credentials Setup

### Telegram Bot
Create a bot using **@BotFather** and add the token in n8n Telegram credentials.

### Google Sheets
Create a sheet with columns:
```
Name | Email | Budget | Timeline | Decision Maker | Lead type | Score | Reasoning | Next Steps
```

Connect Google Sheets OAuth to the workflow.

### AI Model
Use either:
- Google Gemini  
- OpenRouter (recommended)

---

## 🧠 AI Prompt (Core Logic)

```
You are a friendly sales assistant collecting lead information via Telegram
and qualifying leads using BANT criteria.

Ask one question at a time.
Store memory using chat.id.
If all details are collected, mark conversation as complete.
```

---

## 💬 Sample Conversation

```
User: Hi
Bot: What's your email address?
User: user@email.com
Bot: What's your budget?
A) Under $1,000
B) $1,000–$5,000
C) $5,000+
```

---

## 📊 Google Sheet Output

Each completed lead is automatically saved with:
- Lead score
- Qualification status
- Reasoning
- Next steps

---

## 🎯 Use Cases

- AI Agencies
- Coaches & Consultants
- SaaS Startups
- Freelancers
- Telegram Communities

---

## 🔁 Customization Ideas

- Add Calendly booking
- Push to CRM
- WhatsApp follow-ups
- Supabase instead of Sheets

---

## ✅ Status

Production-ready, scalable, and beginner-friendly.
