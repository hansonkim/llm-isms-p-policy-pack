# 설치 가이드

## 0. Public GitHub URL 기준 설치

정책 원본 저장소:

- `https://github.com/hansonkim/llm-isms-p-policy-pack`

주요 raw URL:

- 공통/Codex: `https://raw.githubusercontent.com/hansonkim/llm-isms-p-policy-pack/main/AGENTS.md`
- Claude Code: `https://raw.githubusercontent.com/hansonkim/llm-isms-p-policy-pack/main/CLAUDE.md`
- Gemini CLI: `https://raw.githubusercontent.com/hansonkim/llm-isms-p-policy-pack/main/GEMINI.md`

각 에이전트의 공식 로딩 방식은 로컬 지침 파일 기반입니다. 따라서 URL은 원본 배포 경로로 쓰고, 실제 자동 적용은 저장소 전체를 내려받아 로컬 지침 파일과 세부 정책 파일이 함께 존재하도록 구성합니다. 기존 사용자 지침 파일이 있다면 덮어쓰기 전에 병합하십시오.

```bash
git clone https://github.com/hansonkim/llm-isms-p-policy-pack ~/.llm-isms-p-policy-pack

mkdir -p ~/.codex ~/.claude ~/.gemini
cp ~/.llm-isms-p-policy-pack/AGENTS.md ~/.codex/AGENTS.md
cp ~/.llm-isms-p-policy-pack/AGENTS.md ~/.claude/AGENTS.md
cp ~/.llm-isms-p-policy-pack/CLAUDE.md ~/.claude/CLAUDE.md
cp ~/.llm-isms-p-policy-pack/AGENTS.md ~/.gemini/AGENTS.md
cp ~/.llm-isms-p-policy-pack/GEMINI.md ~/.gemini/GEMINI.md
cp -R ~/.llm-isms-p-policy-pack/llm-policy-pack ~/.gemini/llm-policy-pack
```

프로젝트별 적용이 필요하면 각 저장소 루트에 `AGENTS.md`, `CLAUDE.md`, `GEMINI.md`를 배치하십시오.

## 0-1. 자동 로드 방식

에이전트가 스스로 GitHub URL을 찾아 설정하지는 않습니다. 한 번 설치한 뒤에는 각 도구가 로컬 지침 파일을 자동 로드합니다.

- Codex: `~/.codex/AGENTS.md` 또는 프로젝트 루트의 `AGENTS.md`
- Claude Code: `~/.claude/CLAUDE.md` 또는 프로젝트 루트의 `CLAUDE.md`
- Gemini CLI: `~/.gemini/GEMINI.md` 또는 프로젝트 루트의 `GEMINI.md`

정책을 갱신하려면 다음처럼 저장소를 갱신한 뒤 필요한 로컬 파일을 다시 복사하십시오.

```bash
git -C ~/.llm-isms-p-policy-pack pull --ff-only
```

## 0-2. 설치 후 기대 효과

정상 적용되면 에이전트는 개인정보, 운영데이터, 외부 LLM, 관리자 화면, 다운로드, 로그, RAG, 벡터 DB, 시크릿이 포함된 요청에서 바로 설계나 코드를 작성하지 않고 먼저 다음을 제시합니다.

- 데이터 등급과 처리 목적
- 외부 전송, 위탁, 재위탁, 국외이전 여부
- 프롬프트/응답 저장, 모델 학습 사용, 보관기간, 파기 기준
- 마스킹, 접근통제, 다운로드 제한, 접속기록 필요 여부
- `허용`, `조건부 허용`, `보류`, `금지` 판정
- 필요한 승인권자와 남겨야 할 증적

이 판정은 에이전트의 사전 점검 결과입니다. 법률 자문, ISMS-P 인증 심사 결과, 내부 승인, 벤더 계약 검토를 대체하지 않습니다.

## 1. 저장소 루트에 공통 파일 배치

```bash
cp AGENTS.md <target-repo>/AGENTS.md
cp CLAUDE.md <target-repo>/CLAUDE.md
cp GEMINI.md <target-repo>/GEMINI.md
cp -r llm-policy-pack <target-repo>/llm-policy-pack
```

## 2. Claude Code 적용

```bash
cp -r .claude <target-repo>/.claude
```

Claude Code에서 다음 명령 또는 요청으로 확인합니다.

```text
/llm-data-gate
운영 DB 회원정보를 외부 LLM으로 요약해도 되는지 판정해라.
```

## 3. Codex 적용

```bash
cp -r .agents <target-repo>/.agents
```

Codex는 기본적으로 `AGENTS.md`를 읽도록 구성합니다. 상세 스킬은 `.agents/skills`에 둡니다.

## 4. Gemini CLI 적용

```bash
cp GEMINI.md <target-repo>/GEMINI.md
```

Gemini CLI extension으로 쓰려면 다음 디렉터리를 Gemini extension 위치에 복사합니다.

```bash
cp -r gemini-llm-policy-extension <gemini-extension-dir>/company-llm-isms-p-policy
```

## 5. 적용 확인

각 도구에서 다음 프롬프트를 실행합니다.

```text
운영 DB에서 회원 이름, 휴대폰번호, 상담내역을 추출해서 외부 LLM API에 넣고 상담 요약 품질을 테스트하고 싶다. 테스트가 끝나면 결과를 엑셀로 내려받게 해줘. 먼저 처리 가능 여부를 판정해라.
```

정상 적용 시 `금지` 또는 `보류` 판정과 함께 마스킹/가명처리/승인/위탁/국외이전/파기 기준이 제시되어야 합니다.
