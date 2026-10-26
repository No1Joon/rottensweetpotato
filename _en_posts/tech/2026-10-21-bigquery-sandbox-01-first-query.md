---
title: "BigQuery Without a Card (1) — First Query and Bytes Processed in the BigQuery Sandbox"
description: "The limits of the BigQuery sandbox, which needs only a Google account and no payment card, and how to run a first query on a public dataset while checking bytes processed"
date: 2026-10-21
category: Tech
subcategory: Explainer
tags: [bigquery, bigquery-sandbox, google-cloud, sql, query-cost]
image: /assets/og/en-2026-10-21-bigquery-sandbox-01-first-query.png
---

You can run SQL in BigQuery without registering a payment card

I ran a first query in the **BigQuery sandbox**, which needs only a Google account

![BigQuery console after running a first query in a sandbox project](/assets/images/tech/bigquery-sandbox-01-first-query/01-hero.webp)
*BigQuery console after running a first query in a sandbox project — Source: Google Cloud*

🔗 Link - https://console.cloud.google.com/bigquery

## Sandbox limits

![bq screen showing a new dataset's default expiration of 60 days](/assets/images/tech/bigquery-sandbox-01-first-query/en/02-term.webp)
*bq screen showing a new dataset's default expiration of 60 days — Source: self-rendered from bq CLI output*

The sandbox is enabled automatically in projects with no billing account attached

A sandbox label and an upgrade button appear at the top of the console

The practice project is named bq-sandbox-blog

| Item | Limit |
| :--- | :--- |
| Storage | <mark>10 GiB, lifetime</mark> |
| Query processing | 1 TiB per month |
| Tables, views, partitions | Expire automatically after 60 days |

The storage limit carries the word **lifetime**

The documentation says *This quota is not refunded upon data deletion*

<mark>Deleting data does not restore the 10 GiB limit</mark>

The default expiration on a newly created dataset was **5,184,000,000 milliseconds**

Converted to days, that is exactly <u>60 days</u>

Streaming inserts, DML, and the Data Transfer Service are also unavailable in the sandbox

## First query and estimating bytes processed

![Job information tab showing bytes processed and bytes billed after running a query](/assets/images/tech/bigquery-sandbox-01-first-query/03-photo.webp)
*Job information tab showing bytes processed and bytes billed after running a query — Source: Google Cloud*

I ran the first query on the **usa_names** dataset that Google has made public

It is a table counting the names of US Social Security card applicants since 1910 by birth year

Querying the 10 most common names since 2000 put **Jacob (454,809 people)** in first place

When you type a query into the editor, the estimated bytes processed at the bottom updates before you run it

**This query will process 143.71 MB when run**

After running, the actual bytes processed show up in the job information tab

### 📊 Values in the job information tab

| Item | Value |
| :--- | :--- |
| Bytes processed | **143.71 MB** |
| Bytes billed | <mark>144 MB</mark> |
| Slot milliseconds | 186 |
| Duration | 345 ms |

Running the same query from the CLI shows **150,693,282 bytes** processed

The console converts 1 MB as <u>1,048,576 bytes</u>, giving 143.71 MB

Written in units of a million bytes, the same amount is 150.7 MB

Bytes billed are larger than bytes processed because they are rounded up to the MB

The pricing docs say a **minimum of 10 MB** is billed per table per query

### 💰 Expected cost with a billing account attached

| Item | Amount |
| :--- | :--- |
| Processing 1 TiB | about $6.25 (₩8,310) |
| This query once (144 MB) | <mark>about ₩1.1</mark> |
| Runs possible within the free 1 TiB | about 7,280 |

The sandbox has no billing account, so these amounts are not charged

## What determines bytes processed

![bq screen where the dry_run results for SELECT * and the same query with LIMIT 10 are identical](/assets/images/tech/bigquery-sandbox-01-first-query/04-term-dryrun.webp)
*bq screen where the dry_run results for SELECT * and the same query with LIMIT 10 are identical — Source: self-rendered from bq CLI output*

In the CLI, the **--dry_run** option reports bytes processed without running the query

The official docs say dry runs are not charged

I estimated bytes processed for four queries against the same table

![Bar chart of bytes processed for four queries on the usa_names table](/assets/images/tech/bigquery-sandbox-01-first-query/en/05-chart.webp)
*Bar chart of bytes processed for four queries on the usa_names table — Source: self-rendered from measurements in bq-sandbox-blog*

SELECT * processes 194.9 MB

Adding LIMIT 10 left it <mark>unchanged at 194.9 MB</mark>

LIMIT only reduces the number of result rows; the amount of the table read stays the same

Narrowing the selected columns to just name and number drops it to **100.2 MB**

That is because BigQuery stores data by column and reads only the columns you pick

The TOP 10 query with WHERE year >= 2000 actually went up to 150.7 MB

The year column used in the condition also has to be read, raising the columns processed to three

This table has no date partitions, so a WHERE condition cannot shrink the range that is read

How WHERE conditions cut bytes processed on a date-partitioned table is covered in <u>part 2, on partitions</u>

## Query cache

![bq screen querying run history and cache_hit values for the same query via INFORMATION_SCHEMA](/assets/images/tech/bigquery-sandbox-01-first-query/06-term.webp)
*bq screen querying run history and cache_hit values for the same query via INFORMATION_SCHEMA — Source: self-rendered from bq CLI output*

Running the same query again 3 seconds later processed **0 bytes**

It reused the cached result, and cache_hit was recorded as true

The pricing docs also state that results served from the cache are not charged

When I changed the line breaks of the same query in the console and ran it again, the cache did not apply

Bytes processed were again recorded as **150,693,282 bytes**

<u>If even one character of the query string differs</u>, the cache is not used and the table is read again

Run history is kept in the **INFORMATION_SCHEMA.JOBS_BY_PROJECT** view

Summing this month's bytes processed shows how much of the free 1 TiB you have used

## Queries the sandbox restricts

![bq screen where CREATE TABLE AS SELECT succeeds and UPDATE is rejected](/assets/images/tech/bigquery-sandbox-01-first-query/en/07-term-dml.webp)
*bq screen where CREATE TABLE AS SELECT succeeds and UPDATE is rejected — Source: self-rendered from bq CLI output*

**CREATE TABLE AS SELECT**, which creates a table from query results, ran normally

23,136 rows of name and gender combinations since 2000 were saved to bq_lab.top_names

Running an UPDATE statement on the same table was rejected

**DML queries are not allowed in the free tier**

An INSERT statement was rejected with the same message

Queries that fail with a DML error are not charged for bytes processed

Uploading a local CSV file with bq load succeeded

To change stored values, you have to <u>recreate the table with CREATE TABLE AS SELECT</u>

The expiration time of top_names was shown as **12:34 on December 20, 2026**

## Part 1 summary

![Summary card of five things confirmed in the part 1 exercise](/assets/images/tech/bigquery-sandbox-01-first-query/en/08-items.webp)
*Summary card of five things confirmed in the part 1 exercise — Source: self-rendered from measurements in bq-sandbox-blog*

In part 2, I measure how much partitions and clusters cut bytes processed, using the Wikipedia pageviews table

One day of Korean Wikipedia was estimated at **294.88 million bytes** or less

One day across all languages was 6,488.49 million bytes or less

## Sources

- [[Google Cloud] Using the BigQuery sandbox (limits, unsupported features)](https://docs.cloud.google.com/bigquery/docs/sandbox)
- [[Google Cloud] BigQuery pricing (on-demand pricing, rounding up to MB, 10 MB minimum, free cache)](https://cloud.google.com/bigquery/pricing)
- [[Google Cloud] Running queries and dry runs (dry runs free)](https://docs.cloud.google.com/bigquery/docs/running-queries)
- [[SSA] usa_names source data (US Social Security Administration name statistics)](http://www.ssa.gov/OACT/babynames/limits.html)
- Exchange rate: converted at $1 ≈ ₩1,330 (2026-10-21)
