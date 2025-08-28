## 📊 Amazon Best Seller Page Scraper (n8n Workflow)

This project is an automated product-hunting pipeline built in n8n
. It scrapes the Amazon Best Sellers page for any category, stores the results in Google Sheets, and applies filters to highlight potential opportunities (Insights).

## 🚀 Features

Form Input → Paste any Amazon Best Sellers URL via an n8n Form Trigger.

Scraping → Uses Apify’s Amazon Best Seller Actor to fetch the top 50 products.

Auto Timestamp → Each product row is tagged with crawl_date and crawl_time.

Google Sheets Output

Scrapped Data (Raw) → all 50 products from the selected category.

Insights (Filtered) → products that meet hunting criteria.

Filter Criteria (Insights)

Price between $5 and $50

Stars greater than 4.5

Review count less than 3000

Scalable Design → easily extend filters, scoring, or add Slack/Telegram alerts.

## 🛠 Workflow Overview

Form Trigger

Input field: Amazon Best Seller URL

Example: https://www.amazon.com/Best-Sellers-Electronics/zgbs/electronics/

HTTP Request (POST)

Starts an Apify run with the provided category URL.

HTTP Request (GET)

Fetches dataset results from the completed Apify run (top 50 products).

Code Node – Add Crawl Date & Time

Appends crawl_date (YYYY-MM-DD) and crawl_time (HH:MM:SS).

IF Node – Apply Filters

Passes only items meeting: price 5–50, stars > 4.5, reviews < 3000.

Google Sheets – Scrapped Data

Appends all 50 items into Scrapped data sheet (raw log).

Google Sheets – Insights

Appends only filtered products into Insights sheet.

## 📂 Google Sheets Structure

Sheet 1: Scrapped Data (Raw)

crawl_date | crawl_time | asin | name | url | category | price | stars | reviews

Sheet 2: Insights (Filtered)

crawl_date | crawl_time | asin | name | url | category | price | stars | reviews
(only rows that pass the IF filter)

## 🔧 How to Run

Clone this repo or import workflow JSON into your n8n instance.

Set up credentials for:

Google Sheets (service account or OAuth).

Apify API token.

Open the Form Trigger → paste an Amazon Best Sellers URL → Submit.

Workflow executes:

Raw data → Scrapped Data sheet.

✅ This setup gives you a hands-free product research tool: every time you run it, you get a fresh shortlist of promising Amazon Best Seller products right in Google Sheets.

Filtered data → Insights sheet.
