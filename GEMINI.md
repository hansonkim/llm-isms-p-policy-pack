@./AGENTS.md

# GEMINI.md - Gemini CLI 전용 어댑터

## 적용 원칙

Gemini는 개인정보, 중요정보, 로그, 운영 DB, 테스트 데이터, 외부 LLM, 클라우드, RAG, 임베딩, 프롬프트 로그가 포함된 요청을 처리하기 전에 공통 LLM Data Gate를 적용한다.

## 상세 정책 Import

@./llm-policy-pack/01-core-instructions/core-data-handling-instruction.md
@./llm-policy-pack/02-skills/skill-llm-data-gate.md
@./llm-policy-pack/02-skills/skill-planning-review.md
@./llm-policy-pack/02-skills/skill-development-review.md
@./llm-policy-pack/02-skills/skill-test-data-review.md
@./llm-policy-pack/02-skills/skill-external-llm-vendor-review.md
@./llm-policy-pack/02-skills/skill-masking-output-review.md

## Gemini 작업 규칙

1. 데이터 관련 요청은 허용/조건부 허용/보류/금지로 먼저 판정한다.
2. 보류 또는 금지 요청은 안전한 대안을 제시한다.
3. 외부 LLM, SaaS, API, 클라우드 연계는 벤더 검토 항목을 먼저 확인한다.
4. 개발 또는 기획 산출물은 ISMS-P 증적 매핑을 함께 제시한다.
