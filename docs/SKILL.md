---
name: docs
description: MD 파일을 D:\documents 하위에 규칙에 맞게 저장하거나 검색할 때 사용. Claude가 마크다운 문서를 생성할 때 반드시 이 스킬을 따른다.
---

# docs 스킬 — MD 파일 저장 & 검색

## 기본 규칙

**BASE_DIR:** `D:\documents`
(다른 환경에서 사용 시 해당 환경의 CLAUDE.md에서 BASE_DIR을 재정의한다)

**저장 경로 형식:**
```
D:\documents\{project}\{type}\{slug}.md
```

- `{project}`: 현재 작업 중인 프로젝트명 (예: `InsThor`, `moyeora`). 프로젝트 무관 문서는 `_global`
- `{type}`: 아래 유형 중 하나
- `{slug}`: 내용을 함축하는 짧은 영문 케밥케이스 (예: `auth-design`, `refactor-prompt`)
- 날짜는 파일명에 포함하지 않는다
- 동일 slug 문서는 덮어쓴다 (단일 진실 원칙)

## 문서 유형 (`{type}`)

| 타입 | 언제 사용 |
|------|-----------|
| `design` | 설계서, 아키텍처 문서, 스펙 |
| `prompt` | Claude에게 주는 프롬프트, 지시 파일 |
| `qa` | QA 리포트, 버그 메모, 테스트 결과 |
| `note` | 아이디어, 조사 메모, 기타 |

## 저장 모드 (`/docs save`)

Claude가 MD 파일을 생성할 때 아래 절차를 따른다:

1. **프로젝트 파악** — 현재 작업 컨텍스트에서 프로젝트명을 추론한다. 불명확하면 사용자에게 확인한다.
2. **유형 판단** — 문서 내용을 보고 `design` / `prompt` / `qa` / `note` 중 하나를 선택한다.
3. **slug 결정** — 문서 핵심 내용을 3단어 이내 영문 케밥케이스로 표현한다.
4. **경로 결정** — `D:\documents\{project}\{type}\{slug}.md`
5. **디렉토리 생성** — 경로가 없으면 먼저 생성한다.
6. **파일 저장** — Write 도구로 저장한다.
7. **경로 보고** — 사용자에게 저장된 전체 경로를 알린다.

## 검색 모드 (`/docs search {query}`)

`D:\documents` 전체에서 키워드를 검색하고 결과를 계층 구조로 출력한다.

절차:
1. Grep으로 `D:\documents` 전체에서 파일 내용 검색 (`pattern: {query}`, `path: D:\documents`)
2. Glob으로 `D:\documents\**\*{query}*.md` 패턴으로 파일명 검색
3. 두 결과를 합쳐 중복 제거 후 아래 형식으로 출력:

```
{project} > {type}
  - {slug}.md  (매칭된 라인 또는 파일명)
```

## 이식성 안내

이 스킬 파일(`docs.md`) 하나를 다른 Claude 환경의 `~/.claude/skills/` 에 복사하면 동작한다.
다른 베이스 경로를 사용하는 환경은 해당 CLAUDE.md에 아래를 추가한다:

```
docs 스킬의 BASE_DIR은 D:\documents 대신 {원하는 경로}를 사용한다.
```
