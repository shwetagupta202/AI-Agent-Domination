# Role-Based E‑commerce Platform with AI Data Analysis Agent

## 📌 Overview

This project demonstrates a **real-world, end-to-end use case** where a traditional **E‑commerce application** is enhanced with an **AI-powered Data Analysis Agent**, accessible only to specific users based on their role.

The core idea of this use case is to show how:

- **Supabase Authentication** can be used for secure login and role management
- **Role-based access control (RBAC)** can unlock advanced features
- **AI Agents (via n8n)** can be embedded into real products
- **Non-technical users** can analyze business data using natural language

This is not just a demo — it is a **production-style architecture** that can be extended into SaaS products, internal dashboards, or AI-powered business tools.

---

## 🎯 Use Case Summary

An **online bookstore** where:

- Regular users shop for books
- Data Analysts get an **additional AI-powered chat interface**
- The AI agent can analyze sales, orders, and customer behavior
- All authentication and data storage are handled by Supabase

The same application serves **two different user experiences** based on role.

---

## 👥 User Roles

### 1️⃣ Customer

Customers can:

- Sign up and log in securely
- Browse available books
- View book details
- Add books to cart
- Place orders

They **do not** see any analytics or AI features.

---

### 2️⃣ Data Analyst

Data Analysts can do **everything a Customer can**, plus:

- Access a **Data Analysis** section in the app
- Use an **AI-powered Chat Window**
- Ask questions in natural language about business data

Example questions:

- “Which books sold the most last month?”
- “Total revenue by category”
- “Customer purchase trends”

The AI agent translates these questions into database queries and returns insights.

---

## 🤖 Data Analysis Agent (Key Highlight)

The Data Analysis Agent is:

- Powered by **n8n AI Agent workflow**
- Connected to **Supabase PostgreSQL**
- Embedded into the app using an **n8n Chat Webhook URL**

### Agent Capabilities

- Understand natural language queries
- Inspect database schema automatically
- Generate safe, read-only SQL queries
- Analyze structured and JSON data
- Return summaries, aggregations, and insights

The agent works like a **virtual Data Analyst**, not just a chatbot.

---

## 🧩 System Architecture

**Frontend (Lovable)**
- Role-based UI
- Authentication screens
- Store UI + Data Analysis Chat UI

**Backend**
- Supabase Auth (Sign up / Login / Logout)
- Supabase PostgreSQL Database

**AI Layer**
- n8n AI Agent workflow
- Schema Tool → Table Definition Tool → SQL Query Tool

---

## 🔐 Authentication & Roles

- Users sign up using **Supabase Authentication**
- During signup, users select a role:
  - Customer
  - Data Analyst
- Role is stored in Supabase (user metadata or profile table)
- UI dynamically adapts based on role

---

## 🛍️ E‑commerce Features

- Book listing page
- Book details page
- Shopping cart
- Order summary
- (Optional / Mocked) payment flow

Supabase tables typically include:

- `books`
- `orders`
- `order_items`
- `users`

---

## 💡 Why This Use Case Matters

This project showcases:

- How AI agents fit into **real business applications**
- Practical use of **Agentic AI**, not just chatbots
- Clear separation of concerns (UI, Auth, Data, AI)
- A strong example for:
  - AI product builders
  - Data engineers
  - SaaS founders
  - Automation professionals

---

## 🚀 Ideal Extensions

This use case can be extended to:

- Paid analytics dashboards
- Internal BI tools
- Multi-tenant SaaS products
- Department-based data access
- Advanced visual analytics

---

## 👩‍💻 Author

**Shweta Gupta**  
AI, Automation & Career Coach

This use case is designed to help professionals understand how **AI Agents + Databases + Real Products** come together in practice.

---

---

## 🧠 ChatGPT Prompt to Generate Lovable App

You can use the following **ready-to-use ChatGPT prompt** to generate this entire application inside **Lovable**.

```
Act as a prompt engineer.

I want to create a prompt for building an app in Lovable for my data analysis agent.

Give me the prompt to create an ecommerce website for selling books which will have the login feature for each user to login.

While logging in, the user should be asked about his role.

If the role is **Data Analyst**, that user should get an additional option to analyse data using a chat window.

The signup functionality has to be built using **Supabase authentication**.

For the Data Analyst chat agent, add the embedded URL as:
"<n8n production embedded url>"

Now give me the complete Lovable prompt.
```

📌 **Tip:** Replace `<n8n production embedded url>` with your actual n8n chat webhook embed URL before using this prompt.

---

Happy building 🚀

