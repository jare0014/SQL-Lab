# SQL Lab: Systems Analysis & Data Foundations
This is a working log of my transition into data engineering and SQL-based analysis. My background is in physics, so I tend to treat a database as a system to be measured and validated rather than just a collection of rows.

The goals here are:

Master the BigQuery/Python stack.

Build data pipelines that don't break when the schema changes.

Optimize for cost and memory (Data Projection).

## Exercise 1: Chicago Crime Data: Logic & Implementation
The first lab involved exploring Chicago's crime records. While the exercises were straightforward, I used them as a sandbox to test "defensive" coding patterns.

The "Over-Engineered" Field Count
Instead of just printing the schema and counting the columns by hand (the "human-in-the-loop" failure point), I wrote a quick script to audit the table structure.

Logic: I used a generator expression to scan for keywords like timestamp and specific types like TIMESTAMP.

The Reason: If I’m working with 200 columns instead of 20, I’m not going to count them manually. This is schema-agnostic; it doesn't matter how the table grows—the check remains accurate.

Smarter Data Extraction
When pulling coordinates for mapping, I avoided the "Junior" move of downloading the whole table into a local DataFrame.
Logic: I utilized the selected_fields argument to perform Data Projection at the API level.
The Reason: In a real-world cloud environment, you pay for every byte you move. Fetching only latitude and longitude is faster, cheaper, and easier on the machine's RAM.

Handling "Dirty" Metadata
I implemented case-insensitive checks (.lower() and .upper()) throughout the lab. Experience has shown that metadata is rarely consistent—Time_Stamp is just as likely as timestamp. My code assumes the data is messy and builds the filter accordingly.

Tech Used
SQL (BigQuery): Focus on relational algebra and set theory.
Python (Google Cloud API): Using the client library to orchestrate data flow.
Pandas: Strictly for final formatting and visualization.

Current Progress
[x] Programmatic Schema Inspection
[x] Efficient Data Retrieval
[ ] Complex Aggregations & Joins (Next)
