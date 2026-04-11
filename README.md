# claude-skills

jaywapp의 개인 Claude Code 스킬 모음.

> **플러그인은 별도 저장소로 관리한다.** (`jaywapp/claude-plugin-{name}`)  
> 이 저장소는 단일 `.md` 파일로 구성되는 스킬만 포함한다.

## 사용법

원하는 스킬 폴더를 `~/.claude/skills/` 에 복사한다.

```bash
# 예: docs 스킬 설치
cp -r docs/SKILL.md ~/.claude/skills/docs.md
```

## 스킬 목록

| 스킬 | 설명 |
|------|------|
| [docs](./docs/SKILL.md) | MD 파일을 `D:\documents` 하위에 규칙에 맞게 저장하고 검색 |

## 구조

각 스킬은 독립 폴더로 관리된다. 폴더 내 `SKILL.md`가 스킬 본체다.

```
claude-skills/
  {skill-name}/
    SKILL.md    ← 스킬 본체 (Claude Code의 ~/.claude/skills/{skill-name}.md 로 복사)
```

---

## 작업 가이드

### 새 스킬 추가

**1. 로컬 스킬 파일 먼저 작성**

Claude Code가 스킬을 인식하는 경로에 직접 만든다:

```
C:\Users\jaywa\.claude\skills\{skill-name}.md
```

SKILL.md 프론트매터 형식:

```markdown
---
name: {skill-name}
description: 언제 이 스킬을 사용하는지 한 줄 설명 (Claude가 이걸 보고 스킬을 선택한다)
---

# 스킬 제목

...스킬 내용...
```

**2. 로컬에서 동작 검증 후 repo에 복사**

```bash
mkdir D:/workspace/claude-skills/{skill-name}
cp C:/Users/jaywa/.claude/skills/{skill-name}.md D:/workspace/claude-skills/{skill-name}/SKILL.md
```

**3. README 스킬 목록 업데이트**

`## 스킬 목록` 테이블에 새 스킬 한 줄 추가.

**4. 커밋 & 푸시**

```bash
cd D:/workspace/claude-skills
git add .
git commit -m "feat: add {skill-name} skill"
git push
```

---

### 기존 스킬 수정

로컬(`~/.claude/skills/`)과 repo(`D:/workspace/claude-skills/`) 양쪽을 동시에 수정한다. 한쪽만 수정하면 내용이 어긋난다.

```bash
# 로컬 파일 수정 후 repo에 반영
cp C:/Users/jaywa/.claude/skills/{skill-name}.md D:/workspace/claude-skills/{skill-name}/SKILL.md
cd D:/workspace/claude-skills
git add {skill-name}/SKILL.md
git commit -m "fix: update {skill-name} skill"
git push
```

---

### 다른 환경에서 스킬 가져오기

```bash
# 전체 clone
git clone https://github.com/jaywapp/claude-skills.git

# 원하는 스킬만 복사
cp claude-skills/{skill-name}/SKILL.md ~/.claude/skills/{skill-name}.md
```

---

### 커밋 메시지 컨벤션

| prefix | 용도 |
|--------|------|
| `feat:` | 새 스킬 추가 |
| `fix:` | 스킬 내용 수정 |
| `docs:` | README, 가이드 문서 수정 |
| `refactor:` | 폴더 구조 변경 (내용 변경 없음) |
