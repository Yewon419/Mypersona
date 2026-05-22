---
type: procedural
created: 2026-05-21
updated: 2026-05-21
importance: 6
trigger: "AskUserQuestion 호출에서 한글이 들어갈 때 (question, label, description)"
tags: [tool-use, korean, encoding, askuserquestion]
related: []
---

# AskUserQuestion 한글은 UTF-8 직접 입력 — Unicode escape 금지

## When to apply

`AskUserQuestion` 도구의 `question`·`option.label`·`option.description` 파라미터에 한글이 들어갈 때. JSON 직렬화 단계.

## Steps

1. 한글을 **UTF-8 그대로** 입력. 예: `"label": "풀 자체"`
2. JSON 표준 escape가 필요한 특수문자(`"`, `\`, 제어문자)만 escape

## Anti-patterns

- `\uXXXX` Unicode escape로 한글을 인코딩하지 말 것
  - 예: `"풀 자체"` 같은 패턴
  - 코드포인트가 어긋나는 사례 반복 발생 (인접 글자로 깨짐)
  - 관찰된 깨짐: "풀(풀)" → "풌(풌)", "헷갈렸다", "옆이야"

## Why

JSON 직렬화 시 한글 표현 방식 두 가지가 모두 valid (직접 입력 / `\uXXXX` escape). 하지만 후자는 작성·디버깅 단계에서 코드포인트를 사람이 또는 모델이 잘못 쓸 위험이 크다. 1자만 어긋나도 사용자가 의미 파악 불가능해지고, 잘못된 선택을 유도하거나 묻는 비용이 발생.

## Scope

- `AskUserQuestion`에 한정. `Write`/`Edit`/`Bash` 등 다른 도구는 이미 직접 입력 패턴 사용 중 — 패턴 유지
- 영어·숫자·기호는 무관
