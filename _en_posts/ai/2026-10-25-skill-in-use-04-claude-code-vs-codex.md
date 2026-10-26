---
title: "Skills in Practice (4) — One SKILL.md, 16 Runs Compared in Claude Code and Codex"
description: "Following the Agent Skills standard now moved to AAIF, the same release-note skill was run 16 times in Claude Code and Codex to compare output format and skill folders"
date: 2026-10-25
category: AI
subcategory: Explainer
tags: [agent-skills, claude-code, codex, aaif, skill-md]
image: /assets/og/en-2026-10-25-skill-in-use-04-claude-code-vs-codex.png
---

I put the same SKILL.md file into Claude Code and Codex and compared how the two tools behave
On October 22, Anthropic donated the **Agent Skills** standard to AAIF

I made one small skill that writes release notes and ran it 16 times in total across the two tools
The output had the same format <mark>all 16 times</mark>, while the folder that stores skills differed between the two tools

🔗 Link - https://blog.naver.com/rottensweetpotato/224406152414

![Claude Code and OpenAI logos side by side](/assets/images/ai/skill-in-use-04-claude-code-vs-codex/01-hero-vs.webp)
*Claude Code and OpenAI logos side by side*

## The standard changes hands

![Front page of the official Agent Skills documentation](/assets/images/ai/skill-in-use-04-claude-code-vs-codex/02-photo-agentskills.webp)
*Front page of the official Agent Skills documentation — Source: Agent Skills*

The recipient of the donation is the **Agentic AI Foundation (AAIF)**
The Agent Skills name, logo, GitHub organization, and the agentskills.io domain were transferred

AAIF is a foundation under the Linux Foundation
Anthropic founded it together with Block and OpenAI

The same foundation also holds **MCP**, which Anthropic donated earlier
If MCP is the spec for connecting tools, a skill is a folder that stores work procedures and reference material as files

| Item | Figure |
| :--- | :--- |
| Supported agent platforms | **70+** |
| Published skills | 1 million |
| Cumulative installs | <mark>about 280 million</mark> |

ChatGPT, Cursor, GitHub Copilot, and VS Code are on the support list
It said it will ship versions going forward and set up a formal proposal process and skill security guidelines

### 📄 What the standard defines

A skill is a folder containing a single SKILL.md
The top of SKILL.md must have two values, **name** and **description**

name is up to 64 characters of lowercase letters, digits, and hyphens, and must match the folder name
description is up to 1,024 characters and says both what the skill does and when to use it

Tools read only the name and description at first
They read the SKILL.md body only when a request matches the skill description

When the SKILL.md body needs a reference file, the tool <mark>reads that file</mark>

## The practice skill

![Contents of the practice skill's SKILL.md](/assets/images/ai/skill-in-use-04-claude-code-vs-codex/03-term-skill.webp)
*Contents of the practice skill's SKILL.md — Source: self-rendered from a file I wrote*

The practice skill is named **release-note-ko**
It takes a list of commits and turns it into a Korean release note

I added two check items so that whether the skill ran can be confirmed from the output alone
Section titles are written only in references/sections.md, not in SKILL.md

If those titles appear verbatim in the output, it means the tool <u>read the reference file too</u>
If the last line **생성: release-note-ko v1** ("Generated: release-note-ko v1") appears, it means it followed the SKILL.md body

### 📁 Two folders

![Skill source folder and symbolic link structure](/assets/images/ai/skill-in-use-04-claude-code-vs-codex/en/04-term.webp)
*Skill source folder and symbolic link structure — Source: self-rendered from my own run*

| Tool | Folder where it looks for skills |
| :--- | :--- |
| Codex | **.agents/skills** |
| Claude Code | **.claude/skills** |

I stored the source only in .agents/skills and created a <mark>symbolic link</mark> in the Claude Code folder
Not storing the files twice prevents changes from landing in only one tool's copy

When I removed the symbolic link for a moment and ran Claude Code again, it <mark>could not find</mark> the skill
Claude Code 2.1.310 does not read .agents/skills, so the link is needed

## How it was measured

I fed in the same **five lines** of commits and called the skill in two ways

| Method | Prompt | Runs |
| :--- | :--- | :--- |
| Automatic invocation | Write a release note | **5** per tool |
| Explicit invocation | /name or $name | 3 per tool |
| Control | Folder without the skill | 1 per tool |

Claude Code ran the Sonnet 5.5 model via claude -p
Codex used GPT-6.1 Sol via codex exec

Both tools used default settings, and Codex ran in a read-only sandbox

Since the models differ, response times and wording are <mark>for reference only</mark>, not a tool comparison
What this test checked is whether the two tools follow the same skill file's instructions the same way

## Results

![Run log of Codex reading SKILL.md and then the reference file](/assets/images/ai/skill-in-use-04-claude-code-vs-codex/05-term-codex.webp)
*Run log of Codex reading SKILL.md and then the reference file — Source: self-rendered from my own run log*

| Type | Claude Code | Codex |
| :--- | :--- | :--- |
| Automatic invocation | **5/5** | **5/5** |
| Explicit invocation | 3/3 | 3/3 |
| Control | <mark>0/1</mark> | <mark>0/1</mark> |

All 16 runs output the three section titles and the last line <mark>exactly</mark>
All five items also ended in "~했습니다" (the formal past-tense ending)

In the control without the skill, the two tools used <mark>different titles</mark>
Claude Code sorted items into four categories: new features, bug fixes, docs, and other

Codex output a one-sentence summary and a five-line list with no titles

### 🔍 Reading order

The Codex log shows it reading SKILL.md first and then sections.md
All five automatic invocations followed the same order

Claude Code took **4** conversation turns with automatic invocation and 2 with explicit invocation
Explicit invocation appears to preload the skill body, cutting the skill discovery step

### 📊 Response time

![Bar chart of median response time by skill invocation method](/assets/images/ai/skill-in-use-04-claude-code-vs-codex/en/06-chart.webp)
*Bar chart of median response time by skill invocation method — Source: self-rendered from my own measurements*

Response time was measured <u>from the start of the CLI run to process exit</u>
Claude Code took 14–19 seconds with automatic invocation and 9–14 seconds with explicit invocation

Codex took 9–40 seconds with automatic invocation, and 12 and 15 seconds with explicit invocation
One explicit invocation took <mark>451 seconds</mark>, but the log had no errors and the output was normal

The median tokens Codex used was 8,545 for runs with the skill and 7,599 for the control
Reading SKILL.md and the reference file used about 950 extra tokens

## Trying it yourself

![Concept shot of one skill folder connected to two workbenches](/assets/images/ai/skill-in-use-04-claude-code-vs-codex/07-agy.webp)
*Concept shot of one skill folder connected to two workbenches — Source: concept shot · self-generated with agy*

### 🧩 Lining up the folders

Put the source in the repository's **.agents/skills/name/** folder
For Claude Code, create a symbolic link with the same name under .claude/skills

Personal skills go in the folder of the same name in your home directory
For Codex that is ~/.agents/skills, and for Claude Code ~/.claude/skills

If the name value and the folder name differ, it violates the standard, so <u>make the two names match exactly</u>

### ✍️ Writing the description

Both tools first pick which skill to use based on what the description says
Including the phrases users will actually type in the description makes automatic invocation more likely

This skill's description lists **릴리스 노트, 변경 사항 정리, 배포 노트** (release notes, change summary, deployment notes) in Korean
The skill was invoked automatically in all 5 Korean requests

### ⚙️ Differences between the tools

| Item | Claude Code | Codex |
| :--- | :--- | :--- |
| Explicit invocation | /release-note-ko | **$release-note-ko** |
| Model in this test | Sonnet 5.5 | GPT-6.1 Sol |
| ChatGPT on the web | Not applicable | Must be put in a plugin |

Codex can turn off automatic invocation with an agents/openai.yaml setting inside the skill folder
Just write **allow_implicit_invocation: false**

ChatGPT on the web cannot use a standalone skill directly
Only skills included in a plugin can be used

🔗 Link - https://blog.naver.com/rottensweetpotato/224406152414

![Summary card of the Agent Skills test across the two tools](/assets/images/ai/skill-in-use-04-claude-code-vs-codex/en/08-items.webp)
*Summary card of the Agent Skills test across the two tools — Source: self-rendered from my own measurements*

## Sources

- [[Anthropic] Donating Agent Skills to the Agentic AI Foundation (2026-10-22, scope of donation, number of supported platforms)](https://www.anthropic.com/news/donating-agent-skills-to-the-agentic-ai-foundation)
- [[Agent Skills] Specification (required SKILL.md values, progressive loading)](https://agentskills.io/specification)
- [[OpenAI] Build skills (Codex skill folders, $ invocation, agents/openai.yaml)](https://learn.chatgpt.com/docs/build-skills)
- [[Claude Code Docs] Skills (Claude Code skill folders)](https://code.claude.com/docs/en/skills)
- Test environment: macOS, Claude Code 2.1.310 (Sonnet 5.5), Codex CLI 0.164.0 (GPT-6.1 Sol, reasoning high), 2026-10-25
