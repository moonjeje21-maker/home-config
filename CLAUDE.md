# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

`/Users/ky.moon`은 홈 폴더다. 실제 코드는 `workspace1/` 아래 각 폴더에 있고, 그 폴더의 `CLAUDE.md`를 먼저 읽는다.

## Git 주의

- 홈 폴더는 공개 저장소 `home-config`다. `.gitignore`가 모든 파일을 무시하고 `CLAUDE.md`·`.gitignore`만 예외로 둔다. 파일을 더 추적하려면 `.gitignore`에 `!파일명`을 추가하고, `*` 규칙은 지우지 않는다.
- 프로젝트 작업의 git 명령은 그 프로젝트 폴더 안에서 쓴다.
- `workspace1/friends-fortune/`, `workspace1/claude-nextjs/`는 별도 저장소라 그 폴더 안에서 따로 커밋·푸시한다. 나머지는 `workspace1` 저장소다.

## 작업 방식

- **[중요]** 파일을 고치는 작업은 plan 모드로 진행한다. 질문에 답하거나 파일을 읽기만 할 때는 쓰지 않는다.
- 계획이 승인되면 해당 프로젝트 아래 `plans/` 디렉토리(없으면 만든다)에 계획 md 파일로 저장한다.
  - 파일 이름: `날짜-프로젝트-주제-plan.md` (예: `2026-09-27-friends-fortune-gif-plan.md`)
  - 여러 프로젝트에 걸친 작업이면 관련된 프로젝트마다 `plans/`에 같은 계획을 넣는다.
  - 어느 프로젝트에도 속하지 않는 작업(예: `~/CLAUDE.md` 수정)은 따로 요청이 없으면 계획 파일을 저장하지 않는다.
  - 한국어로 쓴다. 작업이 끝나면 같은 파일에 완료 상태와 남은 작업을 적어 둔다.

## 기존 프로젝트 (정적 사이트)

- 빌드 단계·패키지 설치·테스트 도구 없이 HTML/CSS/JS 파일만 쓴다. 라이브러리나 프레임워크를 새로 추가하지 않는다.
- 데이터는 별도 JS 파일에서 `window` 전역 변수로 내보내고(`fortunes.js`, `lines.js`, `data.js` 등), `app.js`가 `<script>` 태그 순서대로 읽는다. 모듈(import/export)은 쓰지 않는다.
- 화면 문구는 한국어/영어 `{ ko, en }` 쌍으로 쓴다.
- 데이터를 `innerHTML`에 넣을 때는 이스케이프 함수(`escapeHtml()` / `esc()`)를 거친다.
- 실행: 프로젝트 폴더에서 `python3 -m http.server 8000` 후 `http://localhost:8000` (또는 `open index.html`)
- 문법 확인: `node --check app.js`

## 새 React 프로젝트

- 스택: Tailwind CSS, shadcn/ui, Zustand(상태관리), React Hook Form + Zod(폼)
- 들여쓰기 2칸, camelCase(컴포넌트는 PascalCase), `any` 타입 금지
- 컴포넌트는 나눠서 재사용하고, 반응형은 필수
