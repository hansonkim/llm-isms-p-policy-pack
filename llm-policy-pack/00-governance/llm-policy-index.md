---
owner: CISO/CPO
review_cycle: quarterly
last_reviewed: 2026-04-30
status: draft
source_reference: ISMS-P 인증기준 안내서(2023.11.23), ISMS-P 인증제도 안내서(2024.07), ISMS-P 인증제 실효성 강화방안(2026.4.10)
---

# LLM 정책 색인

## 목적

LLM 사용 시 개인정보와 중요정보가 부적절하게 입력, 저장, 출력, 전송되는 것을 방지하기 위한 정책 문서의 색인이다.

## 문서 체계

| 영역 | 문서 | 용도 |
|---|---|---|
| 책임 모델 | `00-governance/responsibility-model.md` | LLM 판정과 조직 내 승인/책임 경계 정의 |
| 공통 지침 | `01-core-instructions/core-data-handling-instruction.md` | 모든 LLM 데이터 처리 요청의 기본 원칙 |
| 금지 데이터 | `01-core-instructions/prohibited-data-instruction.md` | 입력·출력·저장 금지 정보 |
| 출력 최소화 | `01-core-instructions/output-minimization-instruction.md` | 마스킹 및 집계 출력 기준 |
| 에스컬레이션 | `01-core-instructions/escalation-instruction.md` | 보류·금지·사고 후보 처리 |
| 데이터 게이트 | `02-skills/skill-llm-data-gate.md` | 데이터 처리 전 판정 |
| 기획 검토 | `02-skills/skill-planning-review.md` | PRD, 화면, 정책, 분석 기획 검토 |
| 개발 검토 | `02-skills/skill-development-review.md` | API, DB, 로그, 관리자 기능 검토 |
| 테스트 데이터 | `02-skills/skill-test-data-review.md` | 운영데이터의 개발/시험 사용 방지 |
| 외부 LLM | `02-skills/skill-external-llm-vendor-review.md` | SaaS/API/클라우드 LLM 검토 |
| 로그 보관 | `02-skills/skill-log-retention-review.md` | 프롬프트/응답/접속기록 보관 검토 |
| 출력 마스킹 | `02-skills/skill-masking-output-review.md` | 개인정보 출력 최소화 |
| 사고 분류 | `02-skills/skill-incident-triage.md` | 유출·오입력·과다출력 사고 후보 분류 |

## 운영 원칙

1. 공통 지침은 짧고 강하게 유지한다.
2. 세부 절차는 skill 문서에 둔다.
3. 실수 사례가 발생하면 관련 skill을 보강한다.
4. 법령, 고시, 안내서 개정 시 `legal-update-log.md`를 먼저 갱신한다.
5. 개정 시 보안책임자와 개인정보보호책임자의 승인을 받는다.
6. LLM 판정은 사전 검토 보조이며, 운영 반영은 지정 승인권자의 승인과 증적을 기준으로 한다.
