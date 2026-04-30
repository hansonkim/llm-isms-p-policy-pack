@AGENTS.md

# CLAUDE.md - Claude Code 전용 어댑터

## 적용 원칙

Claude는 데이터, 로그, 고객정보, 테스트 데이터, 외부 LLM, 클라우드, RAG, 임베딩, 프롬프트 로그가 언급되면 먼저 LLM Data Gate를 적용한다.

## 우선 사용할 Skill

- `/llm-data-gate`
- `/planning-privacy-review`
- `/development-security-review`
- `/test-data-review`
- `/external-llm-vendor-review`

## Claude Code 작업 규칙

1. 정책 판단 없이 코드 생성부터 시작하지 않는다.
2. 개인정보 또는 중요정보가 포함된 요청은 판정 결과를 먼저 제시한다.
3. 개발 작업은 보안 요구사항, 마스킹, 접근권한, 로그, 파기 기준을 먼저 정리한 뒤 진행한다.
4. 사용자가 운영 데이터 사용을 요청하면 시험 데이터 보안 검토를 수행한다.
5. 외부 LLM API를 사용하는 경우 위탁, 국외이전, 프롬프트/응답 보관 여부를 먼저 확인한다.
