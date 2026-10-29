# rottensweetpotato.com

Jekyll 블로그. 내 프로젝트의 개발 일지(무엇을 했고 왜 그렇게 결정했는지)와 공부 기록(알고리즘 설명 등)을 쓴다.

## Commands

- `bundle install` — 의존성 설치
- `bundle exec jekyll serve` — 로컬 프리뷰 (http://localhost:4000)
- `npm run generate-og` — 포스트 OG 이미지 생성 (`assets/og/`, gitignore)
- `npm run generate-brand` — 파비콘·기본 OG 이미지 생성

## Architecture

- `_posts/<category-slug>/` — 글. 하위 폴더는 정리용이고 URL(`/posts/<slug>/`)에는 영향 없다.
- `_data/categories.yml` — front matter `category`·`subcategory` 의 유효값. 글이 없는 카테고리는 화면에서 숨겨진다.
- `_en_posts/` — 영문판 컬렉션 (`/en/posts/<slug>/`). 한국어 글과 파일명이 같으면 짝으로 묶인다. 화면 문구는 `_data/i18n.yml`.
- `assets/images/` — 글 이미지(WebP). 원본은 `assets/raw-images/`(gitignore)에 같은 구조로 둔다. `scripts/add-screenshot.py` 가 변환·배치한다.
- `_plugins/content_lastmod.rb` — 본문이 바뀐 글에만 수정 시각을 주고, 배포 워크플로가 그 URL 만 IndexNow 로 통지한다.
- `api/` — 댓글 API (별도 배포, 사이트는 아직 쓰지 않음).
- `docs/design/` — UI 방향·와이어프레임. UI 를 만지기 전에 읽는다.
- `Tasks.md` — 진행 중 작업.

## Environment

- CI 는 Ruby 3.3 / Node 22. `main` 푸시 시 `.github/workflows/deploy.yml` 가 rottensweetpotato.com 에 배포한다.
