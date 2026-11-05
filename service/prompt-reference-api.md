# 프롬프트·기준정보 API

프롬프트·기준정보 원본(서비스 DB)을 읽는 API다. 수집은 프롬프트 · 측정 설정 · 수집 기준정보를, 분석은 분석 기준정보를 읽는다. 지표, 판정, 답변 원문, 회차 · 측정 작업 기록은 주지 않는다. 주소는 [urls.md](../shared/urls.md)에 있다.

## 엔드포인트 (GET만)

| 경로 | 응답 |
|---|---|
| `/ext/v1/projects` | 허용된 프로젝트 목록: id · 상태 · 표면 · `change_seq` · `reset_seq` · etag |
| `/ext/v1/projects/{id}` | 프로젝트 정보와 측정 설정 |
| `/ext/v1/projects/{id}/prompts?after_seq=&limit=` | `change_seq` 순 프롬프트(삭제 표시 포함), `next_after_seq` · `has_more` |
| `/ext/v1/reference` | 공개된 기준정보 종류: 건수 · `change_seq` · etag |
| `/ext/v1/reference/{family}?after_key=&limit=` | 기준정보 항목, `next_after_key` · `has_more` |
| `/ext/healthz` | `{"ok": true}`. DB에 닿지 않으면 503 |

## 내보내는 데이터

| 구분 | 데이터 | 읽는 쪽 |
|---|---|---|
| 프롬프트 | Global prompts, Project 프롬프트 · 커스텀 태그. 상태는 active · draft · paused · archived · removed이고, active가 아니면 id와 상태만 나간다 | 수집 |
| 측정 설정 | 측정할 브랜드 · 국가, website 측정 단위 · 기준 URL, AI 엔진, 측정 주기, ACR 반복 수, 소유 URL, 추적 URL, 추적 대상 | 수집 |
| 수집 기준정보 | AI 엔진(`engine`), 국가(`country`), 언어(`language`), 글로벌 키워드 카탈로그(`interest_keyword`), 글로벌 소스 URL(`interest_source`) | 수집 |
| 분석 기준정보 | 분류 체계(`taxon`), 자사 브랜드(`brand`), 도메인 큐레이션(`source_override`), 시드(`source_seed`), 공식 소셜(`source_social`), 코드표(`source_code`), 브랜드 엔티티 역할(`entity_role`), 서비스 코드표(`surface` · `brand_bit` · `mention_type`) | 분석 |

각 항목의 내용은 [input-contract.md](../shared/input-contract.md).

## 변경 감지

- 모든 변경은 순번 하나(`change_seq`)를 받는다. 순번 순서가 커밋 순서다.
- 받는 쪽은 프로젝트마다 `after_seq`를 들고 이어 읽는다. 처음 보는 프로젝트나 `reset_seq`가 기준점보다 큰 프로젝트는 0부터 다시 읽는다.
- `meta.contract_version`이 바뀌면 전부, 기준정보는 etag가 바뀐 종류만 다시 읽는다.
