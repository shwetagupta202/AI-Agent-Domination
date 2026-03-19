# FAQ RAG Workflows (n8n) -- Beginner Friendly Guide

This project helps you build an AI chatbot that answers questions using
Google Sheets.

Even if you're **non-technical**, you can set this up by following the
steps below.

------------------------------------------------------------------------

## 🎯 What Can You Use This For?

### 🔹 1. Customer Support Bot

-   Answer FAQs like return policy, delivery time, refunds
-   Reduce manual support effort

### 🔹 2. Instagram / WhatsApp Auto Replies

-   Connect with automation tools
-   Instantly reply to common queries

### 🔹 3. Course / Community Assistant

-   Answer student questions
-   Share links, policies, contact info

### 🔹 4. E-commerce Product Assistant

-   Answer product-related questions
-   Help users decide faster → increases sales

### 🔹 5. Internal Team Knowledge Bot

-   HR policies
-   SOPs
-   Company guidelines

------------------------------------------------------------------------

## 📁 Files Included

### 1. Single Sheet (Beginner Friendly)

-   Uses ONE Google Sheet
-   Simple question → answer matching

👉 Best if you're starting out

------------------------------------------------------------------------

### 2. Multi Sheet (Advanced)

-   Uses MULTIPLE sheets
-   Understands type of question:
    -   Policy
    -   Product
    -   Contact

👉 Best for serious business use

------------------------------------------------------------------------

## 🧠 Simple Understanding

Think of it like this:

👉 Google Sheet = Brain\
👉 AI Agent = Smart Assistant\
👉 n8n = Automation Engine

User asks → AI checks sheet → gives best answer

------------------------------------------------------------------------

## 🚀 Step-by-Step Setup (Non-Tech Friendly)

### Step 1: Install n8n

-   Use n8n cloud OR install locally
-   Login to dashboard

------------------------------------------------------------------------

### Step 2: Import the File

-   Click **Import**
-   Upload JSON file (Single or Multi Sheet)

------------------------------------------------------------------------

### Step 3: Connect Google Sheets

-   Click on Google Sheets node
-   Login with your Google account
-   Select your sheet

------------------------------------------------------------------------

### Step 4: Prepare Your Google Sheet

For Single Sheet: - Column 1: question_canonical - Column 2:
answer_rich_text

Example: \| question_canonical \| answer_rich_text \|
\|------------------\|------------------\| \| return policy \| You can
return within 7 days \|

------------------------------------------------------------------------

For Multi Sheet: Create 3 tabs: 1. Policies 2. Products 3. Contact

(Keep columns same as given in file)

------------------------------------------------------------------------

### Step 5: Add Your Data

-   Fill FAQs clearly
-   Keep answers short and structured

------------------------------------------------------------------------

### Step 6: Connect AI Model

-   Add Gemini API key
-   Select model in n8n

------------------------------------------------------------------------

### Step 7: Activate Workflow

-   Turn ON the workflow
-   Copy webhook/chat link

------------------------------------------------------------------------

### Step 8: Test It

Ask questions like: - "What is return policy?" - "Do you have cotton
shirts?" - "How can I contact support?"

------------------------------------------------------------------------

## 🔥 Pro Tips (Important)

-   Write FAQs in simple language
-   Avoid duplicate questions
-   Keep answers clear (1--3 lines)
-   Update sheet regularly

------------------------------------------------------------------------

## ⚡ When to Upgrade to Multi Sheet?

Move to advanced version when: - You have 50+ FAQs - You sell multiple
products - You want better accuracy

------------------------------------------------------------------------

## 💡 Final Advice

Don't overcomplicate this.

Start with **Single Sheet → Test → Get Results → Then Upgrade**

Most people fail because they try to build complex systems first.

You don't need that.

You need something that WORKS.

------------------------------------------------------------------------

## 👩‍💻 Created For

Anyone who wants to: - Build AI agents - Automate support - Create
income streams using AI
