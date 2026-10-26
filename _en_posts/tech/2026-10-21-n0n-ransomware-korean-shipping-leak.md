---
title: "Ransomware Group N0n Leaks Data from 12 Korean Firms, Including Pusan Newport and Dongkuk Steel"
description: "How the ransomware group N0n published internal data from 12 Korean shipping, port, and steel companies on the dark web after the negotiation deadline passed, and who is on the list"
date: 2026-10-21
category: Tech
subcategory: News
tags: [ransomware, n0n, data-breach, shipping, supply-chain-attack]
image: /assets/og/en-2026-10-21-n0n-ransomware-korean-shipping-leak.png
---

Internal data from 12 Korean shipping, port, and steel companies has been published on the dark web
After the negotiation deadline passed, the ransomware group **N0n** published downloadable archive files

This time the focus is **corporate business data** rather than customer personal information
It is not yet confirmed whether the 12 were each breached separately or leaked all at once through <mark>a single vendor</mark>

![Concept shot of data modules layered over a container terminal](/assets/images/tech/n0n-ransomware-korean-shipping-leak/01-agy.webp)
*Concept shot of data modules layered over a container terminal — Source: concept shot · self-generated with agy*

## Timeline

![Timeline of N0n's attacks on shipping and ports](/assets/images/tech/n0n-ransomware-korean-shipping-leak/en/02-chart.webp)
*Timeline of N0n's attacks on shipping and ports — Source: self-rendered based on SOCRadar, Cydome, and Boan News*

N0n is a new data theft and extortion group first identified on **September 18**
On October 12, it posted <mark>38</mark> shipping and logistics companies at once on its leak site

12 of them were Korean companies
Boan News first reported the list and the demand for each company on October 13

The publication deadline was October 19
Boan News reported on October 20 that, after the deadline passed, zip files that could actually be downloaded had been published

The group said this was the first batch and warned of <u>more releases until a deal is reached</u>

### 📋 The 12 Korean companies on the list

| Sector | Company |
| :--- | :--- |
| Port terminal | **Pusan Newport**, BNCT |
| Port terminal | Dongwon Global Terminal Busan, Masan iPort |
| Shipping | Korea Ferry, Polaris Shipping, Dong-A Tanker |
| Shipping agency | Samjoo Maritime, Saehan Marine |
| Logistics | Yusu Logistics, BKH ICD |
| Steel | **Dongkuk Steel** |

Being on the list does not by itself confirm a breach
As of October 14, not a single company had publicly acknowledged a breach

## Demands and company responses

![Bar chart of N0n's shipping and logistics victim claims by country](/assets/images/tech/n0n-ransomware-korean-shipping-leak/en/03-chart.webp)
*Bar chart of N0n's shipping and logistics victim claims by country — Source: self-rendered based on SOCRadar*

The 38 span 18 countries, with Korea the largest at <mark>12</mark>
Brazil and Indonesia followed with 4 each

### 💰 Demand by company

According to Boan News, the demand for **Pusan Newport** was about $12 million (₩16.8 billion)
For Yusu Logistics it was about $14 million (₩19.6 billion)

The figure for Dongkuk Steel varies by report
Boan News put it at about $10 million (₩14 billion), and Cydome at <mark>about $100 million (₩140 billion)</mark>

Each post comes with a **10% down payment negotiation** option
Cydome considered the ₩14 billion figure to match that down payment

N0n sets a different ransom for each company and wants to be paid in Bitcoin

### 🗣️ Company and agency positions

Dongkuk Steel said it "is aware of the matter and is currently responding"
It added that "this is only the hacking group's one-sided claim, and no actual damage has been confirmed"

**KISA** said it was aware of damage at several port companies and was notifying them of the breach
An IT staff member at one affected company said they were working out what leaked after receiving KISA's notice

## Signs pointing to a single vendor

![Bar chart of clues among the 38 that lead to one vendor](/assets/images/tech/n0n-ransomware-korean-shipping-leak/en/04-chart.webp)
*Bar chart of clues among the 38 that lead to one vendor — Source: self-rendered based on Cydome*

Maritime security firm **Cydome** published an analysis on October 15
Its assessment is that the data appears to be linked to **CyberLogitec**, a Seoul-based shipping software company

<mark>21</mark> of the 38 were CyberLogitec customers identifiable from public information

Seven sample files directly named the company or its products
The Pusan Newport sample was a test environment deployment list, and the BKH ICD sample was release notes for a terminal operating system

Cydome suggested that files from a single data archive may have been split up and posted by customer
It also pointed to a case where one post reused another post's sample file as is

### 🔍 What is not yet confirmed

CyberLogitec confirmed to Korean media that the Korean companies on the list are its customers
It said it had sent preventive notices to customers and that its **systems are operating normally**

As far as Cydome could confirm, CyberLogitec has not acknowledged a breach
Which systems were accessed and how, and whether N0n stole the data itself or bought it from a third party, <u>have not been confirmed</u>

SOCRadar noted that N0n got into earlier victims using accounts collected by **infostealers**
An infostealer is malware that gets installed on a PC and steals saved passwords

## Data claimed to be leaked and the scope of damage

| Type of data | Status |
| :--- | :--- |
| Internal spreadsheets, contracts, invoices | <mark>Published</mark> (Boan News) |
| Vessel schedules, export results | Published (Boan News) |
| System release notes, patch scripts | Samples confirmed (Cydome) |
| EDI container messages | Samples confirmed (Cydome) |
| User account lists and passwords | **Claimed**, some samples |
| Individual customer data | Not confirmed |

**EDI** is the electronic document format shipping lines and terminals use to exchange cargo information
Cydome considered that the EDI messages may also contain <mark>cargo information of other shipping lines</mark>

That means shippers and business partners not on the list may also be affected
If the account lists are genuinely leaked data, <u>unauthorized access to connected systems</u> becomes a risk as well

The Pusan Newport data sample SOCRadar checked was 1.5 GB with 774 files
Sample file dates ran from 2009 to August 2026, and example accounts from 2018 to 2022

## Reporting duties and what to do

Information and communications service providers must report within 24 hours of learning of a breach
This is an amended provision of the <mark>Network Act</mark> that took effect on August 14, 2024

If personal data is involved, a separate leak report is due within 72 hours under the Personal Information Protection Act
KISA advises that for a personal data leak caused by hacking, <u>the breach report and the leak report must each be filed</u>

SOCRadar recommended checking shared platforms first
EDI hubs, terminal system vendors, and file transfer services are the places that hold your data

![Card of actions by type of reader](/assets/images/tech/n0n-ransomware-korean-shipping-leak/en/05-items.webp)
*Card of actions by type of reader — Source: self-rendered based on SOCRadar recommendations and KISA guidance*

If you suspect hacking, use KISA's 118 hotline or the Boho Nara breach report

🔗 Link - https://www.boho.or.kr/

## Sources

- [[Boan News] Ransomware attack claimed on 12 Korean shipping and steel firms (2026-10-13, list and demands)](https://www.boannews.com/news/articleView.html?idxno=146345)
- [[Boan News] Hackers who attacked 12 Korean shipping and steel firms publish stolen data (2026-10-20)](https://www.boannews.com/news/articleView.html?idxno=146549)
- [[News Journalism] Dongkuk Steel targeted by hacking group (2026-10-13, Dongkuk Steel's position)](https://www.ngetnews.com/news/articleView.html?idxno=554411)
- [[Cydome] n0n extortion incident likely traces back to a single vendor (2026-10-15)](https://cydome.io/n0n-cyber-extortion-incident-involving-38-maritime-companies-likely-traces-back-to-a-single-vendor/)
- [[SOCRadar] n0n Group Puts Dozens of Global Ports and Shipping on Its Leak Site (count by country, recommendations)](https://socradar.io/blog/n0n-group-global-ports-shipping-leak/)
- [[ASEC] Ransom & Dark Web Issues, third week of October 2026](https://asec.ahnlab.com/ko/95822/)
- [[Boan News] Ministry of Science and ICT puts amended Network Act into effect (2024, 24-hour reporting duty)](https://m.boannews.com/html/detail.html?idx=132012)
- [[KISA] Personal data breach reporting and consultation (where to report)](https://www.kisa.or.kr/1030402)
- Exchange rate: converted at $1 ≈ ₩1,400
