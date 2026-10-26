---
title: "Claude Code PHP 보안 스킬 — 그누보드형 예제 앱 결함 11곳 탐지"
description: "PHP 웹사이트 보안 점검을 맡기는 Claude Code 스킬 php-security-hardening 의 구성과, 결함을 심은 예제 앱에서 탐지한 것과 놓친 것을 정리합니다"
date: 2026-10-25
category: AI
subcategory: Explainer
tags: [claude-code, agent-skills, php, secure-coding, web-security]
image: /assets/og/2026-10-25-claude-code-php-security-skill.png
---

PHP 웹사이트의 보안 점검을 Claude Code에 맡기는 스킬을 만들어 공개했어요

이름은 **php-security-hardening**이에요
GitHub oh-my-skills 저장소의 security 플러그인에 포함돼 있어요

스킬이 실제로 무엇을 탐지하고 무엇을 놓치는지 결함을 일부러 심은 예제 앱으로 확인해 봤어요
결과는 심은 결함 <mark>11곳 전부</mark> 탐지, 놓친 비교 패턴 1개, 아직 반영 못 한 권고 1건이에요

![PHP 공식 로고](/assets/images/ai/claude-code-php-security-skill/01-hero-php.webp)
*PHP 공식 로고 — 출처: PHP Group / Colin Viebrock (CC BY-SA 4.0)*

## 스킬 구성

![Claude Code에서 플러그인을 설치하는 명령](/assets/images/ai/claude-code-php-security-skill/02-term.webp)
*Claude Code에서 플러그인을 설치하는 명령 — 출처: oh-my-skills README 기반 자가 렌더*

스킬은 Claude Code의 **플러그인 마켓플레이스** 방식으로 배포해요
마켓플레이스를 등록하고 security 플러그인을 설치하면 돼요

실행할 때는 **/security:php-security-hardening**을 입력해요

본문 SKILL.md에는 순서와 규칙만 두고 긴 표는 references 폴더의 별도 파일로 분리했어요
Claude는 단계에 필요한 파일만 그때 읽어요

| 파일 | 쓰는 때 |
| :--- | :--- |
| advisories/php2shell.md | **긴급 권고 대응** |
| grep-patterns.md | 코드 점검 |
| platforms-by-region.md | 플랫폼별 보강 |
| incident-response.md | 침해 의심 |

### 🧭 세 가지 모드

| 모드 | 언제 |
| :--- | :--- |
| A. 긴급 대응 | PHP2Shell 같은 런타임 취약점 |
| B. 전체 점검 | 코드 리뷰, 출시 전 점검 |
| C. 침해 대응 | 웹셸, 수상한 프로세스 |

긴급 보안 권고가 적용되는 동안에는 어느 모드든 <mark>런타임 버전 확인부터</mark> 해요
패치되지 않은 런타임을 코드 결함보다 먼저 점검한다는 규칙이에요

### 🛡️ 지키는 원칙

스킬은 **방어 전용**이에요
공격 코드나 페이로드는 쓰지 않고, 남의 사이트를 스캔해 달라는 요청은 거절해요

버전 정보는 매주 바뀌어서 실행할 때마다 php.net과 공식 권고를 다시 확인해요
임시 완화 조치는 <u>취약점 해결이 아니라 공격 노출 범위 감소</u>로 표기하도록 정했어요

## 구조 검증

![claude plugin validate로 마켓플레이스와 플러그인을 검사한 화면](/assets/images/ai/claude-code-php-security-skill/03-term.webp)
*claude plugin validate로 마켓플레이스와 플러그인을 검사한 화면 — 출처: 직접 실행 화면 자가 렌더*

공개 전에 Claude Code의 검사 명령으로 매니페스트를 확인했어요
마켓플레이스와 security 플러그인 모두 <mark>구조 검증을 통과</mark>했어요

검사 시점의 플러그인 버전은 **0.1.2**예요
마지막 수정은 10월 24일, PHP2Shell 확인 절차와 탐지 누락을 고친 커밋이에요

## 예제 앱 실측

![예제 코드 사이에서 위험한 함수를 찾아내는 점검 개념 컷](/assets/images/ai/claude-code-php-security-skill/04-agy.webp)
*예제 코드 사이에서 위험한 함수를 찾아내는 점검 개념 컷 — 출처: 개념 컷, agy 자가 생성*

실측용 예제 앱은 **그누보드** 폴더 구조를 흉내 내 직접 만들었어요
bbs, adm, data 폴더와 common.php로 이뤄져 있어요

파일 5개에 흔한 결함 <mark>11개</mark>와 세션 형식 전환 코드 1개를 의도적으로 삽입했어요

스킬의 판별표는 common.php와 bbs, adm, data 조합을 그누보드 5, 영카트로 분류해요
그다음 references/grep-patterns.md의 검색식을 그대로 실행했어요

### 🔎 검색 결과

![스킬의 검색식으로 예제 앱을 검색한 실제 출력](/assets/images/ai/claude-code-php-security-skill/05-term.webp)
*스킬의 검색식으로 예제 앱을 검색한 실제 출력 — 출처: 직접 실행 화면 자가 렌더*

| 위치 | 분류 | 결과 |
| :--- | :--- | :--- |
| view.php:4 | SQL 인젝션 | **탐지** |
| view.php:5 | XSS | 탐지 |
| download.php:3 | 경로 조작 | 탐지 |
| download.php:4 | 파일 포함 | 탐지 |
| upload.php:2 | 파일 업로드 | 탐지 |
| upload.php:3 | 약한 난수 | 탐지 |

| 위치 | 분류 | 결과 |
| :--- | :--- | :--- |
| tool.php:2 | 명령 실행 | **탐지** |
| tool.php:3 | 역직렬화 | 탐지 |
| tool.php:4 | phpinfo 노출 | 탐지 |
| common.php:2 | 오류 화면 노출 | 탐지 |
| view.php:6 | 약한 해시 | 탐지 |

검색식 11개가 결함 11곳을 각각 탐지했어요
오탐은 이 예제에선 <mark>0건</mark>이었지만 결함만 모아 둔 코드라 실제 앱에선 더 나올 거예요

스킬도 검색 결과를 **후보**로만 다루고 주변 코드를 검토해 실제 결함 여부를 판정하라고 적어 뒀어요

### ❌ 놓친 것

view.php:6은 md5 해시를 == 로 비교하는 줄이에요
md5 검색식으로 약한 해시는 탐지했지만 <mark>느슨한 비교 검색식</mark>은 이 줄을 탐지하지 못했어요

느슨한 비교 검색식은 == 뒤에 hash, token, pass 같은 변수 이름이 바로 나와야 검색식과 일치해요
이 줄은 == 뒤에 배열 이름 row가 먼저 나와서 검색식에 일치하지 않아요

### 🕒 아직 없는 권고

긴급 권고 표에는 10월 24일 기준 **PHP2Shell** 하나만 있어요
10월 23일 공개된 세션 취약점 CVE-2026-115560은 아직 표와 검색식에 <mark>없어요</mark>

예제 common.php에 심어 둔 세션 형식 전환 줄은 별도로 추가한 검색식으로 탐지했어요

PHP2Shell 임시 조치에 같은 완화 설정이 들어 있어 운영 조치는 겹쳐요
다만 표와 검색식에는 이 CVE를 별도로 추가하도록 표와 검색식을 갱신해야 해요

## 런타임 확인

![php-fpm -v로 웹 쪽 PHP 버전을 확인한 화면](/assets/images/ai/claude-code-php-security-skill/06-term.webp)
*php-fpm -v로 웹 쪽 PHP 버전을 확인한 화면 — 출처: 직접 실행 화면 자가 렌더*

스킬은 명령줄 php가 아니라 웹 요청을 처리하는 **SAPI별 버전**을 보라고 해요
배포판은 버전 번호를 유지하고 보안 패치만 적용하기도 해서 변경 이력까지 확인해요

실측 환경의 PHP-FPM 버전은 <mark>8.4.11</mark>이었어요
PHP2Shell 해결 버전 8.4.27보다 낮아 스킬 기준 최우선(P0) 대상이에요

로컬 개발용이라 외부 요청은 받지 않지만 같은 버전을 서버에 배포했다면 바로 업데이트해야 해요
PHP2Shell의 경과와 해결 버전은 앞선 글에 정리했어요

🔗 링크 첨부 - https://blog.naver.com/rottensweetpotato/224450769485

## 국내 환경 반영

![Claude 공식 아이콘](/assets/images/ai/claude-code-php-security-skill/07-logo-claude.webp)
*Claude 공식 아이콘*

| 대상 | 스킬 점검 항목 |
| :--- | :--- |
| 그누보드, 영카트 | **data/ 실행 차단**, adm/ 접근 제한 |
| 영카트 결제 | 주문 금액과 PG 승인 금액 대조 |
| 라이믹스, XE | XE 1.x 이전 |
| PG SDK | 키 하드코딩, 웹훅 서명 |
| 호스팅 | 카페24, 가비아, 닷홈 PHP 버전 |

취약점 정보는 **KISA 보호나라**를 국내 정보원으로 쓰고 개인정보보호법의 안전조치 기준과 연결해요
일본, 중국, 독일 등 다른 나라의 플랫폼 정보도 같은 형식의 표에 들어 있어요

## 쓸 때 주의할 점

검색식은 첫 단계 필터예요
결함으로 확정하려면 사용자 입력이 실제로 그 함수까지 전달되는지 코드를 읽어야 해요

vendor 폴더의 외부 라이브러리는 직접 고치지 말고 <u>composer audit</u>으로 버전을 올려요
서버 설정을 바꾸기 전엔 백업하고 diff부터 보여 주도록 정했어요

검색 결과가 0건이어도 <mark>안전하다는 뜻은 아니에요</mark>
침해 대응 모드에서도 검색 결과에서 결함이 탐지되지 않았다면 발견하지 못했다고만 적어요

![PHP 보안 스킬 실측 정리 카드](/assets/images/ai/claude-code-php-security-skill/08-items.webp)
*PHP 보안 스킬 실측 정리 카드 — 출처: 직접 실측 기반 자가 렌더*

🔗 oh-my-skills 저장소 - https://github.com/No1Joon/oh-my-skills

## 참고 출처

- [[GitHub] No1Joon/oh-my-skills (php-security-hardening 스킬, 2026-10-24 커밋 기준)](https://github.com/No1Joon/oh-my-skills)
- [[PHP] Security advisory: PHP2Shell (2026-10-21, 해결 버전)](https://www.php.net/archive/2026.php)
- [[PHP] Informational advisory: Session upload progress (2026-10-23, CVE-2026-115560)](https://www.php.net/archive/2026.php)
- [[Claude Code Docs] 플러그인과 마켓플레이스](https://code.claude.com/docs/en/plugins)
- 실측 환경: macOS, PHP 8.4.11 CLI와 FPM, Claude Code 2.1.310, 2026-10-25
