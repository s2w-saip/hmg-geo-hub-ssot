# URL 목록

## 저장소

| 이름 | URL | 내용 |
|---|---|---|
| 서비스 저장소 | https://github.com/s2w-saip/hmg-geo-hub | 서비스 FE(`front/`), BE(`back/`) |
| SSOT 저장소 | https://github.com/s2w-saip/hmg-geo-hub-ssot | 이 저장소 |

## 서비스 (S2W 내부망)

| 이름 | URL | 비고 |
|---|---|---|
| 서비스 화면 | http://10.0.20.132:8081/ | |
| 프롬프트·기준정보 API | https://10.0.20.132:8087/ext/ | 내부망(10.x)에서만, GET만. API 키 필요. 자체 서명 인증서. 서비스 코드에서는 `back/ext` |

프롬프트·기준정보 API는 서비스가 저장한 프롬프트와, 수집·가공에 필요한 기준정보(엔진·국가·언어, 분류 체계, 자사 브랜드, 출처 분류, 엔티티 역할, 시드 키워드 등)를 API 키별 범위로 준다. 지표·판정·답변 원문은 주지 않는다.

## 레거시

| 이름 | URL | 비고 |
|---|---|---|
| 레거시 프로젝트 | https://hmg-geo.vercel.app/ | 앤써가 진행 |

## 문서

| 이름 | 위치 |
|---|---|
| 서비스 구조, HUB DB ERD, 프롬프트·기준정보 API 명세 | 서비스 저장소 `docs/architecture/hmg-geo-hub-architecture.html` (프롬프트·기준정보 API는 `#ext` 절) |
