---
title: "카드 없이 빅쿼리 (1) — BigQuery 샌드박스로 첫 쿼리와 처리량 확인"
description: "결제 카드 없이 Google 계정만으로 쓰는 BigQuery 샌드박스의 한도와, 공개 데이터셋에 첫 쿼리를 실행하며 처리량을 확인하는 방법을 정리합니다"
date: 2026-10-21
category: Tech
subcategory: Explainer
tags: [bigquery, bigquery-sandbox, google-cloud, sql, query-cost]
image: /assets/og/2026-10-21-bigquery-sandbox-01-first-query.png
---

결제 카드를 등록하지 않아도 BigQuery에서 SQL을 실행할 수 있어요

Google 계정만 있으면 되는 **BigQuery 샌드박스**로 첫 쿼리를 실행했습니다

![샌드박스 프로젝트에서 첫 쿼리를 실행한 BigQuery 콘솔 화면](/assets/images/tech/bigquery-sandbox-01-first-query/01-hero.webp)
*샌드박스 프로젝트에서 첫 쿼리를 실행한 BigQuery 콘솔 화면 — 출처: Google Cloud*

🔗 링크 첨부 - https://console.cloud.google.com/bigquery

## 샌드박스 한도

![새 데이터셋의 기본 만료 값이 60일로 찍힌 bq 화면](/assets/images/tech/bigquery-sandbox-01-first-query/02-term.webp)
*새 데이터셋의 기본 만료 값이 60일로 찍힌 bq 화면 — 출처: bq CLI 실행 결과 기반 자가 렌더*

샌드박스는 결제 계정을 연결하지 않은 프로젝트에서 자동으로 활성화됩니다

콘솔 맨 위에 샌드박스 표시와 업그레이드 버튼이 나타나요

실습 프로젝트 이름은 bq-sandbox-blog입니다

| 항목 | 한도 |
| :--- | :--- |
| 저장 | <mark>10GiB, 평생</mark> |
| 쿼리 처리 | 매월 1TiB |
| 테이블, 뷰, 파티션 | 60일 뒤 자동 만료 |

저장 한도에는 **평생(lifetime)** 이라는 단어가 붙어 있습니다

문서 원문은 *This quota is not refunded upon data deletion*이에요

<mark>데이터를 삭제해도 10GiB 한도는 회복되지 않습니다!!</mark>

새로 만든 데이터셋의 기본 만료 값은 **5,184,000,000밀리초**였습니다

일수로 환산하면 정확히 <u>60일</u>이에요

스트리밍 입력, DML, Data Transfer Service도 샌드박스에서는 쓸 수 없습니다

## 첫 쿼리와 처리량 예측

![쿼리 실행 뒤 처리한 바이트와 청구된 바이트가 표시된 작업 정보 탭](/assets/images/tech/bigquery-sandbox-01-first-query/03-photo.webp)
*쿼리 실행 뒤 처리한 바이트와 청구된 바이트가 표시된 작업 정보 탭 — 출처: Google Cloud*

첫 쿼리는 Google이 공개한 **usa_names** 데이터셋으로 실행했습니다

1910년 이후 미국 사회보장카드 신청자의 이름을 출생 연도별로 집계한 테이블이에요

2000년 이후 가장 많이 쓰인 이름 10개를 조회했더니 1위는 **Jacob(454,809명)** 이었습니다

편집기에 쿼리를 입력하면 실행 전에 아래쪽 예상 처리량이 갱신됩니다

**실행 시 이 쿼리가 143.71MB를 처리합니다**

실행하면 작업 정보 탭에 실제 처리량이 표시돼요

### 📊 작업 정보 탭의 값

| 항목 | 값 |
| :--- | :--- |
| 처리한 바이트 | **143.71MB** |
| 청구된 바이트 | <mark>144MB</mark> |
| 슬롯 밀리초 | 186 |
| 기간 | 345밀리초 |

CLI로 같은 쿼리를 실행하면 처리량이 **150,693,282바이트**로 나옵니다

콘솔은 1MB를 <u>1,048,576바이트</u>로 환산해 143.71MB가 됐어요

같은 양을 100만 바이트 단위로 쓰면 150.7MB입니다

청구된 바이트가 처리한 바이트보다 큰 이유는 MB 단위 올림이에요

요금 문서는 테이블마다, 쿼리마다 **최소 10MB**를 청구한다고 밝힙니다

### 💰 결제 계정 연결 시 예상 비용

| 항목 | 금액 |
| :--- | :--- |
| 1TiB 처리 | 약 8,310원(6.25달러) |
| 이 쿼리 한 번(144MB) | <mark>약 1.1원</mark> |
| 무료 1TiB로 실행 가능한 횟수 | 약 7,280번 |

샌드박스는 결제 계정이 없어 이 금액이 청구되지 않습니다

## 처리량을 정하는 것

![SELECT * 쿼리와 LIMIT 10을 붙인 쿼리의 dry_run 결과가 같은 bq 화면](/assets/images/tech/bigquery-sandbox-01-first-query/04-term-dryrun.webp)
*SELECT * 쿼리와 LIMIT 10을 붙인 쿼리의 dry_run 결과가 같은 bq 화면 — 출처: bq CLI 실행 결과 기반 자가 렌더*

CLI에서는 **--dry_run** 옵션을 사용하면 실행 없이 처리량만 알려 줍니다

공식 문서는 dry_run에는 요금을 청구하지 않는다고 밝혀요

같은 테이블을 대상으로 쿼리 네 개의 처리량을 예측해 봤습니다

![usa_names 테이블에 쿼리 네 개를 넣었을 때의 처리량 막대 차트](/assets/images/tech/bigquery-sandbox-01-first-query/05-chart.webp)
*usa_names 테이블에 쿼리 네 개를 넣었을 때의 처리량 막대 차트 — 출처: bq-sandbox-blog 실측 기반 자가 렌더*

SELECT *은 194.9MB를 처리합니다

여기에 LIMIT 10을 붙여도 <mark>194.9MB 그대로</mark>였어요!

LIMIT은 결과 행 수만 줄이고 테이블을 읽는 양은 그대로입니다

선택하는 열을 name과 number 두 개로 줄이면 **100.2MB**로 감소합니다

BigQuery는 데이터를 열 단위로 저장해서 고른 열만 읽기 때문이에요

WHERE year >= 2000을 넣은 TOP10 쿼리는 오히려 150.7MB로 증가했습니다

조건에 사용한 year 열도 읽어야 해서 처리 대상 열이 세 개로 늘었어요

이 테이블은 날짜별 파티션이 없어 WHERE 조건으로 읽는 범위를 줄이지 못합니다

날짜별 파티션 테이블에서 WHERE 조건이 처리량을 줄이는 방식은 <u>2탄 파티션 편</u>에서 다룹니다

## 쿼리 캐시

![INFORMATION_SCHEMA로 같은 쿼리의 실행 기록과 cache_hit 값을 조회한 bq 화면](/assets/images/tech/bigquery-sandbox-01-first-query/06-term.webp)
*INFORMATION_SCHEMA로 같은 쿼리의 실행 기록과 cache_hit 값을 조회한 bq 화면 — 출처: bq CLI 실행 결과 기반 자가 렌더*

같은 쿼리를 3초 뒤에 다시 실행했더니 처리량이 **0바이트**였습니다

캐시된 결과를 재사용해 cache_hit 값이 true로 기록됐어요

요금 문서도 캐시에서 가져온 결과는 청구하지 않는다고 적고 있습니다

콘솔에서 같은 쿼리의 줄바꿈을 바꿔 다시 실행했더니 캐시가 적용되지 않았습니다

처리량이 다시 **150,693,282바이트**로 기록됐어요

<u>쿼리 문자열이 하나라도 다르면</u> 캐시를 사용하지 않고 테이블을 다시 읽습니다

실행 기록은 **INFORMATION_SCHEMA.JOBS_BY_PROJECT** 뷰에 남습니다

이번 달 처리량을 합산하면 무료 1TiB 중 얼마나 사용했는지 확인할 수 있어요~

## 샌드박스에서 실행이 제한되는 쿼리

![CREATE TABLE AS SELECT는 성공하고 UPDATE는 거부된 bq 화면](/assets/images/tech/bigquery-sandbox-01-first-query/07-term-dml.webp)
*CREATE TABLE AS SELECT는 성공하고 UPDATE는 거부된 bq 화면 — 출처: bq CLI 실행 결과 기반 자가 렌더*

쿼리 결과로 테이블을 만드는 **CREATE TABLE AS SELECT**는 정상 실행됐습니다

2000년 이후 이름과 성별 조합 23,136행이 bq_lab.top_names에 저장됐어요

같은 테이블에 UPDATE 문을 실행하자 거부됐습니다

**DML queries are not allowed in the free tier**

INSERT 문도 같은 메시지로 거부됐습니다

DML 오류가 난 쿼리에는 처리량에 따른 요금이 청구되지 않아요

로컬 CSV 파일을 bq load로 업로드하는 작업은 성공했습니다

저장된 값을 수정하려면 <u>새 테이블을 CREATE TABLE AS SELECT로 다시 만들어야</u> 합니다

top_names의 만료 시각은 **2026년 12월 20일 12시 34분**으로 표시됐어요

## 1탄 정리

![1탄 실습에서 확인한 다섯 가지 정리 카드](/assets/images/tech/bigquery-sandbox-01-first-query/08-items.webp)
*1탄 실습에서 확인한 다섯 가지 정리 카드 — 출처: bq-sandbox-blog 실측 기반 자가 렌더*

2탄에서는 위키백과 조회수 테이블로 파티션과 클러스터가 처리량을 얼마나 줄이는지 측정합니다

한국어 위키백과 하루치는 **2억 9,488만 바이트** 이하로 예측됐어요

전체 언어 하루치는 64억 8,849만 바이트 이하였습니다

## 참고 출처

- [[Google Cloud] BigQuery 샌드박스 사용 (한도, 미지원 기능)](https://docs.cloud.google.com/bigquery/docs/sandbox)
- [[Google Cloud] BigQuery 가격 책정 (주문형 요금, MB 올림, 최소 10MB, 캐시 무료)](https://cloud.google.com/bigquery/pricing)
- [[Google Cloud] 쿼리 실행과 dry run (dry run 무료)](https://docs.cloud.google.com/bigquery/docs/running-queries)
- [[SSA] usa_names 원자료 (미국 사회보장국 이름 통계)](http://www.ssa.gov/OACT/babynames/limits.html)
- 환율: 1달러 ≈ 1,330원 기준 환산 (2026-10-21)
