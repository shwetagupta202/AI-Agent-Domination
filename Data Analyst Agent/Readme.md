Chat GPT prompt for creating Lovable prompt "Act as a prompt engineer. I want to create a prompt for building an app in lovable for my data analysis agent. Give me the prompt to create an ecommerce website for selling books which will have the login feature for each user to login. While logging in user should be asked about his role. If the role is Data Analyst, that user should get an additional option to analyse data using a chat window. The signup functionality has to be built using supabase authentication. Give me the prompt"



Lovable prompt
"You are a senior full-stack AI engineer building a production-ready web application using Lovable.

🎯 App Goal

Build an E-commerce Website for Selling Books with role-based login and a Data Analysis Agent for specific users.

🧩 Core Features
1️⃣ Authentication (Mandatory)

Use Supabase Authentication for:

Sign Up

Login

Logout

During Sign Up, ask the user to select a Role:

Customer

Data Analyst

Store the selected role in Supabase (user metadata or profile table).

2️⃣ User Roles & Permissions

Customer

Can:

Browse books

View book details

Add books to cart

Place orders

Data Analyst

Has all Customer permissions

PLUS:

Access to a “Data Analysis” option in the navigation/menu

A dedicated Chat Window to interact with a Data Analysis AI Agent

3️⃣ E-commerce Functionality

Book listing page with:

Title

Author

Price

Category

Book detail page

Shopping cart

Order summary page

(Payment integration can be mocked or optional.)

4️⃣ Data Analysis Agent (Only for Data Analyst Role)

Show a Chat Interface only if user role = Data Analyst

Chat window should:

Accept natural language queries

Be positioned as a Data Analysis Assistant

Be capable of:

Analyzing sales data

Summarizing orders

Answering questions like:

“Which books sold the most last month?”

“Total revenue by category”

“Customer purchase trends”

Assume the agent will query data from Supabase tables such as:

books

orders

order_items

users

5️⃣ UI / UX Expectations

Clean, modern UI

Role-based navigation:

Hide Data Analysis features from non-Data Analyst users

Responsive design

Clear separation between:

Store UI

Data Analysis Chat UI

6️⃣ Technical Constraints

Use Supabase for:

Authentication

User role storage

Database

Enforce role-based access control at UI level

Code should be clean, modular, and production-ready

🚀 Final Output

Fully working ecommerce app

Supabase-based authentication with role selection

Role-specific features

Data Analysis Chat Agent visible only to Data Analysts"
