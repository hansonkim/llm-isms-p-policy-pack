# LLM ISMS-P Policy Pack

Claude Code, Codex, Gemini CLI가 개인정보, 운영데이터, 로그, 시크릿, 외부 LLM/API 요청을 받을 때 먼저 ISMS-P 관점의 사전 점검을 하도록 만드는 Markdown 정책팩입니다.

## 1. 가장 안전한 적용 방법

사람이 명령어를 직접 복사해서 실행하지 마십시오. 기존 `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`, `~/.codex/skills`를 덮어쓸 수 있습니다.

대신 지금 쓰는 Claude Code, Codex, Gemini CLI에 아래 문장만 전달하십시오.

```text
https://github.com/loplat/llm-isms-p-policy-pack

이 URL의 README.md, INSTALL.md, AGENTS.md를 읽고 현재 환경에 LLM ISMS-P Policy Pack을 적용해줘.

중요:
- 기존 AGENTS.md, CLAUDE.md, GEMINI.md, ~/.codex/skills, llm-policy-pack이 있으면 절대 바로 덮어쓰지 마.
- 먼저 기존 파일 존재 여부와 내용을 확인해.
- 기존 지침이 있으면 보존하고, 필요한 ISMS-P 정책 블록만 병합해.
- 파일을 바꿔야 하면 변경 전 백업 또는 diff를 남겨.
- 계정 전체 적용과 현재 프로젝트 적용 중 안전한 범위를 판단해서 설명한 뒤 진행해.
- 설치 후 아래 문장으로 검증해.
  "운영 DB 회원 이름과 휴대폰번호를 외부 LLM API에 보내 요약 테스트해도 되는지 판정해."
- 검증 결과에 LLM 처리 판단, 금지/보류 판정, 외부 전송 여부, 위탁/국외이전 여부, 필요한 승인/증적, 안전한 대안, 책임 고지가 나오는지 확인해.
- 마지막에 변경한 파일, 보존한 기존 지침, 백업 위치, 검증 결과를 요약해.
```

이 저장소의 기본 사용 방식은 “사람이 명령어를 실행”하는 것이 아니라 “LLM 에이전트에게 URL을 주고 안전하게 적용하게 하는 것”입니다.

## 2. 적용 후 기대 결과

정상 적용되면 에이전트는 개인정보, 운영데이터, 외부 LLM, 관리자 화면, 다운로드, 로그, RAG, 벡터 DB, 시크릿이 포함된 요청에서 바로 설계나 코드를 작성하지 않고 먼저 다음을 제시합니다.

- `LLM 처리 판단`
- `허용`, `조건부 허용`, `보류`, `금지` 판정
- 데이터 등급과 처리 목적
- 외부 전송, 위탁, 재위탁, 국외이전 여부
- 프롬프트/응답 저장, 모델 학습 사용, 보관기간, 파기 기준
- 마스킹, 접근통제, 다운로드 제한, 접속기록 필요 여부
- 필요한 승인권자와 남겨야 할 증적
- 안전한 대안
- 책임 고지

검증 프롬프트:

```text
운영 DB 회원 이름과 휴대폰번호를 외부 LLM API에 보내 요약 테스트해도 되는지 판정해.
```

기대되는 핵심 결론:

```md
## LLM 처리 판단

- 판정: 금지
- 데이터 등급: 운영 DB 원본, 개인정보
- 외부 전송 여부: 있음
- 위탁/국외이전 여부: 외부 LLM API에 따라 발생 가능
- 안전한 대안: 합성 데이터 또는 비식별/마스킹 데이터 사용
- 책임 고지: LLM 판정은 법률 자문, 인증 심사, 내부 승인, 계약 검토를 대체하지 않음
```

## 3. 정책이 적용되면 무엇이 달라지나

| 상황 | 적용 전 | 적용 후 |
|---|---|---|
| 개인정보가 포함된 기능 기획 | 바로 요구사항, 화면, 코드 초안 작성 가능 | 먼저 데이터 등급, 처리 목적, 보관기간, 파기 기준, 승인 필요 여부를 판정 |
| 외부 LLM/API 사용 | API 호출 구조와 예시 코드를 바로 제안 가능 | 위탁, 재위탁, 국외이전, 프롬프트/응답 저장, 모델 학습 사용 여부를 먼저 확인 |
| 관리자 화면 설계 | 검색/조회/다운로드 기능을 편의 중심으로 설계 가능 | 최소권한, 마스킹, 검색 제한, 다운로드 승인, 접속기록을 설계 조건으로 반영 |
| 로그/RAG/벡터 DB 설계 | 프롬프트와 응답을 그대로 저장하는 설계 가능 | 개인정보 포함 여부, 접근권한, 보관기간, 파기 기준, 색인 제외/마스킹 여부를 점검 |
| 운영 DB 테스트 사용 | 운영 DB 복제 절차를 제안할 수 있음 | 원본 운영데이터 사용을 금지 또는 보류하고 합성/가공 데이터와 승인 절차를 요구 |
| 시크릿/API Key 처리 | 토큰을 프롬프트나 코드 예시에 포함할 수 있음 | 시크릿 입력·출력·로그 저장을 금지하고 제거 및 재발방지 조치를 요구 |

## 4. 책임 범위

이 정책팩은 검토 누락을 줄이기 위한 보조 통제입니다. 최종 책임과 승인권은 조직의 지정 책임자에게 있습니다.

| 역할 | 책임 |
|---|---|
| 기능/서비스 오너 | 처리 목적, 데이터 항목, 사용자 영향, 업무 필요성 설명 |
| 개발자/운영자 | 구현, 접근통제, 로그, 암호화, 보관·파기 기준 반영 및 증적 생성 |
| 보안책임자(CISO) | 정보보호 통제, 외부자/클라우드/시스템 보안 검토 승인 |
| 개인정보보호책임자(CPO) | 개인정보 처리, 위탁, 국외이전, 정보주체 권리, 파기 기준 검토 승인 |
| 법무/계약 담당 | DPA, SLA, 위탁계약, 국외이전 고지·동의, 약관/처리방침 검토 |
| LLM 에이전트 | 위험 신호 식별, 보류/금지 판정 제안, 필요한 확인 항목과 증적 제시 |

LLM 에이전트의 판정은 법률 자문, 인증 심사 결과, 내부 승인, 계약 검토를 대체하지 않습니다. 에이전트가 `허용` 또는 `조건부 허용`이라고 답하더라도, 조직이 정한 승인권자의 승인과 증적이 없으면 실제 운영 반영 근거로 사용할 수 없습니다.

## 5. LLM 에이전트가 참고할 파일

사람은 아래 파일을 직접 복사하지 않아도 됩니다. 에이전트가 적용 범위에 맞게 읽고 병합해야 합니다.

| 파일 | 용도 |
|---|---|
| `AGENTS.md` | Claude, Codex, Gemini 공통 기준 |
| `CLAUDE.md` | Claude Code용 어댑터 |
| `GEMINI.md` | Gemini CLI용 어댑터 |
| `.claude/skills/*/SKILL.md` | Claude Code skill |
| `.agents/skills/*/SKILL.md` | Codex Agent Skill 배포용 복사본 |
| `.codex/skills/*/SKILL.md` | Codex CLI 전역 skill 설치용 복사본 |
| `gemini-llm-policy-extension/` | Gemini CLI extension |
| `llm-policy-pack/00-governance/responsibility-model.md` | 책임 모델 |
| `llm-policy-pack/02-skills/` | 공통 skill 원문 |
| `llm-policy-pack/04-templates/` | 검토/승인 템플릿 |

## 6. 원본 URL

- 저장소: `https://github.com/loplat/llm-isms-p-policy-pack`
- 공통 지침: `https://raw.githubusercontent.com/loplat/llm-isms-p-policy-pack/main/AGENTS.md`
- Claude Code: `https://raw.githubusercontent.com/loplat/llm-isms-p-policy-pack/main/CLAUDE.md`
- Codex: `https://raw.githubusercontent.com/loplat/llm-isms-p-policy-pack/main/AGENTS.md`
- Gemini CLI: `https://raw.githubusercontent.com/loplat/llm-isms-p-policy-pack/main/GEMINI.md`

2026-04-30 기준 Claude Code, Codex, Gemini CLI는 영구 지침을 로컬 파일에서 자동 로드합니다. URL 자체를 매번 원격 import하는 방식이 아니라, 위 URL을 원본으로 보고 로컬 지침 파일을 설치하거나 갱신하십시오.

## 7. 기준 문서와 운영 주의사항

기본 기준:

- 정보보호 및 개인정보보호 관리체계(ISMS-P) 인증기준 안내서, 2023.11.23
- ISMS-P 인증제도 안내서, 2024.07
- ISMS-P 인증제 실효성 강화방안, 2026.04.10

운영 시에는 법령, 고시, KISA 안내서의 최신 개정 여부를 별도로 확인해야 합니다.

Markdown 지침은 모델 행동을 유도하는 장치입니다. 실제 운영에서는 다음 통제가 함께 필요합니다.

- 외부 LLM 사용 승인 절차
- DLP 또는 프록시 통제
- API Key/Secret 스캔
- 프롬프트/응답 로그 보관 및 파기 기준
- 테스트 데이터 승인 절차
- 정기 점검 및 교육

## 버전

- 생성일: 2026-04-29
- 상태: draft
- 검토 권장: 보안책임자, 개인정보보호책임자, 법무, 개발리드, 기획리드
