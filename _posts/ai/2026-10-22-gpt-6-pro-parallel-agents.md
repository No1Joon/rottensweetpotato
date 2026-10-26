---
title: "GPT-6 Pro 병렬 에이전트 — Plus 는 이용 대상 제외"
description: "한 작업을 여러 에이전트로 나눠 동시에 처리하는 ChatGPT GPT-6 Pro 업데이트의 내용과 요금제별 이용 대상을 정리합니다"
date: 2026-10-22
category: AI
subcategory: News
tags: [openai, chatgpt, gpt-6, parallel-agents, multi-agent]
image: /assets/og/2026-10-22-gpt-6-pro-parallel-agents.png
---

ChatGPT의 GPT-6 Pro가 한 작업을 여러 에이전트로 나눠 동시에 처리하게 됐어요
OpenAI가 2026년 10월 16일 릴리스 노트에 공개한 업데이트입니다

Pro 요금제 사용자부터 순차 배포되고, Plus에서는 쓸 수 없어요

![OpenAI 워드마크](/assets/images/ai/gpt-6-pro-parallel-agents/01-openai-wordmark-mono.webp)
*OpenAI 워드마크*

## 업데이트 내용

![ChatGPT 릴리스 노트의 GPT-6 Pro 업데이트 항목](/assets/images/ai/gpt-6-pro-parallel-agents/02-release-notes.webp)
*ChatGPT 릴리스 노트의 GPT-6 Pro 업데이트 항목 — 출처: OpenAI*

[더 빠른 응답]
응답 속도 개선, 수치는 미공개

[플러그인과 도구 활용]
작업을 수행할 때 플러그인과 도구를 더 잘 쓰도록 개선

[병렬 에이전트]
여러 에이전트가 한 작업의 서로 다른 부분을 동시에 처리

진행 상황은 대화 안에서 볼 수 있어요
완료된 작업을 열면 <mark>에이전트마다 무슨 일을 했는지 확인</mark>할 수 있습니다

배포는 <mark>이용 자격이 있는 Pro 사용자에게 순차적으로</mark> 진행돼요
관리형 워크스페이스는 관리자 설정과 배포 대상 여부에 따라 달라집니다

OpenAI의 X 공지는 같은 모델을 **GPT-6 Astra Pro**라고 적었어요
도움말 문서 기준으로 GPT-6 Pro는 GPT-6 Astra 기반이라 같은 모델을 가리킵니다

## 쓸 수 있는 요금제

| 요금제 | 월 요금 | Chat의 GPT-6 Pro |
| :--- | :--- | :--- |
| Pro 100 | 약 14만 원(100달러) | 포함 |
| Pro 200 | 약 28만 원(200달러) | 포함 |
| Pro 500 | 약 70만 원(500달러) | 문서에 미기재 |
| Plus | - | **미포함** |

대상은 **Pro 100, Pro 200, Business, Enterprise**예요
Plus는 Chat에서 고를 수 없고, Work와 Codex에서만 GPT-6 Astra를 씁니다

9월 29일 나온 **Pro 500**은 모델 문서의 GPT-6 Pro 목록에 아직 없어요
Pro 500이 다른 요금제와 구별되는 점은 Ultrafast 속도 모드예요

Pro 200은 9월 11일 신규 가입이 중단됐다가 9월 29일 재개됐어요

🔗 링크 첨부 - https://blog.naver.com/rottensweetpotato/224408268614

다시 열린 Pro 200은 새로 가입하면 <u>이전보다 적은 기본 사용량</u>이 제공돼요
9월 22일부터 29일 사이 Pro 200을 쓰던 사람은 <mark>10월 29일까지</mark> 기존 사용량을 유지합니다

Pro는 월 결제만 되고 연간 결제는 없어요
이번 업데이트 공지에는 국가 제한이 적혀 있지 않습니다

## 사용 한도와 차감 방식

![스탠다드 모드 대비 기본 사용량 차감 배율](/assets/images/ai/gpt-6-pro-parallel-agents/03-chart.webp)
*스탠다드 모드 대비 기본 사용량 차감 배율 — 출처: OpenAI 도움말 기반 자가 렌더*

GPT-6 Pro는 무제한이 아니라 **주간 사용 한도**가 있어요
Pro 200에서 주간 한도를 소진하면 GPT-5.6 사고의 중간 수준으로 자동 전환됩니다

Pro 100은 GPT-6 Pro와 GPT-5.6 Sol Pro가 <mark>하나의 주간 사용량을 공유</mark>해요

속도 모드에 따라 차감량도 달라져요
스탠다드 대비 **패스트 모드는 2.5배**, Ultrafast는 **8배**를 차감합니다

Ultrafast는 Work와 Codex의 GPT-6 Astra, GPT-6.1 Sol에 쓰는 속도 모드예요
OpenAI는 이 배율이 그만큼 빠른 성능을 보장하지는 않는다고 적었습니다

병렬 에이전트가 사용량을 어떻게 차감하는지는 공개되지 않았어요!!
에이전트를 최대 몇 개까지 동시에 실행하는지도 OpenAI 문서에 수치가 없습니다

## 다른 에이전트 기능과의 차이

![한 작업을 여러 갈래로 나눠 처리하는 개념 컷](/assets/images/ai/gpt-6-pro-parallel-agents/04-agy.webp)
*한 작업을 여러 갈래로 나눠 처리하는 개념 컷 — 출처: 개념 컷, agy 자가 생성*

이번 병렬 에이전트는 Chat 탭에서 한 답변을 생성하는 동안 실행돼요

9월 29일 나온 **dots**는 대화 사이에도 일을 이어 가는 상시 에이전트예요
GPT-6 Astra 모델을 사용하고 자기 클라우드 컴퓨터를 가집니다

**Codex Cloud**는 코딩 작업마다 격리된 작업 공간을 따로 둬요
노트북을 덮어도 클라우드에서 작업이 계속됩니다

Pro 모델로 생성한 답변에서는 10월 7일 나온 <mark>인텔리전트 UI가 지원되지 않아요</mark>
차트와 버튼이 포함된 답변은 즉시 응답부터 Extra High 수준까지만 지원됩니다

🔗 링크 첨부 - https://blog.naver.com/rottensweetpotato/224438971557

## 확인할 것

![GPT-6 Pro 병렬 에이전트 확인할 것 정리 카드](/assets/images/ai/gpt-6-pro-parallel-agents/05-items.webp)
*GPT-6 Pro 병렬 에이전트 확인할 것 정리 카드 — 출처: OpenAI 도움말 기반 자가 렌더*

## 참고 출처

- [[OpenAI] ChatGPT 릴리스 노트, 2026년 10월 16일 GPT-6 Pro 업데이트](https://help.openai.com/en/articles/6825453-chatgpt-release-notes)
- [[OpenAI] ChatGPT의 GPT-6 및 기타 모델 (요금제별 제공, 사용 한도)](https://help.openai.com/ko-kr/articles/20001354-gpt-6-and-other-models-in-chatgpt)
- [[OpenAI] ChatGPT Pro 등급 정보 (Pro 100, 200, 500 요금과 차감 배율)](https://help.openai.com/ko-kr/articles/9793128-about-chatgpt-pro-tiers)
- [[OpenAI] X 공지 (GPT-6 Astra Pro 표기)](https://x.com/OpenAI/status/2111192259073094035)
- 환율: 1달러 ≈ 1,400원 기준 환산
