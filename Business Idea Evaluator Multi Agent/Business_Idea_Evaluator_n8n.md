# Business Idea Evaluator — n8n Multi-Agent System

## Overview

The **Business Idea Evaluator** is a multi-agent AI workflow built in n8n. It evaluates one business idea through four specialist perspectives and then combines their findings into a final scored verdict.

### What it does

Feed in one business idea and get:

- Market assessment
- Feasibility assessment
- Money/economics assessment
- Skeptical risk assessment
- Overall scores
- A decisive **GO / REWORK / KILL** recommendation

The architecture follows a simple multi-agent pattern:

```text
                    ┌─────────────────┐
       Idea ──────▶ │  Orchestrator   │
                    │   Coordinates    │
                    └────────┬────────┘
                             │
              ┌──────────────┼──────────────┐
              ▼              ▼              ▼
       Market Analyst   Feasibility     Money Agent
              │          Checker             │
              └──────────────┬──────────────┘
                             │
                         ┌───▼────┐
                         │Skeptic │
                         └───┬────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │  Verdict Agent  │
                    │ Scores + Decision│
                    └────────┬────────┘
                             │
                             ▼
                    GO / REWORK / KILL
```

## Node Architecture

| Node | Role | Evaluates |
|---|---|---|
| **Orchestrator** | Coordinator | Dispatches the idea to specialists |
| **Market Analyst** | Specialist | Demand, competition, timing, market size |
| **Feasibility Checker** | Specialist | Buildability, skills, operations, constraints |
| **Money Agent** | Specialist | Revenue model, unit economics, margins |
| **Skeptic** | Specialist | Failure points and kill-shots |
| **Verdict Agent** | Synthesizer | Scores and final decision |

### Recommended n8n pattern

Use one **AI Agent** as the Orchestrator and expose the four specialist agents as tools/sub-agents. After the Orchestrator has collected the four analyses, send the combined information to a final **Verdict Agent**.

---

# PART 1 — n8n System Prompts

Copy each prompt into the **System Message** of the corresponding n8n AI Agent node.

## 1. Orchestrator

**Node type:** AI Agent  
**Role:** Coordinates the specialist agents.

```text
You are the Orchestrator of a business idea evaluation panel. You receive a raw business idea and coordinate four specialist agents to judge it, then hand everything to the Verdict agent.

Your job:
1. Read the incoming idea. If it is one line, restate it in one clear sentence so all specialists judge the same thing.
2. Call each specialist tool exactly once, passing the restated idea: Market Analyst, Feasibility Checker, Money Agent, Skeptic.
3. Do not analyze the idea yourself. You coordinate, you do not judge.
4. Collect all four outputs. If any specialist returns something empty or off-topic, call it once more.
5. Pass the idea plus all four analyses to the Verdict agent and return its final output.

Never skip a specialist. Never invent an analysis a specialist did not return.
```

### Orchestrator responsibilities

The Orchestrator should:

1. Receive the raw business idea.
2. Normalize it into one clear sentence.
3. Call every specialist.
4. Collect their responses.
5. Send all findings to the Verdict Agent.
6. Return the final evaluation.

It should **not** make its own judgment.

---

## 2. Market Analyst

**Node type:** AI Agent / Tool sub-agent  
**Role:** Evaluates the market only.

```text
You are a Market Analyst on a business idea evaluation panel. You judge ONE dimension only: market.

Given a business idea, assess:
- Real demand: is there a paying, underserved need?
- Competition: who already serves this, and how saturated is it?
- Timing: why now, or why not?
- Rough market size: small niche, or scalable.

Return 4 to 6 tight sentences. End with one line: "Market signal: strong / mixed / weak." Do not comment on money, feasibility, or risk. Stay in your lane.
```

### Output expectation

The agent should focus only on:

- Customer demand
- Existing alternatives
- Competitive intensity
- Market timing
- Market potential

Do not let it evaluate profitability or technical complexity.

---

## 3. Feasibility Checker

**Node type:** AI Agent / Tool sub-agent  
**Role:** Evaluates whether the idea can actually be built and operated.

```text
You are a Feasibility Checker on a business idea evaluation panel. You judge ONE dimension only: can a first-time founder actually build and run this?

Assess:
- Operational lift: what has to happen daily for this to work.
- Skills, team, or licenses required.
- Physical or supply constraints.
- Time to a working version.

Return 4 to 6 tight sentences. End with one line: "Buildable by a first-time founder: yes / with help / no." Do not comment on market, money, or risk.
```

### Output expectation

Focus on:

- Required skills
- Team requirements
- Operations
- Licenses or compliance
- Supply/physical constraints
- MVP/build time

---

## 4. Money Agent

**Node type:** AI Agent / Tool sub-agent  
**Role:** Evaluates business economics.

```text
You are the Money Agent on a business idea evaluation panel. You judge ONE dimension only: economics.

Assess:
- How this makes money (the actual model).
- Unit economics: rough cost to serve one customer vs what they pay.
- Realistic path to first revenue.
- Whether margins survive at scale.

Return 4 to 6 tight sentences with rough numbers where you can. End with one line: "Money model: healthy / thin / broken." Do not comment on market, feasibility, or risk.
```

### Output expectation

Focus on:

- Revenue mechanism
- Pricing
- Cost to serve
- Gross margin
- Customer acquisition economics where relevant
- Time/path to first revenue
- Scalability

Use rough numbers when reasonable, but clearly distinguish assumptions from known facts.

---

## 5. Skeptic

**Node type:** AI Agent / Tool sub-agent  
**Role:** Finds the strongest reasons the idea could fail.

```text
You are the Skeptic on a business idea evaluation panel. Your only job is to find the kill-shots.

Name the 2 or 3 reasons this idea most likely fails: the hidden cost, the wrong assumption, the reason 9 of 10 versions of this die. Be specific and blunt, not generic. No praise, no balance.

Return 3 to 5 tight sentences. End with one line: "Biggest kill-shot: <one phrase>."
```

### Output expectation

The Skeptic should look for:

- Hidden assumptions
- Major execution risks
- Customer behavior problems
- Regulatory or operational blockers
- Weak differentiation
- Unsustainable economics
- Reasons the idea may fail despite appearing attractive

Do not ask the Skeptic to balance criticism with positive points.

---

# 6. Verdict Agent

**Node type:** AI Agent  
**Role:** Final synthesizer and decision maker.

```text
You are the Verdict agent. You receive a business idea plus four specialist analyses (Market, Feasibility, Money, Skeptic). You synthesize, you do not re-analyze.

Output exactly:
- Idea: <one line>
- Scores (1 to 10): Market _, Feasibility _, Money _, Risk-adjusted _
- Verdict: GO / REWORK / KILL
- One sentence on why.
- If REWORK: the single change that would most improve it.

Base scores only on what the specialists said. Be decisive.
```

### Verdict format

The final output should look like:

```text
Idea: AI-powered appointment assistant for small clinics

Scores (1 to 10):
Market 8
Feasibility 7
Money 8
Risk-adjusted 6

Verdict: REWORK

Strong demand and attractive economics, but operational and trust risks need to be reduced before launch.

If REWORK: Start with one clinic niche and validate the workflow manually before building the full product.
```

---

# PART 2 — Recommended n8n Node Flow

A practical n8n implementation can use the following sequence:

```text
Chat Trigger / Form Trigger
        │
        ▼
Orchestrator AI Agent
        │
        ├──── Tool → Market Analyst
        │
        ├──── Tool → Feasibility Checker
        │
        ├──── Tool → Money Agent
        │
        └──── Tool → Skeptic
        │
        ▼
Verdict Agent
        │
        ▼
Final Response
```

## Suggested Nodes

### Node 1 — Chat Trigger

Use this as the entry point if users will type their business idea conversationally.

**Example input:**

```text
I want to start an AI-powered WhatsApp assistant for real estate agents that automatically follows up with leads.
```

Alternative triggers:

- Webhook
- Form Trigger
- Telegram Trigger
- WhatsApp integration
- Manual Trigger for testing

---

### Node 2 — Orchestrator AI Agent

Connect the incoming idea to the Orchestrator.

The Orchestrator needs access to:

- Market Analyst
- Feasibility Checker
- Money Agent
- Skeptic

Each specialist can be implemented as an AI Agent and connected to the Orchestrator through the appropriate n8n AI Agent Tool connection.

---

### Node 3 — Specialist Agents

Create four specialist AI Agent nodes.

#### Market Analyst

Input:

```text
{{ business idea }}
```

System prompt:

Use the **Market Analyst** prompt above.

#### Feasibility Checker

Input:

```text
{{ business idea }}
```

System prompt:

Use the **Feasibility Checker** prompt above.

#### Money Agent

Input:

```text
{{ business idea }}
```

System prompt:

Use the **Money Agent** prompt above.

#### Skeptic

Input:

```text
{{ business idea }}
```

System prompt:

Use the **Skeptic** prompt above.

---

# PART 3 — Passing Results to the Verdict Agent

The Verdict Agent needs:

1. Original/restated business idea
2. Market analysis
3. Feasibility analysis
4. Money analysis
5. Skeptic analysis

A useful prompt structure is:

```text
Business Idea:
{{ business_idea }}

MARKET ANALYSIS:
{{ market_analysis }}

FEASIBILITY ANALYSIS:
{{ feasibility_analysis }}

MONEY ANALYSIS:
{{ money_analysis }}

SKEPTIC ANALYSIS:
{{ skeptic_analysis }}

Now produce the final verdict using the required output format.
```

If the Orchestrator already returns a combined structured response, use that output as the input to the Verdict Agent.

---

# PART 4 — Testing the Workflow

Use simple business ideas first.

## Test Idea 1

```text
AI-powered WhatsApp follow-up assistant for real estate agents.
```

Check whether:

- All four specialists are called.
- Each specialist stays within its assigned dimension.
- The Verdict Agent receives all four analyses.
- Scores are between 1 and 10.
- The final decision is exactly GO, REWORK, or KILL.

## Test Idea 2

```text
Subscription service delivering healthy office lunches to employees.
```

## Test Idea 3

```text
AI tool that converts long YouTube videos into short-form social media content.
```

---

# PART 5 — Important n8n Design Principles

## 1. Give each agent one job

Do not create one giant prompt that asks the AI to evaluate everything.

The strength of the architecture comes from specialization.

```text
Market → Market only
Feasibility → Feasibility only
Money → Economics only
Skeptic → Failure points only
Verdict → Synthesis only
```

## 2. Keep the Orchestrator neutral

The Orchestrator should coordinate rather than form an opinion.

This reduces the chance that its initial opinion influences the specialists.

## 3. Keep specialist outputs short

Short outputs make the final synthesis easier and reduce unnecessary token usage.

Recommended:

- Market: 4–6 sentences
- Feasibility: 4–6 sentences
- Money: 4–6 sentences
- Skeptic: 3–5 sentences

## 4. Make the Verdict decisive

The goal is not to produce a long consulting report.

The useful output is:

```text
What is the score?
What is the decision?
Why?
If it is REWORK, what should change?
```

---

# Part 6 — Optional Improvements

Once the basic workflow works, you can improve it with additional nodes.

### Web Research

Add web search tools to the Market Analyst to verify:

- Competitors
- Pricing
- Market trends
- Customer demand
- Recent developments

This is especially useful because the base prompt otherwise relies on the model's existing knowledge.

### Structured Output

Use structured output/JSON for the specialist agents.

Example:

```json
{
  "analysis": "Demand appears strong...",
  "signal": "strong"
}
```

For the Verdict Agent:

```json
{
  "idea": "AI-powered WhatsApp follow-up assistant for real estate agents",
  "market_score": 8,
  "feasibility_score": 7,
  "money_score": 8,
  "risk_adjusted_score": 6,
  "verdict": "REWORK",
  "reason": "The market and economics are attractive, but differentiation and execution risk need validation.",
  "recommended_change": "Start with one real-estate niche and validate the workflow with 5 paying customers."
}
```

Structured output makes it easier to send the result to:

- Google Sheets
- Airtable
- Notion
- CRM
- Email
- Telegram
- WhatsApp
- A dashboard

### Persistence

Store evaluations in a database or Google Sheet so users can compare multiple ideas over time.

Recommended fields:

```text
Date
Business Idea
Market Score
Feasibility Score
Money Score
Risk-adjusted Score
Verdict
Reason
Recommended Change
```

---

# Quick Build Checklist

- [ ] Add Chat/Form/Webhook Trigger
- [ ] Create Orchestrator AI Agent
- [ ] Create Market Analyst
- [ ] Create Feasibility Checker
- [ ] Create Money Agent
- [ ] Create Skeptic
- [ ] Connect four specialists as Orchestrator tools
- [ ] Create Verdict Agent
- [ ] Pass all specialist findings to Verdict Agent
- [ ] Test with 3–5 different business ideas
- [ ] Validate that every specialist stays in its lane
- [ ] Validate GO / REWORK / KILL output
- [ ] Optionally add web research
- [ ] Optionally store evaluations in a database or sheet

---

## Core Learning

This workflow demonstrates the fundamental **multi-agent orchestration pattern**:

```text
One problem
     ↓
Multiple specialized agents
     ↓
Independent perspectives
     ↓
Central synthesizer
     ↓
Actionable decision
```

The important lesson is not the specific business evaluator. The same architecture can be reused for:

- Product research
- Content strategy
- Hiring decisions
- Lead qualification
- Investment research
- Marketing campaign evaluation
- Customer research
- Competitive analysis
- Business planning
