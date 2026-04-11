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
