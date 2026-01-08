# Topic → Titles → Description → Script (Multi‑Agent Newsletter Workflow)
This workflow turns any user‑provided topic into a ready‑to‑publish newsletter draft through four specialized agents:
1. **Research Topics Agent**  
2. **Create Titles Agent**  
3. **Create Description Agent**  
4. **Create Script Agent**  
Plus a **Main Orchestrator Agent** that chains the steps and returns the final output.

The workflow uses **OpenRouter Chat Models (Llama 3.x instruct variants)** for each agent, ensuring consistent style and low latency across steps.

---

## Prompts to Test

### Prompt 1
```
"How is AI disrupting or benefiting IT industry"
```
(This is the default `chatInput` included for quick testing.)

### Prompt 2
```
"Generative AI in customer support for SMBs"
```

### Prompt 3
```
"Top DevOps trends for 2026 every engineering manager should know"
```

---

## How It Works

### 1) Research Topics
**Goal:** Expand and refine the user’s topic into **3–5 relevant, trending angles**.  
**System Message:** “Research and suggest 3–5 trending, relevant newsletter topics for the given input. Keep them short and clear.”  
**Notes:** Keeps suggestions concise and topical; acts as the feeder for the rest of the chain.

### 2) Create Titles
**Goal:** Generate **5 catchy newsletter titles** based on the chosen angle(s).  
**System Message:** “Generate 5 catchy newsletter titles based on the given topic(s). Keep them short, engaging, and professional.”  
**Notes:** Produces headline candidates optimized for clarity and engagement.

### 3) Create Description
**Goal:** Write a **2–3 sentence** intro for the newsletter.  
**System Message:** “Write a short, compelling description (2–3 sentences) for the newsletter based on the chosen title/topic. Make it clear and inviting.”  
**Notes:** Bridges titles to a coherent narrative hook.

### 4) Create Script
**Goal:** Produce a **250–400 word** full newsletter draft with **intro → main insight → closing**.  
**System Message:** “Write a full newsletter draft (250–400 words) based on the given topic and description. Keep the tone professional but conversational. Structure with an intro, main insight, and closing.”  
**Notes:** Finalizes the piece with a balanced tone for general professional audiences.

### 5) Main Orchestrator Agent
**Role:** Receives the user’s topic and **automatically sequences** the four specialist agents in this order:
```
Research Topics → Create Titles → Create Description → Create Script
```
**System Message (Orchestrator):**
> “You are a Newsletter Orchestrator AI. The user will provide only a topic.  
> Your job is to automatically run the full pipeline in order:  
> Research Topics → Create Titles → Create Description → Create Script  
> Always pass outputs step-by-step to the next specialist until the full newsletter is ready.”

---

## System Prompts (Used Inside n8n)

### Orchestrator Prompt
- Accept a single **topic** from the user.
- Call agents in strict order and **pass step outputs forward** until the newsletter draft is complete.
- Return the consolidated result (topics, titles, description, script).

### Agent Prompts
- **Research Topics Agent:** Suggest **3–5** concise, trending angles.  
- **Create Titles Agent:** Generate **5** concise, engaging titles.  
- **Create Description Agent:** Write **2–3 sentences** that are clear and inviting.  
- **Create Script Agent:** Produce a **250–400 word** draft with intro, main insight, and closing.

---

## Example Input
```
How is AI disrupting or benefiting IT industry
```
(Provided in the workflow’s pinned `chatInput` to help you test immediately.)

---

## Best Use Cases
- Weekly or monthly **newsletter production** from a single topic  
- **Content ideation** pipelines for blogs and email campaigns  
- Agency or internal **content operations** that need fast topic → draft conversion  
- **Marketing teams** standardizing voice and structure across issues

---

## n8n Node Map (What’s Included)

- **Trigger:** `When chat message received` (chatTrigger) – starts the pipeline when a chat message arrives; includes test `sessionId` and `chatInput`.  
- **Main Agent:** `AI Agent` (Orchestrator).  
- **Agent Tools:**  
  - `Research Topics` (agentTool) → **OpenRouter Chat Model #1** (Llama 3.2 3B instruct:free).  
  - `Create Titles` (agentTool) → **OpenRouter Chat Model #2** (Llama 3.2 3B instruct:free).  
  - `Create Description` (agentTool) → **OpenRouter Chat Model #3** (Llama 3.2 3B instruct:free).  
  - `Create Script` (agentTool) → **OpenRouter Chat Model #4** (Llama 3.2 3B instruct:free).  
- **Language Models:**  
  - Orchestrator uses `meta-llama/llama-3-8b-instruct`.  
  - Tools use `meta-llama/llama-3.2-3b-instruct:free`.  
  - All via a configured `openRouterApi` credential (“SG OpenRouter account”).  
- **Sticky Notes:** Document the roles (Orchestrator + each Agent) within the canvas for quick orientation.

---

## Setup & Configuration

1) **Import the Workflow**  
- In n8n, **Import** the `SG Multi Agent Researcher.json` as a new workflow.

2) **Credentials (OpenRouter)**  
- Add your **OpenRouter API** key under **Credentials** and associate it with each “OpenRouter Chat Model” node (already referenced as **SG OpenRouter account**).  
- You may swap models (e.g., different Llama or other providers) if you have access.

3) **Triggering**  
- Use the included **chatTrigger** (“When chat message received”) or replace it with your preferred trigger (Webhook, Schedule, Manual).  
- For quick tests, keep the default `chatInput` or send a new topic via chat.

4) **Outputs**  
- The **AI Agent (Orchestrator)** returns the final structured result: a set of topic angles, 5 candidate titles, a short description, and the 250–400 word script.  
- You can append downstream nodes (e.g., email send, CMS draft) to automate publishing.

---

## Safety & Hallucination Notes
- Constrains style and structure through **explicit system messages per agent**.  
- Keeps steps **separate** to avoid role leakage and maintain clarity.  
- You can improve factuality by swapping models or adding external retrieval if needed.

---

## Limitations
- The workflow does **not** include external search or retrieval; factual claims rely on the model alone.  
- Best for **general, non‑controversial** topics; add retrieval for technical or time‑sensitive content.  
- Output quality depends on prompt clarity and chosen model.

---

## Version
**v1.0 — Built for n8n AI Agent Tools Demo**; oriented for topic → newsletter generation using OpenRouter Llama models.

---

## Quick Start (Copy/Paste)
1. Import `SG Multi Agent Researcher.json` into n8n.  
2. Configure **OpenRouter** credentials and confirm each LM node points to your key.  
3. Trigger via chat (use the included example or your own topic).  
4. Review the final **Topics → Titles → Description → Script** bundle and publish.

---

### Optional Enhancements
- **Retrieval step:** Add a web‑search or knowledge base node before the “Create Script” agent to ground claims.  
- **A/B titles:** Fan‑out the “Create Titles” output to test multiple headlines in your ESP/CRM.  
- **Localization:** Duplicate agents with language‑specific prompts for multilingual newsletters.  
- **Publishing:** Connect to Gmail, Outlook, Notion, Confluence, or CMS to automate distribution.
