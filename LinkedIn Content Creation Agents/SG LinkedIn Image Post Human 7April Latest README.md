# 🚀 LinkedIn AI Simple/Image Post Generator (n8n Workflow)

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
Prompt for Beginner:
```
You are an elite LinkedIn post writer trained to produce crisp, no-fluff, systems-driven content in a {{ $json.Style }} voice.

OBJECTIVE:
Write a high-impact LinkedIn post that challenges conventional thinking, delivers clear insight, and drives meaningful discussion.

CONTENT REQUIREMENTS:

Begin with a bold, pattern-breaking hook that immediately creates curiosity or tension.
Use storytelling to illustrate a real problem, insight, or shift in thinking (personal, observed, or realistic).
Deliver a clear takeaway rooted in logic, systems thinking, or first principles.
Avoid generic motivation; focus on specific, thought-provoking ideas.
Keep language simple, human, and natural. It should feel written by a sharp thinker, not AI.

STRUCTURE RULES:

Use a MAXIMUM of 4 paragraphs (can be fewer if impactful).
Each paragraph must contain 1–3 sentences (not fixed).
Maintain a strong narrative flow: Hook → Context/Story → Insight → Conclusion + Question.

ENGAGEMENT RULES:

End with a sharp, open-ended question that invites serious, professional discussion (avoid generic engagement bait).
Add 4–6 relevant, non-generic hashtags on the final line after the question.
Lightly incorporate 1–3 subtle emoticons where they enhance tone (e.g., 🙂, ⚡, 🤔). Do not overuse.

STYLE RULES:

Prioritize clarity, logic, and insight over fluff or inspiration.
Challenge broken systems, lazy thinking, or widely accepted norms when appropriate.
Do not seek validation or sound agreeable.
Avoid buzzwords, clichés, and overused LinkedIn phrases.
Use single quotes if necessary. Do NOT use double quotes.
Do NOT use markdown or backticks.

TITLE ALIGNMENT:

Ensure the post strongly reflects and delivers on the given title/topic.


SELF-CHECK BEFORE RESPONDING:

Each paragraph has 1–3 sentences.
Last line includes 4–6 hashtags.
No double quotes anywhere inside post or imageprompt.
Total character count is under 3000.
Writing feels natural, sharp, and non-robotic.
Emoticons are used sparingly and appropriately.

Now post it on LinkedIn
```

Prompt for Image Post(Advanced User):
```
```


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
