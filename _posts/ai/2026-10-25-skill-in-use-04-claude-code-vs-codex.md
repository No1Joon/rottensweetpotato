---
title: "스킬 실사용 (4) — SKILL.md 하나로 Claude Code와 Codex 16회 실행 비교"
description: "AAIF 로 이관된 Agent Skills 표준을 따라 같은 릴리스 노트 스킬을 Claude Code 와 Codex 에서 16회 실행해 출력 형식과 스킬 폴더 차이를 비교합니다"
date: 2026-10-25
category: AI
subcategory: Explainer
tags: [agent-skills, claude-code, codex, aaif, skill-md]
image: /assets/og/2026-10-25-skill-in-use-04-claude-code-vs-codex.png
---

같은 SKILL.md 파일 하나를 Claude Code와 Codex에 넣어 두 도구의 동작을 비교했습니다
Anthropic은 10월 22일 **Agent Skills** 표준을 AAIF에 기증했습니다

릴리스 노트를 쓰는 작은 스킬을 하나 만들어 두 도구에서 총 16회 실행해 봤습니다
결과는 <mark>16번 모두</mark> 같은 형식이었고, 스킬을 저장하는 폴더는 두 도구에서 서로 달랐습니다

🔗 링크 첨부 - https://blog.naver.com/rottensweetpotato/224406152414

![Claude Code와 OpenAI 로고 비교](/assets/images/ai/skill-in-use-04-claude-code-vs-codex/01-hero-vs.webp)
*Claude Code와 OpenAI 로고 비교*

## 표준 이관 소식

![Agent Skills 공식 문서 첫 화면](/assets/images/ai/skill-in-use-04-claude-code-vs-codex/02-photo-agentskills.webp)
*Agent Skills 공식 문서 첫 화면 — 출처: Agent Skills*

기증 대상은 **Agentic AI Foundation(AAIF)**입니다
Agent Skills의 이름, 로고, GitHub 조직, agentskills.io 도메인이 이관됐습니다

AAIF는 Linux Foundation 산하 재단입니다
Anthropic이 Block, OpenAI와 함께 세웠습니다

같은 재단에는 Anthropic이 앞서 기증한 **MCP**도 있습니다
MCP가 도구를 연결하는 규격이라면, 스킬은 작업 절차와 참고 자료를 파일로 저장한 폴더입니다

| 항목 | 수치 |
| :--- | :--- |
| 지원 에이전트 플랫폼 | **70곳 이상** |
| 공개된 스킬 | 100만 개 |
| 누적 설치 | <mark>약 2억 8천만 회</mark> |

ChatGPT, Cursor, GitHub Copilot, VS Code가 지원 목록에 포함돼 있습니다
앞으로 버전을 출시하고 공식 제안 절차와 스킬 보안 지침을 마련한다고 밝혔습니다

### 📄 표준이 정한 것

스킬은 SKILL.md 하나가 든 폴더입니다
SKILL.md 맨 위에는 **name**과 **description** 두 값이 반드시 있어야 합니다

name은 영문 소문자, 숫자, 하이픈으로 64자까지이고 폴더 이름과 같아야 합니다
description은 1,024자까지이며 무엇을 하는지와 언제 쓰는지를 함께 적습니다

도구는 처음에 이름과 설명만 읽습니다
요청과 스킬 설명이 일치할 때만 SKILL.md 본문을 읽습니다

도구는 SKILL.md 본문에서 참조 파일이 필요할 때 <mark>해당 파일을 읽습니다</mark>

## 실습 스킬 구성

![실습 스킬의 SKILL.md 내용](/assets/images/ai/skill-in-use-04-claude-code-vs-codex/03-term-skill.webp)
*실습 스킬의 SKILL.md 내용 — 출처: 직접 작성 파일 자가 렌더*

실습 스킬 이름은 **release-note-ko**입니다
커밋 목록을 받아 한국어 릴리스 노트로 정리합니다

출력만 보고 스킬의 실행 여부를 확인할 수 있도록 검증 항목을 두 개 넣었습니다
섹션 제목은 SKILL.md가 아니라 references/sections.md에만 적었습니다

출력에 그 제목이 그대로 나오면 도구가 <u>참조 파일까지 읽었다는 뜻</u>입니다
마지막 줄 **생성: release-note-ko v1**이 나오면 SKILL.md 본문을 따랐다는 뜻입니다

### 📁 폴더 두 곳

![스킬 원본 폴더와 심볼릭 링크 구조](/assets/images/ai/skill-in-use-04-claude-code-vs-codex/04-term.webp)
*스킬 원본 폴더와 심볼릭 링크 구조 — 출처: 직접 실행 화면 자가 렌더*

| 도구 | 스킬을 찾는 폴더 |
| :--- | :--- |
| Codex | **.agents/skills** |
| Claude Code | **.claude/skills** |

원본은 .agents/skills에만 저장하고 Claude Code용 폴더에는 <mark>심볼릭 링크</mark>를 생성했습니다
파일을 중복 저장하지 않아 한 도구의 파일에만 수정 사항이 반영되는 문제를 방지합니다

심볼릭 링크를 잠시 제거하고 Claude Code를 한 번 더 실행해 보니 스킬을 <mark>찾지 못했습니다</mark>
Claude Code 2.1.310은 .agents/skills를 읽지 않으니 링크가 필요합니다

## 실측 방법

같은 커밋 **다섯 줄**을 입력하고 두 방식으로 스킬을 호출했습니다

| 방식 | 프롬프트 | 횟수 |
| :--- | :--- | :--- |
| 자동 호출 | 릴리스 노트를 써 줘 | 도구마다 **5회** |
| 명시 호출 | /이름 또는 $이름 | 도구마다 3회 |
| 대조군 | 스킬 없는 폴더 | 도구마다 1회 |

Claude Code는 claude -p로 Sonnet 5.5 모델을 실행했습니다
Codex는 codex exec로 GPT-6.1 Sol을 썼습니다

두 도구 모두 기본 설정이고, Codex는 읽기 전용 샌드박스에서 실행했습니다

모델이 다르니 응답 시간과 문장 표현은 도구 비교가 아니라 <mark>참고값</mark>입니다
이번 실측에서 확인한 것은 두 도구가 같은 스킬 파일의 지시를 똑같이 따르는지입니다

## 결과

![Codex가 SKILL.md와 참조 파일을 차례로 읽은 실행 로그](/assets/images/ai/skill-in-use-04-claude-code-vs-codex/05-term-codex.webp)
*Codex가 SKILL.md와 참조 파일을 차례로 읽은 실행 로그 — 출처: 직접 실행 로그 자가 렌더*

| 구분 | Claude Code | Codex |
| :--- | :--- | :--- |
| 자동 호출 | **5/5** | **5/5** |
| 명시 호출 | 3/3 | 3/3 |
| 대조군 | <mark>0/1</mark> | <mark>0/1</mark> |

16번 모두 섹션 제목 세 개와 마지막 줄이 <mark>정확히</mark> 출력됐습니다
항목 다섯 개도 모두 "~했습니다"로 끝났습니다

스킬이 없는 대조군에서는 두 도구가 <mark>서로 다른 제목</mark>을 썼습니다
Claude Code는 새 기능, 버그 수정, 문서, 기타 네 범주로 분류했습니다

Codex는 제목 없이 요약 한 문장과 목록 다섯 줄을 출력했습니다

### 🔍 읽는 순서

Codex 로그에는 SKILL.md를 먼저 읽고 sections.md를 이어 읽는 과정이 그대로 남았습니다
자동 호출 5회 모두 같은 순서였습니다

Claude Code는 자동 호출 때 대화 턴이 **4번**, 명시 호출 때는 2번이었습니다
명시 호출은 스킬 본문을 미리 로드해 스킬 탐색 단계가 줄어든 결과로 보입니다

### 📊 응답 시간

![스킬 호출 방식별 응답 시간 중앙값 막대 차트](/assets/images/ai/skill-in-use-04-claude-code-vs-codex/06-chart.webp)
*스킬 호출 방식별 응답 시간 중앙값 막대 차트 — 출처: 직접 측정 기반 자가 렌더*

응답 시간은 <u>CLI 실행 시작부터 프로세스 종료까지</u> 측정한 값입니다
Claude Code는 자동 호출 14~19초, 명시 호출 9~14초였습니다

Codex는 자동 호출 9~40초, 명시 호출은 12초와 15초였습니다
명시 호출 중 한 번은 <mark>451초</mark>가 걸렸지만 로그에 오류는 없었고 출력은 정상이었습니다

Codex가 쓴 토큰은 스킬을 쓴 실행이 중앙값 8,545개, 대조군이 7,599개였습니다
SKILL.md와 참조 파일을 읽는 데 토큰 약 950개가 추가로 사용됐습니다

## 직접 써 볼 때

![하나의 스킬 폴더가 두 작업대로 이어지는 개념 컷](/assets/images/ai/skill-in-use-04-claude-code-vs-codex/07-agy.webp)
*하나의 스킬 폴더가 두 작업대로 이어지는 개념 컷 — 출처: 개념 컷, agy 자가 생성*

### 🧩 폴더 맞추기

원본은 저장소의 **.agents/skills/이름/** 폴더에 둡니다
Claude Code용으로 .claude/skills 아래에 같은 이름의 심볼릭 링크를 생성합니다

개인용 스킬은 홈 폴더의 같은 이름 폴더에 둡니다
Codex는 ~/.agents/skills, Claude Code는 ~/.claude/skills예요

name 값과 폴더 이름이 다르면 표준 위반이라 <u>두 이름을 정확히 일치시킵니다</u>

### ✍️ description 쓰기

두 도구 모두 처음엔 description의 내용을 기준으로 사용할 스킬을 선택합니다
사용자가 실제로 입력할 표현을 description에 포함하면 자동 호출 가능성이 높아집니다

이번 스킬은 description에 **릴리스 노트, 변경 사항 정리, 배포 노트**를 한글로 적었습니다
한국어 요청 5번 모두에서 스킬이 자동으로 호출됐습니다

### ⚙️ 도구별 차이

| 항목 | Claude Code | Codex |
| :--- | :--- | :--- |
| 명시 호출 | /release-note-ko | **$release-note-ko** |
| 이번 실측 모델 | Sonnet 5.5 | GPT-6.1 Sol |
| 웹 ChatGPT | 해당 없음 | 플러그인에 넣어야 함 |

Codex는 스킬 폴더 안 agents/openai.yaml 설정으로 자동 호출을 비활성화할 수 있습니다
**allow_implicit_invocation: false**를 적으면 돼요

ChatGPT 웹에서는 단독 스킬을 직접 사용할 수 없습니다
플러그인에 포함된 스킬만 사용할 수 있습니다

🔗 링크 첨부 - https://blog.naver.com/rottensweetpotato/224406152414

![Agent Skills 두 도구 실측 정리 카드](/assets/images/ai/skill-in-use-04-claude-code-vs-codex/08-items.webp)
*Agent Skills 두 도구 실측 정리 카드 — 출처: 직접 실측 기반 자가 렌더*

## 참고 출처

- [[Anthropic] Donating Agent Skills to the Agentic AI Foundation (2026-10-22, 기증 범위, 지원 플랫폼 수)](https://www.anthropic.com/news/donating-agent-skills-to-the-agentic-ai-foundation)
- [[Agent Skills] Specification (SKILL.md 필수 값, 단계별 로딩)](https://agentskills.io/specification)
- [[OpenAI] Build skills (Codex 스킬 폴더, $ 호출, agents/openai.yaml)](https://learn.chatgpt.com/docs/build-skills)
- [[Claude Code Docs] Skills (Claude Code 스킬 폴더)](https://code.claude.com/docs/en/skills)
- 실측 환경: macOS, Claude Code 2.1.310(Sonnet 5.5), Codex CLI 0.164.0(GPT-6.1 Sol, 추론 high), 2026-10-25
