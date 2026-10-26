---
title: "WhatsApp 도움말 소스 속 AI 지시문 — 규제기관 안내 금지"
description: "WhatsApp 도움말 문서 페이지 소스에서 발견된 상담 챗봇용 숨은 지시문 102개의 발견 경위와 문제가 된 지시문 두 개를 정리합니다"
date: 2026-10-21
category: AI
subcategory: News
tags: [whatsapp, meta, chatbot, system-prompt, privacy]
image: /assets/og/2026-10-21-whatsapp-hidden-ai-instructions.png
---

WhatsApp 도움말 문서 80쪽에 화면에는 안 보이는 AI용 지시문이 페이지 소스에 포함돼 있었어요
그중 하나는 이용자에게 <mark>규제기관을 안내하지 말라</mark>는 내용이었습니다!!

지시문은 WhatsApp 자체 **상담 챗봇**이 읽도록 넣은 것이었어요
WhatsApp은 버그로 노출됐다고 해명했고, 10월 18일 해당 지시문을 모두 삭제했습니다

![WhatsApp 로고](/assets/images/ai/whatsapp-hidden-ai-instructions/01-whatsapp-wordmark-color.webp)
*WhatsApp 로고*

## 발견 경위

![WhatsApp 도움말 숨은 AI 지시문 조사 규모 카드](/assets/images/ai/whatsapp-hidden-ai-instructions/02-chart.webp)
*WhatsApp 도움말 숨은 AI 지시문 조사 규모 카드 — 출처: Redact 기반 자가 렌더*

개인정보 삭제 도구를 만드는 **Redact**가 10월 8일 처음 발견했어요
도움말 문서 545쪽을 저장해 읽었더니 80쪽에 숨은 블록 <mark>102개</mark>가 있었습니다

이 텍스트는 페이지 소스 안 **HelpContentGalaxyLLMInclude** 표시 근처에 있었어요
일반 화면에는 표시되지 않고 페이지 소스에만 포함돼 있었습니다

대부분은 혼동하기 쉬운 용어 설명이나 다른 문서로 안내하는 정리용 메모였어요
예를 들어 통화 문제에 앱 재설치를 권하지 말라는 식입니다

Facebook과 Instagram 도움말도 같은 시스템을 써요
Redact가 두 곳 300쪽을 따로 봤지만 비슷한 메모는 <u>찾지 못했다</u>고 밝혔습니다

## 문제가 된 지시문 두 개

| 문서 | 숨은 지시 |
| :--- | :--- |
| 계정 삭제 | **규제기관 연락 권유 금지** |
| 계정 삭제 | 수동 삭제 가능 언급 금지 |
| 신고와 차단 | GDPR 등 법 인용 금지 |
| 적용 조건 | 소송, 변호사 언급 시 |

계정 삭제 문서는 휴대폰이나 번호를 잃어 계정을 못 지우는 사람을 다뤘어요
이 문서에 삽입된 지시는 **데이터 보호 기관**, 규제기관, 감독기관에 연락하도록 권하지 말라는 것이었어요

신고와 차단 문서의 지시문은 이용자가 소송, 변호사, 법원을 언급하면 작동했어요
그때 GDPR, LGPD, CCPA 같은 법을 <u>인용하지도 해석하지도 말라</u>고 했어요

이용자가 먼저 법을 꺼내도 마찬가지였습니다

### ⚖️ 회사 처리방침과 어긋나는 지점

7월 2일 시행된 WhatsApp 유럽 개인정보 처리방침은 민원 창구를 적어 두었어요
아일랜드 **데이터 보호 위원회(DPC)**입니다

같은 회사의 챗봇 지시는 이용자에게 그 창구를 <mark>권하지 말라</mark>고 했습니다

## 도움말 지시문 게시 기간

![숨은 지시문의 등장과 삭제 타임라인](/assets/images/ai/whatsapp-hidden-ai-instructions/03-chart.webp)
*숨은 지시문의 등장과 삭제 타임라인 — 출처: Redact, Internet Archive 기반 자가 렌더*

인터넷 아카이브에 남은 계정 삭제 문서 사본을 보면 7월 12일 사본에는 지시문이 없어요
9월 4일 사본에는 <mark>지시문이 있었습니다</mark>

Redact는 10월 15일 21시 40분(UTC)까지도 두 지시문이 남아 있는 것을 확인했어요
10월 18일 2시 8분(UTC)에는 80쪽의 블록 102개가 **모두 삭제됐습니다**

WhatsApp은 WIRED에 이 메모가 상담 챗봇용 지시였다고 설명했어요
"사용자에게 직접 하는 말이 아니라 챗봇에 주는 지시"이고, 버그로 노출돼 고쳤다는 입장입니다

대변인은 챗봇이 WhatsApp 사용법 안내에 집중하고 <u>법률 자문은 하지 않게</u> 하려는 것이라고 밝혔어요

## 도움말 지시문을 처리하는 시스템

![사람에게는 안 보이고 AI만 읽는 문서 층 개념 컷](/assets/images/ai/whatsapp-hidden-ai-instructions/04-agy.webp)
*사람에게는 안 보이고 AI만 읽는 문서 층 개념 컷 — 출처: 개념 컷, agy 자가 생성*

지시문을 읽는 쪽은 WhatsApp의 **자체 상담 챗봇**이에요
도움말 문서를 근거로 답하는 구조라 문서 속 메모도 지시로 처리될 수 있어요

WhatsApp 서버는 Google, Bing 검색 수집기에도 메모가 든 전체 페이지를 보냈어요

10월 9일 OpenAI, Anthropic, Perplexity 수집기 이름으로도 요청해 봤어요
그때는 본문과 메모가 <u>제외된 페이지</u>가 전달됐습니다

실제로 챗봇이 이 지시대로 답했는지는 <mark>확인되지 않았어요</mark>
Redact는 지시문만 읽었고 챗봇 답변은 시험하지 않았다고 밝혔습니다

## 국내 이용자가 알아 둘 것

![AI 상담을 쓸 때 확인할 것 카드](/assets/images/ai/whatsapp-hidden-ai-instructions/05-items.webp)
*AI 상담을 쓸 때 확인할 것 카드 — 출처: 개인정보 보호법, 개인정보보호위원회 안내 기반 자가 렌더*

국내에서 개인정보 보호를 담당하는 기관은 **개인정보보호위원회**예요
침해 신고와 상담은 KISA 개인정보침해신고센터가 국번 없이 118로 받습니다

소송 없이 다투려면 개인정보 분쟁조정위원회에 조정을 신청할 수 있어요
양쪽이 조정안을 받아들이면 <mark>재판상 화해와 같은 효력</mark>이 생깁니다

계정 삭제가 거부되면 회사 챗봇 답변에만 의존하지 말고 <u>법이 정한 삭제 요구</u>를 직접 하세요~

🔗 링크 첨부 - https://privacy.kisa.or.kr/

## 참고 출처

- [[Redact] WhatsApp's help pages hid LLM instructions (2026-10-19, 원 조사)](https://redact.dev/blog/whatsapp-help-pages-hidden-ai-instructions)
- [[WIRED] WhatsApp help pages leaked hidden instructions for a Meta chatbot (WhatsApp 해명)](https://www.wired.com/story/whatsapp-help-pages-leaked-hidden-instructions-for-a-meta-chatbot/)
- [[Internet Archive] WhatsApp 계정 삭제 도움말 2026-10-09 사본 (지시문 포함)](https://web.archive.org/web/20261009054848/https://faq.whatsapp.com/2138577903196467/?cms_platform=android)
- [[법무부] 개인정보 열람, 정정, 삭제, 처리정지 청구 안내](https://moj.go.kr/moj/3495/subview.do)
- [[로톡] 개인정보 침해를 당했을 때 할 수 있는 법적 대응 방법 (분쟁조정 효력)](https://www.lawtalk.co.kr/posts/164807)
