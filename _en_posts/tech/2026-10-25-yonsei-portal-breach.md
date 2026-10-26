---
title: "Yonsei University Portal Hacked — Student IDs and Phone Numbers of 10,000+ Leaked"
description: "How an intrusion into the Yonsei Portal Service leaked the student IDs, phone numbers, and emails of about 10,000 members, and how to check for exposure and guard against smishing"
date: 2026-10-25
category: Tech
subcategory: News
tags: [yonsei-university, data-breach, smishing, personal-information, security]
image: /assets/og/en-2026-10-25-yonsei-portal-breach.png
---

The **Yonsei Portal Service** was breached from outside, and members' personal data leaked
According to press reports, about <mark>10,000</mark> people, including current students and alumni, are affected

Student IDs, phone numbers, and emails were included
The university said unique identifiers such as resident registration numbers were not among the leaked items

![Official Yonsei University symbol and wordmark](/assets/images/tech/yonsei-portal-breach/01-logo-yonsei.webp)
*Official Yonsei University symbol and wordmark*

## Timeline

![Timeline from the Yonsei Portal intrusion to the leak lookup](/assets/images/tech/yonsei-portal-breach/en/02-chart.webp)
*Timeline from the Yonsei Portal intrusion to the leak lookup — Source: self-rendered based on Yonsei University's notice and Seoul Shinmun reporting*

The intrusions happened at <u>7:41–7:43 p.m. on October 20</u> and <u>10:04–10:11 a.m. on October 21</u>

An unauthorized outsider accessed the Yonsei Portal and looked up member information through abnormal means
The university blocked access from the attacker's IP addresses and the leak paths it identified

It reported to the Personal Information Protection Commission, KISA, and the Ministry of Education, and **requested an investigation**
According to Seoul Shinmun, the Seoul Metropolitan Police Agency's cyber investigation unit has opened a preliminary inquiry

On October 22, the university posted an **apology** in the name of its Director of Information and Communications
From 1 p.m. that day, it began offering individual lookups of leaked items and running a damage response call center

### 🚩 Early warning

Seoul Shinmun reported that a sales post appeared on Telegram six days before the intrusion
On October 14, a post offered access to a Yonsei domain site for <mark>about $300 (₩420,000)</mark>

The seller claimed to have installed a web shell on a web server

On October 16, the university shared the post internally and asked for checks
But it judged the post to show no sign of an actual breach

The university's explanation is that no hacking damage had been confirmed at that point
Whether the sales post and this intrusion involve the same attacker <mark>has not been confirmed</mark>

🔗 Link - https://blog.naver.com/rottensweetpotato/224434109837

## Leaked items and scope

The leaked items listed in the university's notice fall into personal data and system management information
The items leaked <mark>vary by user</mark>

| Type | Items |
| :--- | :--- |
| Contact | **Phone number, email** |
| Identity | Student ID (employee ID), user name |
| Affiliation | User type, department name, status code name |
| Access | Last login IP, campus extension number |

System management information includes a login identification key, department code, password error count, and password change date
It also included user status code, last login date and time, and first registration date

### ✅ Items excluded from the leak list

| Item | Leaked |
| :--- | :--- |
| Resident registration number | **No** |
| Alien registration number, passport number | No |
| Sensitive information | No |
| The password itself | <mark>Not on the notice's list</mark> |

The university did not explain what the login identification key is or whether it can be used for other accounts

### 🔢 The figure of 10,000

The university's notice <mark>does not state</mark> how many people were affected
The figure of about 10,000 comes from press reports such as Asia Today and New Daily, without a disclosed source

Seoul Shinmun reported the figure as the university's provisional estimate
The final scale will be confirmed by a university announcement or a PIPC investigation

## Attack method and timing of the report

![Concept shot of a malicious script hidden on a university portal server](/assets/images/tech/yonsei-portal-breach/03-agy.webp)
*Concept shot of a malicious script hidden on a university portal server — Source: concept shot · self-generated with agy*

The university only described the method as **lookups through abnormal means**
The type of vulnerability and the initial entry path have not been disclosed

The two intrusions lasted <mark>3 minutes</mark> and <mark>7 minutes</mark>
Whether a web shell was actually used in the attack will have to wait for the investigation

The Personal Information Protection Act requires a report <u>within 72 hours of learning</u> of a leak affecting 1,000 or more people
Notifying the data subjects has the same deadline

The university reported on October 21, the day of the second intrusion, and began individual notifications on the 22nd
It completed the report and notifications within the legal deadline

The PIPC, however, separately investigates whether the **duty to take safety measures** was met, apart from the timing of the report
Whether the checks after the October 14 sales post were sufficient could also be part of that

## Recurring university portal incidents

![Horizontal bar chart of the scale of recently known university data leaks](/assets/images/tech/yonsei-portal-breach/en/04-chart.webp)
*Horizontal bar chart of the scale of recently known university data leaks — Source: self-rendered based on Boan News, press reports, and the Hankook Ilbo*

At Sogang University, the integrated login system was attacked on August 11, leaking data on about <mark>180,000</mark> people
The university only became aware of the attack three days later, on August 14

The Sogang leak included names, student IDs, emails, phone numbers, and **encrypted integrated passwords**
Seoul Shinmun described that incident as an automated credential-stuffing attack

The Hankook Ilbo reported that Seoul National University suffered 28 hacks over six years from 2021, leaking 1,132 personal records
University portals hold data on alumni and staff as well as current students in one place, which widens the damage

## What to do now

![Personal Information Protection Commission logo](/assets/images/tech/yonsei-portal-breach/05-logo-pipc.webp)
*Personal Information Protection Commission logo*

### 🔎 Check whether you were affected

Check the **notice of personal data leak and apology** under announcements on the university's main website
You can look up whether your information was included through the link to check leaked items posted in the notice

🔗 Link - https://www.yonsei.ac.kr/bbs/sc/58/944433/artclView.do

The university notified affected people individually by text message (LMS) and email
<u>Type the address into the address bar yourself</u> to get there

### 📵 Secondary damage

The university said it <mark>does not send text messages containing links</mark> about this incident
If you get texts, calls, or emails impersonating the university, do not tap the links

With a student ID and phone number together, it is easy to impersonate notices about scholarships, tuition, or academic records
Do not respond to contacts asking for personal or financial information

### 🔑 Accounts

Passwords are not among the leaked items
If you use the same password as the Yonsei Portal on other sites, **changing it is the safer choice**

### ☎️ Inquiries and reports

If you suspect misuse, contact the damage response call center at **02-2123-7015~7017**
Email inquiries go to privacy@yonsei.ac.kr

For personal data infringement reports and consultation, call <mark>118</mark>, no area code

🔗 Link - https://privacy.kisa.or.kr

### 📌 Open questions

- The **final number of people affected** and the entry path, and whether the university will announce them
- Whether the Telegram sales post is connected to this intrusion
- What the login identification key is and whether it is used in other systems
- Whether the PIPC opens an investigation and finds a <mark>breach of the duty to take safety measures</mark>
- Reported cases of smishing that misuse the leaked data

![Summary card of responses to the Yonsei portal hack](/assets/images/tech/yonsei-portal-breach/en/06-items.webp)
*Summary card of responses to the Yonsei portal hack — Source: self-rendered based on Yonsei University's notice*

## Sources

- [[Yonsei University] Notice of personal data leak and apology (2026-10-22, Office of Information and Communications)](https://www.yonsei.ac.kr/bbs/sc/58/944433/artclView.do)
- [[Seoul Shinmun] Despite signs of hacking, data of 10,000+ at Yonsei leaked (2026-10-23, Telegram sales post, police inquiry)](https://www.seoul.co.kr/news/society/accident/2026/10/23/20261023010010)
- [[DailySecu] Yonsei Portal Service hacked (leaked items, call center)](https://www.dailysecu.com/news/articleView.html?idxno=209012)
- [[Asia Today] About 10,000 affected by Yonsei hack (2026-10-22, scale of damage)](https://www.asiatoday.co.kr/kn/view.php?key=20261022010007445)
- [[New Daily] Yonsei portal hacked, about 10,000 students and alumni (2026-10-22)](https://www.newdaily.co.kr/site/data/html/2026/10/22/2026102200087.html)
- [[Boan News] Attack on Sogang's integrated login (2026-08-18, 180,000 people, leaked items)](https://www.boannews.com/news/articleView.html?idxno=145181)
- [[Hankook Ilbo] Seoul National University hacked 28 times in six years (2026-10-11)](https://www.hankookilbo.com/news/article/amp/A2026101121170001639)
- Exchange rate: converted at $1 ≈ ₩1,400
