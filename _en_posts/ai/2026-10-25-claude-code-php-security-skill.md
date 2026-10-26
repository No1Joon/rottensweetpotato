---
title: "A PHP Security Skill for Claude Code — 11 Flaws Found in a Gnuboard-Style Example App"
description: "How php-security-hardening, a Claude Code skill for security-checking PHP websites, is put together, and what it caught and missed in an example app seeded with flaws"
date: 2026-10-25
category: AI
subcategory: Explainer
tags: [claude-code, agent-skills, php, secure-coding, web-security]
image: /assets/og/en-2026-10-25-claude-code-php-security-skill.png
---

I built and published a skill that hands security checks of PHP websites to Claude Code

It is called **php-security-hardening**
It is included in the security plugin of the oh-my-skills repository on GitHub

I tested what the skill actually catches and misses with an example app deliberately seeded with flaws
It caught <mark>all 11</mark> seeded flaws, missed 1 comparison pattern, and has 1 advisory not yet reflected

![Official PHP logo](/assets/images/ai/claude-code-php-security-skill/01-hero-php.webp)
*Official PHP logo — Source: PHP Group / Colin Viebrock (CC BY-SA 4.0)*

## How the skill is put together

![Commands to install the plugin in Claude Code](/assets/images/ai/claude-code-php-security-skill/en/02-term.webp)
*Commands to install the plugin in Claude Code — Source: self-rendered based on the oh-my-skills README*

The skill is distributed through Claude Code's **plugin marketplace**
Add the marketplace and install the security plugin

To run it, enter **/security:php-security-hardening**

The SKILL.md body holds only the order and rules, and the long tables are split into separate files in the references folder
Claude reads only the file needed for each step, when it needs it

| File | When it is used |
| :--- | :--- |
| advisories/php2shell.md | **Responding to urgent advisories** |
| grep-patterns.md | Code checks |
| platforms-by-region.md | Platform-specific hardening |
| incident-response.md | Suspected breach |

### 🧭 Three modes

| Mode | When |
| :--- | :--- |
| A. Urgent response | Runtime vulnerabilities such as PHP2Shell |
| B. Full check | Code review, pre-release checks |
| C. Incident response | Web shells, suspicious processes |

While an urgent security advisory is in effect, every mode <mark>starts by checking the runtime version</mark>
The rule is to check for an unpatched runtime before code flaws

### 🛡️ Principles it keeps

The skill is **defense only**
It does not write attack code or payloads, and it refuses requests to scan other people's sites

Version information changes every week, so it rechecks php.net and the official advisories on every run
Temporary mitigations are to be labeled as <u>reducing attack exposure, not fixing the vulnerability</u>

## Structure validation

![Screen validating the marketplace and plugin with claude plugin validate](/assets/images/ai/claude-code-php-security-skill/en/03-term.webp)
*Screen validating the marketplace and plugin with claude plugin validate — Source: self-rendered from my own run*

Before publishing, I checked the manifests with Claude Code's validation command
Both the marketplace and the security plugin <mark>passed structure validation</mark>

The plugin version at the time of the check was **0.1.2**
The last change, on October 24, was a commit that fixed the PHP2Shell check procedure and a detection gap

## Testing on an example app

![Concept shot of a check picking out dangerous functions among example code](/assets/images/ai/claude-code-php-security-skill/04-agy.webp)
*Concept shot of a check picking out dangerous functions among example code — Source: concept shot · self-generated with agy*

I built the example app for testing myself, imitating the **Gnuboard** folder structure
It consists of bbs, adm, and data folders plus common.php

I deliberately inserted <mark>11</mark> common flaws and 1 line switching the session format across 5 files

The skill's identification table classifies the combination of common.php with bbs, adm, and data as Gnuboard 5 or Youngcart
Then I ran the search patterns in references/grep-patterns.md as written

### 🔎 Search results

![Actual output of searching the example app with the skill's patterns](/assets/images/ai/claude-code-php-security-skill/en/05-term.webp)
*Actual output of searching the example app with the skill's patterns — Source: self-rendered from my own run*

| Location | Category | Result |
| :--- | :--- | :--- |
| view.php:4 | SQL injection | **Caught** |
| view.php:5 | XSS | Caught |
| download.php:3 | Path manipulation | Caught |
| download.php:4 | File inclusion | Caught |
| upload.php:2 | File upload | Caught |
| upload.php:3 | Weak random numbers | Caught |

| Location | Category | Result |
| :--- | :--- | :--- |
| tool.php:2 | Command execution | **Caught** |
| tool.php:3 | Deserialization | Caught |
| tool.php:4 | phpinfo exposure | Caught |
| common.php:2 | Error screen exposure | Caught |
| view.php:6 | Weak hash | Caught |

The 11 search patterns each caught one of the 11 flaws
False positives were <mark>0</mark> in this example, but since the code holds only flaws, a real app will produce more

The skill also says to treat search results only as **candidates** and to review the surrounding code to decide whether each is a real flaw

### ❌ What it missed

view.php:6 is a line comparing an md5 hash with ==
The md5 pattern caught the weak hash, but the <mark>loose comparison pattern</mark> did not catch this line

The loose comparison pattern matches only when a variable name such as hash, token, or pass comes right after ==
In this line, the array name row comes first after ==, so it does not match the pattern

### 🕒 Advisories not yet included

As of October 24, the urgent advisory table has only **PHP2Shell**
The session vulnerability CVE-2026-115560, disclosed October 23, is <mark>not yet</mark> in the table or patterns

The session format switch line seeded in the example common.php was caught with a search pattern I added separately

The PHP2Shell temporary measures include the same mitigation setting, so the operational steps overlap
Still, the table and patterns need to be updated to add this CVE separately

## Checking the runtime

![Screen checking the web-side PHP version with php-fpm -v](/assets/images/ai/claude-code-php-security-skill/en/06-term.webp)
*Screen checking the web-side PHP version with php-fpm -v — Source: self-rendered from my own run*

The skill says to look at the **version per SAPI** that handles web requests, not the command-line php
Distributions sometimes keep the version number and apply only security patches, so it checks the changelog too

The PHP-FPM version in the test environment was <mark>8.4.11</mark>
That is below 8.4.27, the PHP2Shell fixed version, making it top priority (P0) by the skill's standard

It is for local development and takes no outside requests, but if the same version were deployed to a server, it would need updating right away
The PHP2Shell timeline and fixed versions are covered in an earlier post

🔗 Link - https://blog.naver.com/rottensweetpotato/224450769485

## Fitting the Korean environment

![Official Claude icon](/assets/images/ai/claude-code-php-security-skill/07-logo-claude.webp)
*Official Claude icon*

| Target | What the skill checks |
| :--- | :--- |
| Gnuboard, Youngcart | **Block execution in data/**, restrict access to adm/ |
| Youngcart payments | Match order amount against PG-approved amount |
| Rhymix, XE | Migrate off XE 1.x |
| PG SDKs | Hardcoded keys, webhook signatures |
| Hosting | PHP versions at Cafe24, Gabia, Dothome |

For vulnerability information, it uses **KISA Boho Nara** as the Korean source and ties it to the safety-measure standards of the Personal Information Protection Act
Platform information for other countries such as Japan, China, and Germany is in tables of the same format

## Cautions when using it

Search patterns are a first-stage filter
To confirm a flaw, you have to read the code to see whether user input actually reaches that function

Do not patch external libraries in the vendor folder directly; raise their versions with <u>composer audit</u>
Before changing server settings, it is set to back up and show a diff first

Zero search results <mark>does not mean it is safe</mark>
Even in incident response mode, if the search results show no flaws, it only records that nothing was found

![Summary card of the PHP security skill test](/assets/images/ai/claude-code-php-security-skill/en/08-items.webp)
*Summary card of the PHP security skill test — Source: self-rendered from my own measurements*

🔗 oh-my-skills repository - https://github.com/No1Joon/oh-my-skills

## Sources

- [[GitHub] No1Joon/oh-my-skills (php-security-hardening skill, as of the 2026-10-24 commit)](https://github.com/No1Joon/oh-my-skills)
- [[PHP] Security advisory: PHP2Shell (2026-10-21, fixed versions)](https://www.php.net/archive/2026.php)
- [[PHP] Informational advisory: Session upload progress (2026-10-23, CVE-2026-115560)](https://www.php.net/archive/2026.php)
- [[Claude Code Docs] Plugins and marketplaces](https://code.claude.com/docs/en/plugins)
- Test environment: macOS, PHP 8.4.11 CLI and FPM, Claude Code 2.1.310, 2026-10-25
