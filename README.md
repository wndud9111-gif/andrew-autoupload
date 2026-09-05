# andrew-autoupload

블로그·인스타그램 초안 준비 스킬

키워드 하나로 조사·이미지 준비·초안 작성·브라우저 입력까지 맡기고, 최종 게시 버튼은 사용자가 직접 누릅니다.

**상태: 파일럿용 초안. 두 제품 모두 실제 네이버·인스타그램 완료 검증 전입니다.** 저장소 검토용으로 공유할 수 있지만, 일반 수강생에게 검증 완료판으로 배포하지 마세요. 설치 조건을 충족해도 플랫폼 동작이 보장되지는 않습니다.

## 나에게 맞는 폴더 하나 선택

| 사용하는 도구 | 가져갈 폴더 | 처음 읽을 안내 |
|---|---|---|
| Codex 데스크톱 로컬 + Chrome 확장 | `codex/` 전체 | [Codex 시작하기](codex/START.md) |
| Claude Code 로컬 + Claude in Chrome | `claude-code/` 전체 | [Claude Code 시작하기](claude-code/START.md) |

Claude Code판은 네이버 블로그가 Claude in Chrome에서 차단될 수 있습니다. macOS에서는 ego-browser 스킬과 ego lite 앱을 함께 준비하면 네이버·인스타그램을 ego lite 경로로 진행하고, Windows에서는 네이버 자동 입력을 지원하지 않습니다. 조건은 [Claude Code 시작하기](claude-code/START.md)에 있습니다.

선택한 폴더 자체를 새 프로젝트로 여세요. 각 폴더 안에 andrew-autoupload/SKILL.md가 바로 보이며 숨김 폴더는 없습니다. AGENTS.md 또는 CLAUDE.md가 스킬을 읽도록 연결합니다. 기존 프로젝트의 지침 문서를 덮어쓰지 마세요. Claude 일반 채팅·Cowork·Chrome 사이드패널 단독 사용은 이 패키지의 검증 대상이 아닙니다.

## 저장소 구조

```text
andrew-autoupload/
├── README.md
├── codex/
│   ├── AGENTS.md
│   ├── START.md
│   ├── VALIDATION.md
│   └── andrew-autoupload/
│       ├── SKILL.md
│       ├── references/chrome.md
│       └── assets/
└── claude-code/
    ├── CLAUDE.md
    ├── START.md
    ├── VALIDATION.md
    └── andrew-autoupload/
        ├── SKILL.md
        ├── references/chrome.md
        └── assets/
```

## 스킬과 진입 문서의 차이

- `SKILL.md`: 에이전트가 업무를 수행할 때 읽는 실제 스킬입니다.
- `AGENTS.md` / `CLAUDE.md`: 각 도구가 해당 프로젝트의 스킬을 읽도록 연결합니다.
- `START.md`: 사람이 읽는 설치·사용 안내입니다.

별도 상주 프로그램이나 서버, 여러 하위 에이전트를 설치하지 않습니다. 기존 에이전트 한 명이 스킬에 따라 도구를 사용합니다. 브라우저 확장과 로그인은 별도로 준비합니다.

## 공통 사용법

1. 선택한 프로젝트에서 시작 안내대로 Chrome을 연결합니다.
2. “andrew-autoupload 스킬로 비 오는 날 여행을 주제로 블로그와 인스타 초안을 준비해줘.”라고 요청합니다.
3. `channels.md`가 없으면 인스타그램 주소, 네이버 주소를 순서대로 답합니다. 저장된 정상 주소는 다시 묻지 않습니다.
4. 게시 직전 화면을 검토하고 직접 게시합니다. 다음에는 주제만 바꾸거나 “이어서 준비해줘”라고 요청합니다.

이미지는 Codex에서 연결된 생성 도구가 있으면 생성하고, 없으면 사용자 제공 파일을 사용합니다. Claude Code판은 이미지를 생성하지 않습니다. 사용자가 제공한 이미지 파일이 있어야 인스타그램·네이버 입력 단계로 넘어가며, 파일이 없으면 생성용 추천 프롬프트를 제안하고 원고와 프롬프트만 저장한 채 두 채널의 입력을 모두 보류합니다.

## 검증 및 공유

각 폴더의 `VALIDATION.md`에 실제 OS·플랜·앱·확장·도구 버전과 파일럿 결과를 기록합니다. 한 환경의 성공을 다른 환경으로 확대하지 않습니다. Windows·macOS는 각각 검증해야 합니다.

재공유 시 `channels.md`, `brand.md`, `inputs/`, `outputs/`, `.preflight.json`, 로그인 정보와 개인 캡처를 제외하세요. `.gitignore`는 Git에만 적용되므로 파일을 직접 압축할 때도 제외해야 합니다. 수업은 테스트 계정으로 진행하고 사이트 이용 조건을 지킵니다.

이 저장소는 두 환경의 지침을 의도적으로 분리합니다. 공통 흐름을 수정할 때는 양쪽 SKILL.md에 적용하고, 브라우저 안내는 해당 제품 문서만 수정하세요.
