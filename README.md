# Law KR

> 대한민국 법률·시행령·시행규칙을 Git으로 관리합니다.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE) [![data](https://img.shields.io/badge/data-Markdown-blue)](kr/) [![source](https://img.shields.io/badge/source-법제처_DRF_OpenAPI-orange)](https://open.law.go.kr)

대한민국 현행 **법률·시행령·시행규칙** 을 Markdown + YAML frontmatter 로 변환하여 Git 저장소에서 관리합니다. 각 법령은 공포일자를 Git commit date 로 갖고, 법령명·소관부처·법령구분·공포일자·시행일자·법령ID 를 메타·본문으로 보관합니다.

`wellsa-ai` 산하 [regulate-kr](https://github.com/wellsa-ai/regulate-kr) (행정규칙) · [precedent-kr](https://github.com/wellsa-ai/precedent-kr) (판례) 와 함께 **법률(뼈대) + 행정규칙(실무) + 판례(해석)** 의 전체 체계를 통일 패턴으로 관리합니다.

## 왜 필요한가?

법률은 **모든 규제·권리·의무의 근거** 입니다. 법률 텍스트뿐 아니라 **개정 이력 자체** 가 중요한 정보입니다 — 언제, 어떤 사회 변화에 의해, 어떤 조문이 바뀌었는지가 법령 해석의 핵심 단서입니다.

```
근로기준법 (법률)
  └─ 근로기준법 시행령 (대통령령)
       └─ 근로기준법 시행규칙 (고용노동부령)
            └─ 임금체불 사업주 명단 공개 고시 (행정규칙)
```

법률 → 시행령 → 시행규칙 → 행정규칙 → 판례 → 해석례 의 전체 흐름이 Git history 로 추적되어야 진정한 법령 데이터 인프라입니다.

## 빠른 시작

```bash
git clone https://github.com/wellsa-ai/law-kr.git
cd law-kr

# 특정 법령 보기
cat kr/근로기준법/법률.md

# 시행령·시행규칙 함께 보기
ls kr/근로기준법/

# 개정 이력
git log --format="%ai %s" -- kr/근로기준법/

# 두 법령 비교
diff kr/근로기준법/법률.md kr/근로자퇴직급여보장법/법률.md
```

## 구조

```
kr/{법령명}/
  법률.md           # 법률 본문 (조문)
  시행령.md         # 대통령령
  시행규칙.md       # 부령
  부칙.md           # 부칙
  별표1.md          # 별표
  ...
```

## 메타데이터 (YAML Frontmatter)

```yaml
---
법령명: 근로기준법
법령구분: 법률
소관부처: 고용노동부
공포일자: "2024-10-22"
시행일자: "2025-02-23"
공포번호: "법률 제20XXX호"
법령ID: "001234"
법령분야: 노동
상태: 현행
출처: https://www.law.go.kr/법령/근로기준법
---
```

## 자동 업데이트

매일 [국가법령정보센터 DRF API](https://open.law.go.kr) 의 `target=law` 를 체크하여 신규·개정 법령이 있으면 자동으로 커밋합니다.

- `pipeline/cron_update.sh` — 매일 06:00 KST (신규·개정 체크)
- `pipeline/cron_full_sweep.sh` — 매일 23:30 KST (전체 풀 스윕)

## 관련 프로젝트 (wellsa-ai 데이터 인프라)

| 프로젝트 | 대상 | 설명 |
|---|---|---|
| **law-kr** (이 저장소) | 법률·시행령·시행규칙 | 대한민국 법령 |
| [regulate-kr](https://github.com/wellsa-ai/regulate-kr) | 행정규칙·고시 | 전 부처 행정규칙 |
| [precedent-kr](https://github.com/wellsa-ai/precedent-kr) | 법원 판례 | 대한민국 법원 판례 |
| [interpretation-kr](https://github.com/wellsa-ai/interpretation-kr) | 법령해석례 | 법제처 법령해석례 |
| [constitution-kr](https://github.com/wellsa-ai/constitution-kr) | 헌재결정례 | 헌법재판소 결정례 |
| [localrule-kr](https://github.com/wellsa-ai/localrule-kr) | 자치법규 | 지자체 자치법규 |
| [treaty-kr](https://github.com/wellsa-ai/treaty-kr) | 조약 | 대한민국 조약 |

## 활용 사례

- **법률 검색**: 법령 + 행정규칙 + 판례 + 해석례 통합 검색 (예: [MiniLex](https://minilex.wellsa.ai))
- **준법감시(Compliance)**: 법령 개정 시 `git diff` 로 변경 조문 파악 → Gap 분석
- **법률 AI**: 7종 통합 학습 데이터셋
- **법학 교육·연구**: Git history 로 법령 변천 학습

## 데이터 출처

모든 법령 데이터는 [국가법령정보센터 DRF API](https://open.law.go.kr) 에서 가져옵니다. 법령 원문은 대한민국 정부 공공저작물로 자유롭게 이용 가능합니다.

## 라이선스

- 법령 원문: 공공저작물 (대한민국 정부)
- 저장소 구조·파이프라인 코드: MIT

## 기여

이슈, PR 환영합니다.
