# LLM ISMS-P Policy Pack

Claude Code, Codex, Gemini CLI가 개인정보, 운영데이터, 로그, 시크릿, 외부 LLM/API 요청을 받을 때 먼저 ISMS-P 관점의 사전 점검을 하도록 만드는 Markdown 정책팩입니다.

이 저장소를 읽는 첫 사용자는 아래 순서대로 진행하십시오.

## 1. 먼저 적용 범위를 정한다

| 원하는 적용 방식 | 언제 선택하나 | 해야 할 일 |
|---|---|---|
| 내 계정 전체 적용 | 내가 쓰는 Claude/Codex/Gemini에서 항상 이 정책을 적용하고 싶다 | `~/.claude`, `~/.codex`, `~/.gemini`에 설치 |
| 특정 프로젝트만 적용 | 특정 저장소에서만 정책을 적용하고 싶다 | 대상 repo 루트에 `AGENTS.md`, `CLAUDE.md`, `GEMINI.md` 복사 |
| 조직 표준으로 배포 | 여러 사람이 같은 정책을 쓰게 하고 싶다 | 이 repo를 기준으로 각 개발자 환경 또는 프로젝트 템플릿에 배포 |

처음이면 **내 계정 전체 적용**으로 시작하는 것이 가장 빠릅니다.

## 2. 내 계정에 설치한다

```bash
git clone https://github.com/loplat/llm-isms-p-policy-pack ~/.llm-isms-p-policy-pack

mkdir -p ~/.codex ~/.codex/skills ~/.claude ~/.gemini

cp ~/.llm-isms-p-policy-pack/AGENTS.md ~/.codex/AGENTS.md
cp -R ~/.llm-isms-p-policy-pack/.codex/skills/* ~/.codex/skills/

cp ~/.llm-isms-p-policy-pack/AGENTS.md ~/.claude/AGENTS.md
cp ~/.llm-isms-p-policy-pack/CLAUDE.md ~/.claude/CLAUDE.md

cp ~/.llm-isms-p-policy-pack/AGENTS.md ~/.gemini/AGENTS.md
cp ~/.llm-isms-p-policy-pack/GEMINI.md ~/.gemini/GEMINI.md
cp -R ~/.llm-isms-p-policy-pack/llm-policy-pack ~/.gemini/llm-policy-pack
```

이미 각 도구의 지침 파일을 쓰고 있다면 덮어쓰기 전에 기존 내용을 병합하십시오.

## 3. 프로젝트에만 설치한다

대상 프로젝트 루트에서 실행합니다.

```bash
cp ~/.llm-isms-p-policy-pack/AGENTS.md ./AGENTS.md
cp ~/.llm-isms-p-policy-pack/CLAUDE.md ./CLAUDE.md
cp ~/.llm-isms-p-policy-pack/GEMINI.md ./GEMINI.md
cp -R ~/.llm-isms-p-policy-pack/llm-policy-pack ./llm-policy-pack
```

Codex skill까지 명시적으로 쓰려면 다음도 설치합니다.

```bash
mkdir -p ~/.codex/skills
cp -R ~/.llm-isms-p-policy-pack/.codex/skills/* ~/.codex/skills/
```

## 4. 적용됐는지 확인한다

Claude, Codex, Gemini 중 사용하는 도구에서 아래 문장을 입력합니다.

```text
운영 DB 회원 이름과 휴대폰번호를 외부 LLM API에 보내 요약 테스트해도 되는지 판정해.
```

정상 적용되면 에이전트가 바로 코드나 절차를 만들지 않고 다음 항목을 먼저 답해야 합니다.

- `LLM 처리 판단`
- `판정: 금지` 또는 `보류`
- 데이터 등급
- 외부 전송 여부
- 위탁/국외이전 여부
- 필요한 승인/증적
- 안전한 대안
- 책임 고지

예상되는 핵심 결론은 다음과 같습니다.

```md
## LLM 처리 판단

- 판정: 금지
- 데이터 등급: 운영 DB 원본, 개인정보
- 외부 전송 여부: 있음
- 위탁/국외이전 여부: 외부 LLM API에 따라 발생 가능
- 안전한 대안: 합성 데이터 또는 비식별/마스킹 데이터 사용
- 책임 고지: LLM 판정은 법률 자문, 인증 심사, 내부 승인, 계약 검토를 대체하지 않음
```

## 5. 정책이 적용되면 무엇이 달라지나

| 상황 | 적용 전 | 적용 후 |
|---|---|---|
| 개인정보가 포함된 기능 기획 | 바로 요구사항, 화면, 코드 초안 작성 가능 | 먼저 데이터 등급, 처리 목적, 보관기간, 파기 기준, 승인 필요 여부를 판정 |
| 외부 LLM/API 사용 | API 호출 구조와 예시 코드를 바로 제안 가능 | 위탁, 재위탁, 국외이전, 프롬프트/응답 저장, 모델 학습 사용 여부를 먼저 확인 |
| 관리자 화면 설계 | 검색/조회/다운로드 기능을 편의 중심으로 설계 가능 | 최소권한, 마스킹, 검색 제한, 다운로드 승인, 접속기록을 설계 조건으로 반영 |
| 로그/RAG/벡터 DB 설계 | 프롬프트와 응답을 그대로 저장하는 설계 가능 | 개인정보 포함 여부, 접근권한, 보관기간, 파기 기준, 색인 제외/마스킹 여부를 점검 |
| 운영 DB 테스트 사용 | 운영 DB 복제 절차를 제안할 수 있음 | 원본 운영데이터 사용을 금지 또는 보류하고 합성/가공 데이터와 승인 절차를 요구 |
| 시크릿/API Key 처리 | 토큰을 프롬프트나 코드 예시에 포함할 수 있음 | 시크릿 입력·출력·로그 저장을 금지하고 제거 및 재발방지 조치를 요구 |

## 6. 책임 범위를 이해한다

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

## 7. 정책을 갱신한다

```bash
git -C ~/.llm-isms-p-policy-pack pull --ff-only
```

갱신 후 필요한 파일을 다시 복사합니다.

```bash
cp ~/.llm-isms-p-policy-pack/AGENTS.md ~/.codex/AGENTS.md
cp -R ~/.llm-isms-p-policy-pack/.codex/skills/* ~/.codex/skills/
cp ~/.llm-isms-p-policy-pack/CLAUDE.md ~/.claude/CLAUDE.md
cp ~/.llm-isms-p-policy-pack/GEMINI.md ~/.gemini/GEMINI.md
cp -R ~/.llm-isms-p-policy-pack/llm-policy-pack ~/.gemini/llm-policy-pack
```

## 8. 원본 URL

- 저장소: `https://github.com/loplat/llm-isms-p-policy-pack`
- 공통 지침: `https://raw.githubusercontent.com/loplat/llm-isms-p-policy-pack/main/AGENTS.md`
- Claude Code: `https://raw.githubusercontent.com/loplat/llm-isms-p-policy-pack/main/CLAUDE.md`
- Codex: `https://raw.githubusercontent.com/loplat/llm-isms-p-policy-pack/main/AGENTS.md`
- Gemini CLI: `https://raw.githubusercontent.com/loplat/llm-isms-p-policy-pack/main/GEMINI.md`

2026-04-30 기준 Claude Code, Codex, Gemini CLI는 영구 지침을 로컬 파일에서 자동 로드합니다. URL 자체를 매번 원격 import하는 방식이 아니라, 위 URL을 원본으로 보고 로컬 지침 파일을 설치하거나 갱신하십시오.

## 9. 주요 파일

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

## 10. 기준 문서와 운영 주의사항

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
