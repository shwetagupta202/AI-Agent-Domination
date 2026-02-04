# 📍 AI Agent -- Google Maps Business Scraper (n8n + Apify)

An automated **AI-powered Google Maps scraping agent** that extracts
local business data based on a **search query and location**, and stores
it directly into **Google Sheets** for lead generation, market research,
and business intelligence.

------------------------------------------------------------------------

## 🚀 What This Agent Does

-   Accepts a **Search Term** (e.g. SaaS, Restaurants, Clinics)
-   Accepts a **Location** (City or Area)
-   Scrapes Google Maps business listings using **Apify**
-   Extracts structured business data
-   Automatically appends results into **Google Sheets**

------------------------------------------------------------------------

## 🧩 Tech Stack

-   **n8n** -- Workflow automation\
-   **Apify Actor** -- Google Maps Scraper (crawler-google-places)\
-   **Google Sheets API** -- Data storage

------------------------------------------------------------------------

## 📊 Extracted Data Fields

-   Business Name\
-   Address\
-   City\
-   Website\
-   Phone Number\
-   Category\
-   Rating\
-   Reviews Count\
-   Opening Hours (if available)

------------------------------------------------------------------------

## 🔁 Workflow Overview

1.  **Manual Trigger**
    -   Start the workflow from n8n
2.  **Search Field (Set Node)**
    -   Example:
        -   Search Term: `SaaS`
        -   Location: `Bengaluru`
3.  **Google Maps Scraper (Apify Actor)**
    -   Fetches top local businesses from Google Maps
    -   Configurable result limits
4.  **Google Sheets -- Append Row**
    -   Stores clean business data automatically

------------------------------------------------------------------------

## 📂 Google Sheet Structure

  Column     Description
  ---------- -------------------
  Title      Business name
  Address    Full address
  City       City name
  Website    Business website
  Phone      Contact number
  Category   Business category
  Rating     Google rating
  Reviews    Number of reviews

------------------------------------------------------------------------

## 🌍 Real-World Use Cases

### 1️⃣ Local Lead Generation

Sales teams extract businesses by niche and city to build: - Cold
outreach lists - WhatsApp & email campaigns - CRM lead pipelines

------------------------------------------------------------------------

### 2️⃣ Agency Prospecting

Marketing agencies scrape: - Clinics, gyms, salons, SaaS, restaurants -
Identify businesses without websites or low ratings - Pitch SEO, ads, or
automation services

------------------------------------------------------------------------

### 3️⃣ Market Research & Expansion

Startups analyze: - Business density by location - Competitor presence -
Category-wise saturation

------------------------------------------------------------------------

### 4️⃣ Local SEO & Reputation Analysis

SEO teams track: - Ratings & reviews - Competitor visibility - Ranking
by area

------------------------------------------------------------------------

### 5️⃣ AI Enrichment Pipelines

Scraped data can be sent to AI agents to: - Enrich missing emails -
Classify leads - Generate personalized outreach messages

------------------------------------------------------------------------

### 6️⃣ Automation & AI Training

Used as a **real-world demo workflow** for: - n8n automation - AI agent
building - Ethical web scraping

------------------------------------------------------------------------

## 🔒 Compliance & Best Practices

-   Uses **Apify-managed Google Maps actor**
-   No login or private data scraping
-   Designed for research, sales intelligence & outreach

------------------------------------------------------------------------

## 🚀 Future Enhancements

-   Email enrichment via third-party APIs
-   CRM sync (HubSpot, Zoho, Salesforce)
-   Scheduled city-wise scraping
-   AI-based lead scoring
-   WhatsApp automation integration

------------------------------------------------------------------------

## 📌 Ideal For

-   Growth Marketers\
-   Sales & Lead Gen Teams\
-   Agencies & Consultants\
-   AI Automation Builders\
-   Local SEO Professionals

------------------------------------------------------------------------

## 🧠 Pro Tip

Combine this agent with: - **AI copywriting agents** - **WhatsApp /
Email automation** - **CRM pipelines**

This turns Google Maps data into a **fully automated revenue engine**.
