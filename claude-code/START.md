# Claude Code에서 시작하기

**파일럿용 초안. 플랫폼 완료 검증 전입니다.** Claude 일반 채팅·Cowork·Chrome 사이드패널 단독용 설치 파일이 아닙니다.

1. 이 `claude-code` 폴더에서 Claude Code를 시작합니다. CLAUDE.md와 andrew-autoupload 폴더를 함께 두면 자연어 요청으로 스킬을 읽습니다.
2. 직접 Anthropic 유료 플랜(Pro/Max/Team/Enterprise), Claude in Chrome 확장 1.0.36 이상, 파일 업로드를 위한 Claude Code 2.1.211 이상이 공식 전제입니다. 가능한 최신 버전을 사용하세요. 이는 문서상 최소 조건이며 이 패키지의 검증 버전은 아직 없습니다.
3. `/login`으로 로그인하고 `claude --chrome`으로 시작합니다. API 키 또는 setup-token 인증을 Chrome 연결 대용으로 사용하지 마세요. `/chrome`에서 연결 확인·재연결 및 Chrome 선택을 합니다.
4. 같은 Chrome 프로필에서 인스타그램·네이버에 로그인하고 필요한 사이트 동작을 승인합니다.
5. “andrew-autoupload 스킬로 연결 점검만 해줘”로 점검 후 “andrew-autoupload 스킬로 비 오는 날 여행 게시물을 준비해줘”로 시작합니다. `/andrew-autoupload` 명령도 사용하려면 andrew-autoupload 폴더를 프로젝트의 .claude/skills/ 안에 복사하고 새 세션을 시작하세요.

네이버 블로그는 Claude in Chrome에서 이동이 거부될 수 있습니다. macOS라면 ego-browser 스킬과 ego lite 앱을 함께 준비하면 네이버와 인스타그램을 ego lite 경로로 진행합니다. 스킬 파일만으로는 동작하지 않고 앱 설치와 최초 온보딩까지 마쳐야 `ego-browser` 명령이 PATH에 등록됩니다. ego lite 설치 스크립트는 macOS 전용이라 Windows에서는 네이버 자동 입력을 지원하지 않으며 원고를 직접 붙여넣어야 합니다.

정사각형 또는 4:5 이미지 1장을 미리 준비하세요. 이 버전은 이미지 생성 프롬프트를 작성하며 실제 이미지 첨부는 제공된 파일로 진행합니다. 주소는 channels.md가 있으면 다시 묻지 않습니다.

Claude의 첨부는 세션의 파일 읽기 권한이 필요합니다. 한 번에 총 10MB 이내여야 하며 다중 하드링크 파일은 복사본을 사용합니다. 파일 URL 설정을 업로드의 만능 해결책으로 안내하지 않습니다.

검수 전에 `/clear`를 실행하지 마세요. 작성 중인 탭이 닫힐 수 있습니다. 최종 게시 버튼은 직접 누릅니다. 재공유 시 channels.md, brand.md, inputs/, outputs/, .preflight.json과 개인 캡처를 제외하세요.

[공식 Chrome 연결·첨부 문서](https://code.claude.com/docs/en/chrome) · [프로젝트 스킬 안내](https://code.claude.com/docs/en/skills)
