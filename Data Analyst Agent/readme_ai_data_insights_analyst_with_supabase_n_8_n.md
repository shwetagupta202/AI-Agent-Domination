# AI Data Insights Analyst with Supabase (n8n)

This repository contains an **n8n workflow** that lets users chat with a **Supabase (PostgreSQL) database** using an **AI-powered Data Insights Analyst**.

Instead of writing SQL manually, users can ask questions in natural language. The AI agent understands the database schema, generates safe SQL queries, executes them, and returns insights.

---

## 🚀 What This Workflow Does

This workflow enables:

- Conversational querying of a Supabase/PostgreSQL database
- Automatic discovery of database schema and table definitions
- Safe, read-only SQL generation using AI
- Aggregations, summaries, and JSON field extraction
- Multi-step reasoning using tools (schema → table definition → query)

The AI agent behaves like a **Data Analyst**, not just a chatbot.

---

## 🧠 Architecture Overview

**Trigger**
- Chat Webhook (public)

**AI Brain**
- OpenRouter (Gemini 2.5 Flash Lite)
- Optional Google Gemini Chat Model

**Tools Used by AI Agent**
1. **DB Schema Tool** – lists all tables in the public schema  
2. **Get Table Definition Tool** – fetches column names, types, constraints   
3. **Run SQL Query Tool** – executes AI-generated SQL safely  

**Memory**
- Buffer-based conversational memory

**Database**
- Supabase PostgreSQL

---

## 🛠️ Prerequisites

Create accounts on:

- **n8n** – workflow automation
- **Supabase** – PostgreSQL database
- **OpenRouter** – AI model access (Gemini)
- *(Optional)* Google Gemini API

---

## ⚙️ Setup Instructions

### 1. Import Workflow into n8n

- Download the workflow JSON file
- In n8n, click **Import Workflow**
- Upload the JSON file

---

### 2. Configure Supabase Credentials

In n8n:

- Create a **PostgreSQL credential** using Supabase details
- Update all Postgres Tool nodes:
  - **DB Schema**
     Query- SELECT table_schema, table_name
FROM information_schema.tables
WHERE table_type = 'BASE TABLE' AND table_schema = 'public';
  - **Get Table Definition**
    Query- "SELECT 
    c.column_name,
    c.data_type,
    c.is_nullable,
    c.column_default,
    tc.constraint_type,
    ccu.table_name AS referenced_table,
    ccu.column_name AS referenced_column
FROM 
    information_schema.columns c
LEFT JOIN 
    information_schema.key_column_usage kcu 
    ON c.table_name = kcu.table_name 
    AND c.column_name = kcu.column_name
LEFT JOIN 
    information_schema.table_constraints tc 
    ON kcu.constraint_name = tc.constraint_name
    AND tc.constraint_type = 'FOREIGN KEY'
LEFT JOIN
    information_schema.constraint_column_usage ccu
    ON tc.constraint_name = ccu.constraint_name
WHERE 
    c.table_name = '{{ $fromAI("table_name") }}'" -- Your table name
    AND c.table_schema = 'public' -- Ensure it's in the right schema
ORDER BY 
    c.ordinal_position;
"
  - **Run SQL Query**
    Query- {{ $fromAI("query","SQL query for PostgreSQL DB in Supabase") }}

Required values:
- Host
- Database name
- Username
- Password
- Port (usually `5432`)

---

### 3. Configure AI Model (Brain)

You can use **either or both**:

- **OpenRouter Chat Model** (Recommended)
- **Google Gemini Chat Model**

Update API credentials in n8n accordingly.
**System Message:** "You are DB assistant. You need to run queries in DB aligned with user requests. Whenever you use column names in the query enclose with double quotes. Example instead of SUM(Units) write SUM("Units")

Run custom SQL query to aggregate data and response to user.

Fetch all data to analyse it for response if needed.

Always fetch the schema and table defination before you create the query. 

Use these in sequence to get the relevant results
1. DB Schema  - for getting all tables from database
2. Get table definition - for getting schema of relevant table by using DB Schema
3. Run SQL Query - for querying the actual user problem by using  "DB Schema" and "Get table definition"

Consider table tbl_transactions for all orders and transactions of customers


Never delete any table or schema"

---

### 4. Activate the Workflow

- Enable the workflow
- Copy the **Chat Webhook URL**
- Use it in your frontend or testing tool

---

## 🤖 AI Agent Behavior

The AI agent is instructed to:

- Always fetch schema before querying
- Always fetch table definitions before writing SQL
- Enclose column names in double quotes
- Use `->>` for JSON field extraction
- Never delete tables or schemas
- Assume `tbl_transactions` contains customer order data

This makes the agent **safe, structured, and analyst-like**.

---

## 💬 Example Questions You Can Ask

- "Show total sales by month"
- "Which customers placed the most orders?"
- "Extract city from JSON address field"
- "What is the average order value?"
- "List all tables in the database"

---

## 🔐 Security Notes

- The workflow is **read-only** by design
- No DELETE, DROP, or ALTER operations are allowed
- All queries are generated based on schema inspection

---

## 🧩 Extending This Workflow

You can easily extend it to:

- Add role-based access (via Supabase Auth)
- Connect a frontend (Lovable, React, Next.js)
- Add charts and dashboards
- Log queries and responses
- Add department-level data access

---

## 📌 Use Cases

- AI-powered BI assistant
- Internal analytics chatbot
- Data analyst copilot
- Self-serve reporting for non-technical users
- SaaS analytics feature

---

## 📄 License

Free to use and modify for educational and internal projects.

---

## 🙌 Author

**Shweta Gupta**  
AI & Career Coach | Data + Automation Educator

If you’re building AI-powered analytics or teaching agentic workflows, this is a solid production-grade foundation.

Happy building 🚀

