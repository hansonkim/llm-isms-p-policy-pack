---
owner: CISO/CPO
review_cycle: quarterly
last_reviewed: 2026-04-29
status: draft
source_reference: ISMS-P 인증기준 안내서(2023.11.23)
---

# LLM Skill Registry

| Skill ID | 이름 | 트리거 | 사용 대상 |
|---|---|---|---|
| LLM-SKILL-001 | LLM Data Gate | 데이터, 로그, 외부 LLM, 운영 DB | 전원 |
| LLM-SKILL-002 | Planning Privacy Review | 신규 기능, PRD, 고객 데이터 분석 | 기획자 |
| LLM-SKILL-003 | Development Security Review | API, DB, 관리자 기능, RAG, 로그 | 개발자 |
| LLM-SKILL-004 | Test Data Review | 테스트 데이터, 샘플 데이터, 개발 서버 | 개발자/QA |
| LLM-SKILL-005 | External LLM Vendor Review | 외부 LLM, SaaS, 클라우드, API | 기획/개발/보안 |
| LLM-SKILL-006 | Log Retention Review | 프롬프트 로그, 응답 로그, 접속기록 | 개발/운영 |
| LLM-SKILL-007 | Masking Output Review | 고객 목록, 엑셀, 보고서, 상담요약 | 전원 |
| LLM-SKILL-008 | Incident Triage | 오입력, 과다출력, 유출 의심 | 보안/개인정보 |

## Skill 작성 규칙

각 skill은 다음 구조를 따른다.

```md
---
id:
title:
owner:
review_cycle:
last_reviewed:
status:
isms_p_mapping:
---

# Skill

## Trigger
## Required Checks
## Decision
## Required Output
## Evidence
## Escalation
```
