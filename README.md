# LLM ISMS-P Policy Pack

## 목적

이 패키지는 Claude, Codex, Gemini 등 LLM 기반 도구가 개인정보, 중요정보, 운영데이터, 로그, 소스코드, 시크릿을 다룰 때 사전 점검을 수행하도록 하기 위한 Markdown 정책/스킬 묶음입니다.

프로그래밍 코드보다 Markdown 지침 중심으로 관리할 수 있도록 구성했습니다.

## 사용 효과

이 정책팩을 적용하면 에이전트의 동작이 다음처럼 바뀝니다.

| 상황 | 적용 전 | 적용 후 |
|---|---|---|
| 개인정보가 포함된 기능 기획 | 바로 요구사항, 화면, 코드 초안 작성 가능 | 먼저 데이터 등급, 처리 목적, 보관기간, 파기 기준, 승인 필요 여부를 판정 |
| 외부 LLM/API 사용 | API 호출 구조와 예시 코드를 바로 제안 가능 | 위탁, 재위탁, 국외이전, 프롬프트/응답 저장, 모델 학습 사용 여부를 먼저 확인 |
| 관리자 화면 설계 | 검색/조회/다운로드 기능을 편의 중심으로 설계 가능 | 최소권한, 마스킹, 검색 제한, 다운로드 승인, 접속기록을 설계 조건으로 반영 |
| 로그/RAG/벡터 DB 설계 | 프롬프트와 응답을 그대로 저장하는 설계 가능 | 개인정보 포함 여부, 접근권한, 보관기간, 파기 기준, 색인 제외/마스킹 여부를 점검 |
| 운영 DB 테스트 사용 | 운영 DB 복제 절차를 제안할 수 있음 | 원본 운영데이터 사용을 금지 또는 보류하고 합성/가공 데이터와 승인 절차를 요구 |
| 시크릿/API Key 처리 | 토큰을 프롬프트나 코드 예시에 포함할 수 있음 | 시크릿 입력·출력·로그 저장을 금지하고 제거 및 재발방지 조치를 요구 |

즉, 이 패키지는 에이전트를 개발 보조자에서 ISMS-P 관점의 사전 검토 보조자로 바꾸는 장치입니다. 다만 Markdown 지침은 모델 행동을 유도하는 통제이며, 법적 승인이나 보안 승인을 자동으로 대체하지 않습니다.

## 책임 범위

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

## 기준 문서

- 정보보호 및 개인정보보호 관리체계(ISMS-P) 인증기준 안내서, 2023.11.23
- 관리체계 수립 및 운영
- 보호대책 요구사항
- 개인정보 처리 단계별 요구사항

운영 시에는 법령, 고시, KISA 안내서의 최신 개정 여부를 별도로 확인해야 합니다.

## 빠른 적용

### 원격 원본 URL

이 저장소의 public GitHub URL과 raw URL을 정책 원본으로 사용합니다.

- 저장소: `https://github.com/hansonkim/llm-isms-p-policy-pack`
- 공통 지침: `https://raw.githubusercontent.com/hansonkim/llm-isms-p-policy-pack/main/AGENTS.md`
- Claude Code: `https://raw.githubusercontent.com/hansonkim/llm-isms-p-policy-pack/main/CLAUDE.md`
- Codex: `https://raw.githubusercontent.com/hansonkim/llm-isms-p-policy-pack/main/AGENTS.md`
- Gemini CLI: `https://raw.githubusercontent.com/hansonkim/llm-isms-p-policy-pack/main/GEMINI.md`

2026-04-30 기준 Claude Code, Codex, Gemini CLI는 영구 지침을 로컬 파일에서 자동 로드합니다. URL 자체를 원격 import로 매번 자동 로드하는 방식이 아니라, 위 URL을 기준으로 각 도구의 로컬 지침 파일을 설치하거나 갱신하십시오. 자세한 설치 명령은 `INSTALL.md`를 참고하십시오.

### Codex

Codex는 저장소 루트의 `AGENTS.md`를 기본 지침으로 사용합니다.

```bash
cp AGENTS.md /path/to/your/repo/AGENTS.md
cp -r .agents /path/to/your/repo/.agents
```

### Claude Code

Claude Code는 `CLAUDE.md`를 사용합니다. 이 패키지의 `CLAUDE.md`는 `AGENTS.md`를 import하도록 작성되어 있습니다.

```bash
cp AGENTS.md /path/to/your/repo/AGENTS.md
cp CLAUDE.md /path/to/your/repo/CLAUDE.md
cp -r .claude /path/to/your/repo/.claude
```

### Gemini CLI

Gemini CLI는 `GEMINI.md`를 사용합니다. 이 패키지의 `GEMINI.md`는 `AGENTS.md`와 세부 정책 문서를 import하도록 작성되어 있습니다.

```bash
cp AGENTS.md /path/to/your/repo/AGENTS.md
cp GEMINI.md /path/to/your/repo/GEMINI.md
```

Gemini extension으로 배포하려면 `gemini-llm-policy-extension/` 디렉터리를 Gemini CLI extension 경로에 배치하십시오.

## 핵심 원칙

LLM은 데이터를 받기 전에 다음을 먼저 판정해야 합니다.

- 데이터 종류
- 처리 행위
- 외부 전송 여부
- 위탁 또는 국외이전 가능성
- 보관기간
- 파기 기준
- 승인 및 증적 필요 여부

## 표준 판정

- 허용
- 조건부 허용
- 보류
- 금지

## 주요 파일

| 파일 | 용도 |
|---|---|
| `AGENTS.md` | Claude, Codex, Gemini 공통 기준 |
| `CLAUDE.md` | Claude Code용 어댑터 |
| `GEMINI.md` | Gemini CLI용 어댑터 |
| `.claude/skills/*/SKILL.md` | Claude Code skill |
| `.agents/skills/*/SKILL.md` | Codex Agent Skill |
| `gemini-llm-policy-extension/` | Gemini CLI extension |
| `llm-policy-pack/02-skills/` | 공통 skill 원문 |
| `llm-policy-pack/04-templates/` | 검토/승인 템플릿 |

## 운영 주의사항

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
