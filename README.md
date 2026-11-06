# Subagents

Codex와 Claude Code에서 쓸 수 있는 Swift·Flutter·Python 서브에이전트 모음입니다. 도구별로 같은 이름의 역할 12개를 제공합니다.

| 폴더 | 설정 형식 | 전역 설치 경로 |
| --- | --- | --- |
| [Codex](codex/agents/) | TOML | `~/.codex/agents/` |
| [Claude Code](claude/agents/) | Markdown + YAML frontmatter | `~/.claude/agents/` |

## 역할

에이전트 이름은 `<언어>-<역할>` 형식입니다. 언어는 `swift`, `flutter`, `python` 중 하나입니다.

| 역할 | 담당 업무 |
| --- | --- |
| `architecture` | 기존 구조 조사, 변경 설계, 구현 범위와 검증 기준 정리 |
| `implementation` | 지정된 범위의 기능 구현, 버그 수정, 리팩터링 |
| `test` | 회귀 테스트 작성, 경계 조건과 비동기 실패 검증 |
| `reviewer` | 버그, 회귀, 보안 문제, 검증 누락 리뷰 |

## 설치

저장소 루트에서 사용하는 도구의 명령을 실행하세요. 설치 경로에 같은 이름의 파일이 있으면 건너뜁니다.

### Codex

```sh
mkdir -p "$HOME/.codex/agents"
for file in codex/agents/*.toml; do
  target="$HOME/.codex/agents/${file##*/}"
  if [ ! -e "$target" ] && [ ! -L "$target" ]; then
    cp -n "$file" "$target"
  fi
done
```

### Claude Code

```sh
mkdir -p "$HOME/.claude/agents"
for file in claude/agents/*.md; do
  target="$HOME/.claude/agents/${file##*/}"
  if [ ! -e "$target" ] && [ ! -L "$target" ]; then
    cp -n "$file" "$target"
  fi
done
```

한 프로젝트에서만 사용하려면 해당 프로젝트의 `.codex/agents/` 또는 `.claude/agents/`에 필요한 파일을 복사하세요.

## 사용 예시

- `swift-architecture` 서브에이전트로 이 변경의 설계와 수정 범위를 정리해줘.
- `flutter-test` 서브에이전트로 중복 탭과 요청 실패에 대한 회귀 테스트를 작성해줘.
- `python-reviewer` 서브에이전트로 이번 변경의 버그와 검증 누락을 리뷰해줘.

[Codex 서브에이전트 문서](https://learn.chatgpt.com/docs/agent-configuration/subagents) · [Claude Code 서브에이전트 문서](https://code.claude.com/docs/en/sub-agents)
