# Codex Chrome 경로

대상: 데스크톱 로컬 세션 + 연결된 Chrome 확장. Instagram 이미지 첨부 경로는 macOS 로컬 세션에서 검증됐으며 나머지 플랫폼 파일럿은 미완료다.

1. 연결된 Chrome의 문서화된 브라우저 도구만 선택한다. 앱 설정의 Chrome 연결·프로필·사이트 권한을 확인한다. 인앱 브라우저로 바꾸지 않는다.
2. 업로드 전에 Browser Use의 `file-uploads` 문서를 읽는다. 현재 Codex Chrome 흐름은 `waitForEvent("filechooser")`와 반환된 chooser의 `setFiles(...)`를 사용한다. Claude 도구명, `file_upload`, `upload_image`, `setInputFiles` 같은 다른 런타임 API를 추측하지 않는다.
3. 이미지 생성 도구나 사용자 첨부가 반환한 **원본 파일의 절대 경로**를 먼저 사용한다. 프로젝트에 복사한 결과물은 보관용으로 유지하되 원본보다 먼저 업로드 경로로 바꾸지 않는다. 성공 경로, 형식, 크기를 `status.md`에 기록한다.
4. 로컬 `assets/upload-test.html`을 열 수 있으면 `assets/upload-test.png`로 로컬 폼을 점검한다. `file://` 방문이 Browser Use URL 정책으로 거부되면 해당 결과만 실패로 기록하고, Chrome 확장의 파일 URL 설정이 그 정책까지 해제한다고 단정하지 않는다. 사용자가 실제 채널 첨부를 요청하거나 확인했다면 실제 작성 화면 검증으로 이어갈 수 있다.
5. 실제 사이트에서는 새 게시물 영역을 연 뒤 대화상자 내부의 `input[type="file"]`을 확인한다. 프로필 사진·스토리·배너 입력과 구분하고 `accept`, `multiple`, 대화상자 범위를 확인한다.

## Instagram에서 검증된 첨부 순서

1. 지정 프로필에서 **새로운 게시물 → 게시물**을 열고 `새 게시물 만들기` 대화상자를 확인한다.
2. 대화상자 내부의 게시물 전용 `input[type="file"]`이 이미지 형식을 받는지 확인한다. 숨은 입력을 강제로 클릭했을 때 파일 선택 이벤트가 발생하지 않은 사례가 있으므로 강제 클릭을 성공 경로로 사용하지 않는다.
3. `waitForEvent("filechooser")`를 먼저 시작한다.
4. 화면에 보이는 **컴퓨터에서 선택** 버튼을 클릭한다. 이벤트를 받은 chooser에 `chooser.setFiles([원본_절대_경로])`를 호출한다. 이 흐름은 OS 파일 선택창을 직접 조작하지 않는다.
5. chooser 호출 성공만으로 끝내지 않는다. 화면이 **자르기** 단계로 바뀌고 이미지 미리보기가 실제로 렌더링됐는지 확인한다.
6. 기본 1:1 자르기로 위아래가 잘리면 비율 메뉴에서 **원본**을 선택한다. 필요한 순간에만 스크린샷으로 전체 이미지와 여백을 확인한다.
7. **다음 → 편집 → 다음**으로 캡션 화면에 도달했는지 확인한다. 문구 입력과 공개 공유 권한은 별개로 판단하고, 이 스킬은 `공유하기`를 누르지 않는다.

검증된 호출 형태:

```javascript
const chooserPromise = tab.playwright.waitForEvent("filechooser", { timeoutMs: 10000 });
await tab.playwright.getByRole("button", { name: "컴퓨터에서 선택", exact: true }).click();
const chooser = await chooserPromise;
await chooser.setFiles([originalAbsolutePath], { timeoutMs: 10000 });
```

로컬 파일 URL 페이지를 읽지 못했다고 127.0.0.1 서버나 다른 브라우저 표면으로 우회하지 않는다. 실제 채널 첨부가 허용된 작업이라면 위의 HTTPS 작성 화면과 문서화된 chooser 흐름으로 그 채널만 검증한다.

| 증상 | 조치 |
|---|---|
| 도구 미연결 | 설정 → Computer Use → Chrome 설치/연결 및 올바른 프로필 확인, @Chrome 선택 |
| 읽기만 가능 | 계획 모드, 파일 읽기 전용 권한, 사이트 조작 승인 대기를 서로 구분 |
| 특정 사이트 불가 | 사이트 차단 목록과 오류 확인, 같은 프로필의 사람 직접 접속과 비교 |
| 로컬 `file://`만 차단 | 로컬 폼 실패로 기록하고 Browser Use URL 정책과 Chrome 확장 설정을 구분 |
| chooser 대기 시간 초과 | 현재 화면과 대화상자 범위를 확인한 뒤 화면의 선택 버튼 방식으로 1회 재시도 |
| 경로 거부 | 프로젝트 사본보다 이미지 생성·사용자 첨부가 반환한 원본 절대 경로를 확인 |
| 호출 성공 후 화면 정지 | 자르기 화면·미리보기·형식 검증 결과를 확인하고 성공으로 보고하지 않음 |

위 Instagram 호출은 macOS 로컬 세션의 연결된 Chrome 확장에서 검증됐다. 다른 OS·브라우저·플랜에는 같은 결과를 확대하지 않는다. 파일 첨부 조건이 바뀌면 다시 검증한다.

[공식 연결·업로드 안내](https://learn.chatgpt.com/docs/chrome-extension)

명시적인 URL 보안 정책·권한 거부가 나온 경로 자체는 우회하지 않는다. 실제 채널의 HTTPS 작성 화면 검증은 사용자가 그 채널과 파일 첨부를 승인한 경우에만 별도 경로로 수행한다.
