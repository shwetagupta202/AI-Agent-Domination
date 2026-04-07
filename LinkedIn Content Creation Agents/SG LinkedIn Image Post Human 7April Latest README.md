# 🚀 LinkedIn AI Image Post Generator (n8n Workflow)

This n8n workflow automates the creation and publishing of high-quality LinkedIn posts with AI-generated content and images, including a human approval step.

---

## 📌 Overview

This workflow helps you:

- Generate LinkedIn posts using AI (based on your idea + style)
- Automatically create a matching image using AI
- Add a human approval step before posting
- Publish directly to LinkedIn with image

---

## 🧠 Use Cases

- Personal branding on LinkedIn (daily content)
- Coaches & creators building authority
- Automating content marketing for businesses
- AI-powered social media management
- Content teams needing approval workflows

---

## ⚙️ Workflow Architecture

Form Input → AI Content Generation → Human Approval → Image Generation → LinkedIn Post

---

## 🔁 Step-by-Step Flow

### 1. Form Trigger (Input Collection)
- Node: `On form submission`
- Collects:
  - **Post Idea**
  - **Style** (Funny / Contrary / Informative)

---

### 2. AI Agent (Content Generation)
- Node: `AI Agent`
- Uses:
  - Google Gemini model
  - Structured output parser

**Output:**
{
  "post": "LinkedIn post content",
  "prompt": "Image generation prompt"
}

---

### 3. Human-in-the-Loop Approval
- Node: `Gmail (sendAndWait)`
- Sends generated post to your email
- Waits for approval before proceeding

---

### 4. AI Image Generation
- Node: `HTTP Request (Hugging Face)`
- Model: FLUX.1-schnell

---

### 5. LinkedIn Post Publishing
- Node: `LinkedIn`
- Posts:
  - Text content
  - AI-generated image

---

## 🔐 Credentials Required

- Google Gemini API
- Gmail OAuth2
- LinkedIn OAuth2
- Hugging Face API Token

---

## 🛠 Setup Instructions

1. Import the workflow JSON into n8n
2. Configure all credentials
3. Add your Hugging Face API key
4. Activate the workflow
5. Use the form webhook to start

---

## 💡 Suggested Enhancements

- Store 30 content ideas in Google Sheets
- Auto-run daily using Cron
- Track post status
- Multi-platform publishing

---

## 🎯 Who Should Use This?

- Coaches
- IT professionals
- AI automation enthusiasts
- Content creators

---

## 🧠 Final Thought

This is not just a workflow.

It’s a content system.
