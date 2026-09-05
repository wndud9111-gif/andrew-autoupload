# 파일럿 검증 기록

상태: macOS 로컬 Claude Code + Claude in Chrome에서 로컬 폼 첨부를 검증했다. 네이버 블로그는 Claude in Chrome 경로가 확장의 도메인 차단으로 막혀 ego lite 경로에서 글쓰기 화면 진입과 제목 입력까지 확인했다. 본문 입력·이미지 첨부·임시저장·공개 발행, 인스타그램 첨부·캡션은 실행하지 않았다. 아래 미확인 항목은 지원을 뜻하지 않는다. (기록일 2026-09-05)

| 항목 | 실제 기록 |
|---|---|
| OS·버전 | macOS, Darwin 25.5.0 로컬 세션 |
| 계정 플랜 | 미확인 |
| 앱·확장 버전 | 미확인. Claude in Chrome 확장은 연결 상태만 확인했고 버전은 조회하지 않음 |
| 브라우저·도구명·호출 인수 | Chrome 경로: claude-in-chrome MCP. `list_connected_browsers` → `select_browser(deviceId)` → `find`로 `input[type=file]` ref 확보 → `file_upload(tabId, ref, paths)`. ego lite 경로: `ego-browser nodejs` heredoc의 `useOrCreateTaskSpace` / `openOrReuseTab` / `click` / `typeText` / `js` |
| 파일 접근 경로·용량 조건 | 스킬 `assets/upload-test.png`(1,017바이트, 320×320) 첨부 성공. 10MB 한도와 하드링크 조건은 작은 파일 1개만 시험해 미검증 |
| 로컬 폼 첨부·텍스트 입력 | `file://` 은 `navigate`가 `https://file://` 로 재작성해 사용 불가. `assets` 폴더만 `127.0.0.1:8731`에 제공한 임시 서버의 `upload-test.html`에서 첨부 성공, 페이지가 파일명·바이트·해상도를 표시하는 것까지 확인. 폼의 텍스트 입력 필드는 시험하지 않음 |
| OS 파일 선택창 미사용 | 준수. 선택창 버튼을 누르지 않고 `find`로 얻은 ref에 직접 파일을 연결함 |
| 네이버 본문 구조·첨부·임시저장 | Chrome 경로: `navigate`가 실행 전 거부됨 — "This site is not allowed due to safety restrictions." 같은 머신에서 curl 직접 요청은 HTTP 200(60ms)이라 네이버측 IP 차단이 아님을 확인. ego lite 경로: 글쓰기 화면 진입, 스마트에디터가 iframe이 아닌 메인 문서에 있음을 확인, 유일한 `contenteditable`이 화면 밖(x=-9999) 입력 버퍼임을 확인, 제목에 write probe를 넣어 실제 제목 필드에 반영되는 것까지 확인. 본문 입력·이미지 첨부·임시저장은 미실행 |
| 인스타그램 첨부·캡션·잘림 확인 | 계정 페이지에서 "프로필 편집" 노출로 로그인 계정 일치만 확인. 이미지 미제공으로 작성 화면 미진입, 첨부·캡션·비율 확인 모두 미실행 |
| 화면 보존·중단 후 재개 | 미실행 |
| 최종 공개 발행 미실행 | 준수. 네이버 임시저장과 발행, 인스타그램 공유 모두 누르지 않음 |

로컬 폼과 실제 플랫폼 검증은 서로 다른 결과로 취급한다. 로컬 폼 첨부 성공은 네이버·인스타그램 첨부 성공을 뜻하지 않는다. Chrome 경로의 네이버 차단은 확장의 서버측 URL 분류로 관측된 것이며 원인은 공개 자료로 확인되지 않았다. 개인 계정 정보 없이 성공한 범위만 기록하고, 다른 OS·플랜으로 확대하지 않는다. Windows는 미검증이며 ego lite 설치 스크립트가 macOS 전용이라 네이버 경로가 없다.
