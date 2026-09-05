# Codex에서 시작하기

**파일럿용 초안. 플랫폼 완료 검증 전입니다.** 검증 결과는 VALIDATION.md를 확인하세요.

1. 이 `codex` 폴더를 Codex 데스크톱의 새 로컬 프로젝트로 엽니다. AGENTS.md와 andrew-autoupload 폴더를 함께 두면 자연어 요청으로 스킬을 읽습니다.
2. 앱 설정 → Computer Use → Chrome의 설치 안내를 따라 확장을 연결합니다. 사용할 Chrome 프로필에서 인스타그램과 네이버에 로그인합니다.
3. Chrome 확장 프로그램 관리 → 해당 확장 세부정보 → 파일 URL에 대한 액세스 허용을 켭니다. 앱에서 `@Chrome`을 선택합니다. 이 설정은 파일 chooser 업로드에 필요할 수 있지만 Browser Use가 `file://` 페이지 방문을 허용한다는 뜻은 아닙니다. 데스크톱 화면 제어는 필요하지 않습니다.
4. “andrew-autoupload 스킬로 연결 점검만 해줘.”를 요청합니다. 로컬 테스트 페이지가 URL 정책으로 차단돼도 실제 채널 첨부 전체가 실패했다고 단정하지 않습니다. 사용자가 실제 채널 첨부를 요청하면 연결된 Chrome의 문서화된 chooser 방식으로 별도 검증합니다.
5. “andrew-autoupload 스킬로 비 오는 날 여행을 주제로 블로그와 인스타 초안을 준비해줘.”를 요청합니다. 스킬 목록 등록 없이도 AGENTS.md가 SKILL.md를 연결합니다. 자동 검색되는 스킬로 별도 등록하려면 andrew-autoupload 폴더를 프로젝트의 .agents/skills/ 안에 복사하세요.

연결된 생성 도구가 없을 때를 대비해 사용 권한이 있는 정사각형 또는 4:5 이미지 1장을 준비하세요. 생성 도구나 사용자 첨부가 반환한 원본 경로를 업로드에 우선 사용하고, 프로젝트 사본은 결과 보관용으로 유지합니다. 주소는 처음에만 질문하며 `channels.md`가 있으면 재사용합니다. 사용자가 검수하고 직접 게시합니다.

파일럿에서 확인한 범위와 호출 조건은 `VALIDATION.md`에 기록합니다. 폴더 복사만으로 Chrome 연결이나 권한이 생기지 않습니다.

재공유 시 channels.md, brand.md, inputs/, outputs/, .preflight.json과 개인 캡처를 제외하세요.

[공식 Chrome 설정](https://learn.chatgpt.com/docs/chrome-extension) · [스킬 안내](https://learn.chatgpt.com/docs/build-skills)
