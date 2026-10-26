---
title: "Claude Duet 공개 — 먼저 연락하는 비서 앱, 미국 Pro·Max 만 이용"
description: "연결된 앱을 몇 시간마다 확인하고 먼저 연락하는 Anthropic 의 별도 비서 앱 Claude Duet 의 기능과 이용 조건을 정리합니다"
date: 2026-10-25
category: AI
subcategory: News
tags: [anthropic, claude, claude-duet, ai-agent, proactive-agent]
image: /assets/og/2026-10-25-claude-duet-proactive-assistant.png
---

Anthropic이 사용자에게 먼저 연락하는 비서 앱 **Claude Duet**을 10월 21일 공개했어요
연결된 앱의 정보를 몇 시간마다 확인하고 필요한 일이 있으면 사용자에게 연락해요

다만 연구 미리보기라 <mark>미국</mark> Pro, Max 가입자만 대기 명단 등록 후 이용할 수 있어요

![Claude Duet 발표 페이지의 Claude 연결 도구 아이콘 모음](/assets/images/ai/claude-duet-proactive-assistant/01-hero-duet.webp)
*Claude Duet 발표 페이지의 Claude 연결 도구 아이콘 모음 — 출처: Anthropic*

## 발표 내용

![Anthropic 공식 로고](/assets/images/ai/claude-duet-proactive-assistant/02-logo-anthropic.webp)
*Anthropic 공식 로고*

Claude Duet은 Claude 채팅 앱과 따로 설치하는 **별도 앱**이에요
iPhone, Android 앱과 claude.ai에서 이용할 수 있어요

모델은 **Claude Opus 5.5** 하나로 고정돼 있어요
작업별 추론 노력 수준은 Duet이 자동으로 설정해요

Anthropic은 주요 이용 대상을 전문직 종사자와 <mark>소상공인</mark>으로 설정했어요
회의 일정 잡기, 대시보드 만들기, 매출 예측, 웹 앱 시제품 같은 일을 예로 들었어요

- 매일 아침 연결 앱에서 중요한 일을 골라 브리핑
- 몇 시간마다 계정을 확인하고 필요할 때만 메시지
- 텍스트나 음성으로 맡긴 일을 백그라운드에서 처리
- 자체 가상 머신과 브라우저로 작업, 휴대폰이 꺼져 있어도 진행

## 작동 방식과 제한

![아침마다 정리된 업무 카드가 휴대폰 위로 떠오르는 개념 컷](/assets/images/ai/claude-duet-proactive-assistant/03-agy.webp)
*아침마다 정리된 업무 카드가 휴대폰 위로 떠오르는 개념 컷 — 출처: 개념 컷, agy 자가 생성*

Duet은 자료 조회, 초안 작성, 작업 준비까지 자동으로 수행해요
외부에 영향을 주는 행동을 하기 전에는 <u>정확한 내용을 보여 주고 승인을 받아요</u>

| 구분 | 해당 행동 |
| :--- | :--- |
| 혼자 진행 | 읽기, 초안, 준비 |
| 승인 후 진행 | **발송, 결제, 서명, 삭제** |
| 승인해도 금지 | <mark>증권 거래, 계좌 이체</mark> |

다른 사람에게 전화나 문자를 보내는 기능도 없어요
연결된 메일 계정으로 보내는 이메일만 승인을 받아 처리해요

### 🔐 민감 정보

새 분류기가 메시지마다 민감 정보를 검사해요
카드 번호와 신분증 번호 같은 최고 등급 정보는 <mark>차단</mark>해요

건강, 개인 금융 정보는 사용자가 명시적으로 지시할 때만 보내요
비밀번호는 기기의 **별도 입력 창**에서 받아 대화 기록에 저장되지 않도록 설계했어요

### 💳 결제

구매는 Stripe의 지갑 **Link**나 Shopify의 **Shop Pay**로만 해요
구매마다 일회용 가상 카드를 써서 실제 카드 번호가 판매자에게 전달되지 않아요

### 🔌 연결 앱

| 종류 | 서비스 |
| :--- | :--- |
| 메일, 일정 | Gmail, Google Calendar |
| 문서, 협업 | Google Drive, Slack |
| 업무 | **QuickBooks, HubSpot** |
| 계약, 예약 | Docusign, Calendly |

Microsoft 365는 아직 연결되지 않아요
연결 도구가 없는 사이트에서는 Duet의 클라우드 브라우저로 작업을 수행해요

### ⚠️ 한계

계정을 일정 간격으로 확인하기 때문에 그 사이에 발생한 <mark>긴급한 변경 사항에 즉시 대응하지 못할 수 있어요</mark>
Anthropic도 무엇이 급한지 잘못 판단할 수 있다고 밝혔어요

Duet이 쓰는 브라우저 화면을 사용자가 보거나 넘겨받을 수도 없어요

## 요금과 사용량

![선제형 에이전트를 쓰는 가장 낮은 월 요금 막대 차트](/assets/images/ai/claude-duet-proactive-assistant/04-chart.webp)
*선제형 에이전트를 쓰는 가장 낮은 월 요금 막대 차트 — 출처: Anthropic, OpenAI 요금표 기반 자가 렌더*

연구 미리보기 동안 Duet은 Pro, Max 요금제에 **추가 요금 없이** 포함돼요
Pro는 월 28,000원(20달러), Max는 월 14만 원(100달러)부터예요

대신 Claude 채팅과 같은 <u>5시간, 주간 사용 한도</u>를 함께 써요
아침 브리핑과 정기 확인 같은 백그라운드 작업도 사용 한도에서 차감돼요

Anthropic은 가입이 승인된 사용자에게 한도를 한 번 <mark>전부 초기화</mark>해 줘요
이 초기화는 2026년 11월 30일까지 쓸 수 있어요

## 국내 이용 조건

연구 미리보기 기간에는 <mark>미국 외 지역에서는 이용이 제한돼 있어요!!</mark>

Team, Enterprise 요금제도 아직 대상이 아니에요
Anthropic은 두 요금제에 나중에 제공할 계획이라고 밝혔어요

연결 앱 목록에는 **국내 서비스가 없어요**
카카오톡, 네이버 메일, 스마트스토어를 쓰는 국내 소상공인이 연결해 사용할 수 있는 서비스가 적어요

## 경쟁 구도

![OpenAI 공식 로고](/assets/images/ai/claude-duet-proactive-assistant/05-logo-openai.webp)
*OpenAI 공식 로고*

비슷한 서비스로 OpenAI가 10월 초 공개한 **dots**가 있어요
dots는 국내 ChatGPT Pro 요금제에서 이미 쓸 수 있어요

| 항목 | Claude Duet | dots |
| :--- | :--- | :--- |
| 국내 이용 | <mark>불가</mark> | **가능** |
| 최저 요금 | 월 28,000원 | 월 15만 9,000원 |
| 작업 환경 | 자체 VM, 브라우저 | 클라우드 컴퓨터 |

해외 매체는 Meta의 Muse와 Grok Bot도 같은 경쟁군으로 묶었어요

🔗 링크 첨부 - https://blog.naver.com/rottensweetpotato/224429637004

## 앞으로 주목할 점

![Claude Duet 핵심 정리 카드](/assets/images/ai/claude-duet-proactive-assistant/06-items.webp)
*Claude Duet 핵심 정리 카드 — 출처: Anthropic 발표 기반 자가 렌더*

- 미국 밖 지역과 Team, Enterprise 요금제로의 **확대 일정**
- 11월 30일 한도 초기화 기한 이후 사용량 정책
- Microsoft 365 같은 연결 앱 추가 여부
- 무엇이 급한지 판단하는 기준의 조정, Anthropic이 시험 중이라고 밝힌 부분

## 참고 출처

- [[Anthropic] Introducing Claude Duet (2026-10-21, 기능, 승인 규칙, 결제)](https://claude.com/blog/claude-duet)
- [[Claude 고객지원] Claude Duet 시작하기 (대상 국가, 요금제, 사용량, 연결 앱, 한계)](https://support.claude.com/en/articles/17631495)
- [[Anthropic] Claude 요금제 (Pro, Max 요금)](https://claude.com/pricing)
- [[MacRumors] Anthropic Launches Claude Duet (출시 보도)](https://macrumors.com/2026/10/21/anthropic-claude-duet/)
- [[iPhone in Canada] Claude Duet과 Muse, Grok Bot, dots 비교 (경쟁 구도)](https://iphoneincanada.ca/2026/10/21/claude-duet-proactive-ai-agent-app)
- 환율: 1달러 ≈ 1,400원 기준 환산
