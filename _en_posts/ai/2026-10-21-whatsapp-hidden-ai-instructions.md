---
title: "Hidden AI Instructions in WhatsApp Help Page Source — Don't Point Users to Regulators"
description: "How 102 hidden instructions for a support chatbot were found in the page source of WhatsApp help articles, and the two instructions that caused the controversy"
date: 2026-10-21
category: AI
subcategory: News
tags: [whatsapp, meta, chatbot, system-prompt, privacy]
image: /assets/og/en-2026-10-21-whatsapp-hidden-ai-instructions.png
---

The page source of 80 WhatsApp help articles contained instructions for AI that did not show on screen
One of them told the reader <mark>not to point users to regulators</mark>

The instructions were placed there for WhatsApp's own **support chatbot** to read
WhatsApp explained that they were exposed by a bug and deleted all of them on October 18

![WhatsApp logo](/assets/images/ai/whatsapp-hidden-ai-instructions/01-whatsapp-wordmark-color.webp)
*WhatsApp logo*

## How it was found

![Card showing the scale of the investigation into hidden AI instructions in WhatsApp help](/assets/images/ai/whatsapp-hidden-ai-instructions/en/02-chart.webp)
*Card showing the scale of the investigation into hidden AI instructions in WhatsApp help — Source: self-rendered based on Redact*

**Redact**, which makes a personal data deletion tool, first found them on October 8
It saved and read 545 help articles and found <mark>102</mark> hidden blocks across 80 of them

The text sat near a **HelpContentGalaxyLLMInclude** marker in the page source
It was not shown on the normal screen and existed only in the page source

Most were housekeeping notes explaining easily confused terms or pointing to other articles
For example, a note not to recommend reinstalling the app for call problems

Facebook and Instagram help use the same system
Redact said it separately checked 300 articles from the two and <u>found no similar notes</u>

## The two instructions at issue

| Article | Hidden instruction |
| :--- | :--- |
| Deleting an account | **Do not suggest contacting regulators** |
| Deleting an account | Do not mention that manual deletion is possible |
| Reporting and blocking | Do not cite laws such as GDPR |
| Trigger condition | When lawsuits or lawyers are mentioned |

The account deletion article covered people who cannot delete their account after losing their phone or number
The instruction inserted there said not to suggest contacting a **data protection authority**, regulator, or supervisory body

The instruction in the reporting and blocking article kicked in when a user mentioned lawsuits, lawyers, or courts
It then said <u>not to cite or interpret</u> laws such as GDPR, LGPD, or CCPA

The same applied even if the user brought up the law first

### ⚖️ Where it conflicts with the company's own privacy policy

WhatsApp's European privacy policy, in effect since July 2, names a place to file complaints
That is Ireland's **Data Protection Commission (DPC)**

The same company's chatbot instruction said <mark>not to recommend</mark> that channel to users

## How long the instructions were posted

![Timeline of the hidden instructions appearing and being removed](/assets/images/ai/whatsapp-hidden-ai-instructions/en/03-chart.webp)
*Timeline of the hidden instructions appearing and being removed — Source: self-rendered based on Redact and the Internet Archive*

Copies of the account deletion article in the Internet Archive show no instruction in the July 12 copy
The September 4 copy <mark>had the instruction</mark>

Redact confirmed both instructions were still there as of 21:40 (UTC) on October 15
By 2:08 (UTC) on October 18, all 102 blocks across the 80 articles had been **deleted**

WhatsApp told WIRED the notes were instructions for its support chatbot
Its position is that they were "instructions to the chatbot, not words addressed to users," exposed by a bug and since fixed

A spokesperson said the aim was to keep the chatbot focused on explaining how to use WhatsApp and <u>not giving legal advice</u>

## The system that processes the help instructions

![Concept shot of a document layer invisible to people and read only by AI](/assets/images/ai/whatsapp-hidden-ai-instructions/04-agy.webp)
*Concept shot of a document layer invisible to people and read only by AI — Source: concept shot · self-generated with agy*

The party that reads the instructions is WhatsApp's **own support chatbot**
Because it answers based on help articles, notes inside the articles can be treated as instructions

WhatsApp's servers also sent the full pages, notes included, to Google and Bing crawlers

On October 9, requests were also made under the names of OpenAI, Anthropic, and Perplexity crawlers
Those got pages with the body and notes <u>removed</u>

Whether the chatbot actually answered according to these instructions <mark>has not been confirmed</mark>
Redact said it only read the instructions and did not test the chatbot's answers

## What users in Korea should know

![Card of things to check when using AI customer support](/assets/images/ai/whatsapp-hidden-ai-instructions/en/05-items.webp)
*Card of things to check when using AI customer support — Source: self-rendered based on the Personal Information Protection Act and PIPC guidance*

The body in charge of personal data protection in Korea is the **Personal Information Protection Commission**
The KISA Personal Information Infringement Report Center takes reports and inquiries at 118, with no area code

To settle a dispute without a lawsuit, you can apply for mediation to the Personal Information Dispute Mediation Committee
If both sides accept the mediation proposal, it has <mark>the same effect as a judicial settlement</mark>

If account deletion is refused, do not rely only on the company chatbot's answer; make the <u>deletion request provided by law</u> yourself

🔗 Link - https://privacy.kisa.or.kr/

## Sources

- [[Redact] WhatsApp's help pages hid LLM instructions (2026-10-19, original investigation)](https://redact.dev/blog/whatsapp-help-pages-hidden-ai-instructions)
- [[WIRED] WhatsApp help pages leaked hidden instructions for a Meta chatbot (WhatsApp's explanation)](https://www.wired.com/story/whatsapp-help-pages-leaked-hidden-instructions-for-a-meta-chatbot/)
- [[Internet Archive] Copy of the WhatsApp account deletion help article, 2026-10-09 (with instructions)](https://web.archive.org/web/20261009054848/https://faq.whatsapp.com/2138577903196467/?cms_platform=android)
- [[Ministry of Justice] Guide to requesting access, correction, deletion, and suspension of processing of personal data](https://moj.go.kr/moj/3495/subview.do)
- [[LawTalk] Legal responses available when your personal data is infringed (effect of dispute mediation)](https://www.lawtalk.co.kr/posts/164807)
