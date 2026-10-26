---
title: "DeepSeek 추론 엔진 DeepInfer 공개 — 하루 155조 토큰 처리"
description: "DeepSeek 가 자사 서비스에 쓰는 추론 엔진 DeepInfer 를 Apache 2.0 으로 공개한 범위와 이번 릴리스에서 빠진 운영 구성요소를 정리합니다"
date: 2026-10-21
category: AI
subcategory: News
tags: [deepseek, deepinfer, inference-engine, open-source, moe]
image: /assets/og/2026-10-21-deepseek-deepinfer-inference-engine.png
---

DeepSeek가 자사 서비스를 운영하는 추론 엔진 **DeepInfer**를 공개했어요
2025년에는 엔진 전체를 공개하지 않겠다고 했던 바로 그 코드입니다!

라이선스는 **Apache 2.0**이고 저장소 첫 커밋은 2026년 10월 20일이에요
공개 하루 만에 GitHub 별 <mark>9,500개</mark>를 넘겼습니다

![DeepSeek 로고](/assets/images/ai/deepseek-deepinfer-inference-engine/01-deepseek-logo-color.webp)
*DeepSeek 로고*

## 공개된 범위

![DeepSeek V4.1 Flash 추론 시스템 구조도](/assets/images/ai/deepseek-deepinfer-inference-engine/02-photo.webp)
*DeepSeek V4.1 Flash 추론 시스템 구조도 — 출처: DeepSeek*

DeepInfer는 **DeepSeek-V4.1-Flash**를 대량으로 서비스하는 추론 프레임워크예요
추론(inference)은 학습이 끝난 모델로 답을 만들어 내는 단계입니다

이번 공개분은 오프라인 추론까지예요
실제 서비스 운영에 필요한 구성요소 세 개는 <u>이번 릴리스에서 제외됐다</u>고 README에 적었습니다

| 구분 | 내용 |
| :--- | :--- |
| 포함 | 최적화 커널, 전문가 병렬 |
| 포함 | DSpark 추측 디코딩 |
| 포함 | 구조화 출력(JSON 스키마) |
| 포함 | 결정적 샘플링 (NVIDIA만) |
| 빠짐 | **KV 캐시 시스템** |
| 빠짐 | prefill, decode 분리 배치 |
| 빠짐 | 복제본 간 부하 분산 |

DeepSeek는 KV 캐시와 부하 분산이 <mark>내부 인프라에 강하게 의존해</mark> 아직 모두 공개하지 못했다고 밝혔어요
대신 두 구성요소의 설계는 배포 Q&A 문서와 Zhihu 글에서 설명했습니다

같이 공개한 **deepseek-recipe**는 API 요청을 토큰으로 변환하는 모듈이에요
세 API 형식(Chat Completions, Responses, Messages)을 처리해요

## 2025년 발표와 달라진 점

DeepSeek는 2025년 오픈소스 주간 뒤 엔진 공개를 미루는 글을 냈어요
이유는 셋이었습니다

[1년 넘은 vLLM 포크]
DeepSeek 모델에 맞춰 많이 수정해 범용 용도로 확장하기 어려움

[내부 인프라 결합]
클러스터 관리 도구에 의존해 외부 배포에 대규모 수정 필요

[유지 인력 부족]
작은 연구팀이라 큰 오픈소스 프로젝트를 유지할 여력 부족

그때 대안은 활용 가능한 구성요소만 분리해 공개하는 것이었어요
**FlashMLA**, **DeepGEMM**, **DeepEP** 같은 커널 라이브러리가 그렇게 나왔습니다

이번엔 이 구성요소들을 통합한 엔진 본체가 공개됐어요
README는 DeepInfer가 <mark>vLLM을 바탕으로</mark> 만들어졌다고 적었습니다

SGLang, TensorRT-LLM에서도 아이디어를 얻었다고 밝혔어요

다만 두 번째 이유였던 <u>내부 인프라 의존성</u>은 아직 해결되지 않았어요

## 공개 문서 속 운영 수치

![DeepSeek V4.1 Flash 추론 서비스 운영 수치 카드](/assets/images/ai/deepseek-deepinfer-inference-engine/03-chart.webp)
*DeepSeek V4.1 Flash 추론 서비스 운영 수치 카드 — 출처: DeepSeek 배포 Q&A 기반 자가 렌더*

배포 Q&A에 따르면 클러스터 하나가 하루 <mark>155조 토큰</mark>을 처리해요

GPU 1시간당 매출은 할인 시간대 요금 기준 약 **5만 3,200원(38달러)**이에요
KV 캐시를 담는 SSD는 약 100PiB이고 보존 기간은 에이전트 3일, 챗봇 7일입니다

**KV 캐시**는 앞서 계산한 문맥 정보를 저장해 둔 데이터예요
같은 앞부분으로 다시 물으면 중복 계산을 생략해 비용과 처리 시간이 감소합니다

### 📈 디코드 처리량

![디코드 GPU당 처리량 대 사용자당 속도 그래프](/assets/images/ai/deepseek-deepinfer-inference-engine/04-photo.webp)
*디코드 GPU당 처리량 대 사용자당 속도 그래프 — 출처: DeepSeek*

GPU 64장 구성에서 1장당 요청 256건을 동시에 처리하면 초당 약 **2만 6,000토큰**을 생성했어요
대신 사용자 한 명이 받는 속도는 초당 100토큰 남짓으로 떨어집니다

요청을 8건으로 줄이면 사용자당 속도는 초당 <mark>320토큰</mark>을 넘어요
그만큼 GPU 1장의 총 처리량은 초당 약 2,600토큰으로 줄어듭니다

### ⚡ DSpark 가변 길이 검증

![가변 길이 검증의 처리량 변화 막대 차트](/assets/images/ai/deepseek-deepinfer-inference-engine/05-chart-dspark.webp)
*가변 길이 검증의 처리량 변화 막대 차트 — 출처: DeepSeek 배포 Q&A 기반 자가 렌더*

**DSpark**는 작은 초안 토큰을 먼저 만들고 본 모델이 맞는지 검증하는 방식이에요
DeepInfer는 초안마다 맞을 확률을 예측해 검증할 토큰 수를 바꿉니다

고정 5개 검증보다 검증 토큰이 약 30% 줄었어요
실제 운영 구간인 동시 60건 부근에서 처리량이 <mark>4~7%</mark> 늘었습니다

동시 16건에서는 오히려 1.5% 줄었어요

## 국내에서 돌릴 수 있는 곳

지원 하드웨어는 **NVIDIA SM100 GPU**와 Huawei **Ascend 950** NPU 두 가지예요
SM100은 B200 계열 Blackwell 데이터센터 GPU를 가리킵니다

H100, H200 같은 이전 세대는 <u>지원 목록에 없어요</u>
CUDA 13과 Python 3.12, GCC 13 이상도 필요합니다

DeepSeek가 제시한 효율적 운영의 최소 규모는 GPU <mark>128장</mark>이에요
prefill 64장과 decode 64장을 합한 숫자입니다

국내에서는 2025년 2월 국방부, 외교부, 산업통상자원부 등이 DeepSeek 접속을 차단했어요
그 조치는 DeepSeek가 운영하는 앱과 웹 서비스를 겨냥한 것이었습니다

DeepInfer로 가중치를 자체 서버에서 실행하면 입력이 DeepSeek 서버로 가지 않아요
다만 자체 운영도 각 기관의 보안 심사 기준을 따로 거쳐야 합니다

## 앞으로 주목할 점

- DeepSeek는 <u>다음 모델의 추론 코드</u>도 DeepInfer에 계속 올리겠다고 밝혔어요
- 배포 Q&A는 질문을 받아 계속 갱신하는 문서예요
- **KV 캐시와 부하 분산** 코드가 공개되면 그때 완전한 서비스 구성이 됩니다
- vLLM과 SGLang에 V4.1 Flash 최적화가 얼마나 반영되는지도 확인할 항목이에요

지난 V4.1-Flash-1017 공개 소식은 아래 글에 정리했어요~

🔗 링크 첨부 - https://blog.naver.com/rottensweetpotato/224446055227

## 참고 출처

- [[GitHub] deepseek-ai/DeepInfer README (지원 범위, 하드웨어, 라이선스)](https://github.com/deepseek-ai/DeepInfer)
- [[GitHub] DeepSeek V4.1 Flash Inference Deployment Q&A (운영 수치, DSpark 표)](https://github.com/deepseek-ai/DeepInfer/blob/main/doc/inference_deployment_qa.md)
- [[GitHub] open-infra-index, OpenSourcing DeepSeek Inference Engine (2025년 공개 보류 사유)](https://github.com/deepseek-ai/open-infra-index/tree/main/OpenSourcing_DeepSeek_Inference_Engine)
- [[다음뉴스] 국방, 외교, 산업부 DeepSeek 접속 차단 (2025-02-05)](https://v.daum.net/v/20250205211948335)
- 환율: 1달러 ≈ 1,400원 기준 환산
