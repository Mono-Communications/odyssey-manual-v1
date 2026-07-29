# 일반 옵션

**`shutdownhooker`** : Odyssey 관리용 포트. 동일 서버에 Odyssey를 여러 개 실행하는 경우 인스턴스마다 다른 값을 사용해야 합니다.

**`file-size`** : 업로드 이미지 파일 최대 크기. (단위: byte)

**`file-upload`** : 업로드 세션 개수.

**`ping-time`** : 세션 상태 체크 주기. (단위: 초)

**`ping-delay`** : 세션 상태 체크 응답 대기 시간. (단위: 초)

**`restart-delay`** : 세션 재시작 지연 시간. (단위: 초)

**`rcsfile-yn`** : RCS 첨부파일 사용 여부. RCS MMS 발송 시 이미지 파일 처리 활성화 여부를 결정합니다. (기본값: `false`)

**`rcs-auto-upload`** : RCS 첨부파일 자동 업로드 사용 여부. `true`이면 Odyssey가 `file-dir` 경로의 이미지를 RCS 게이트웨이에 자동 업로드합니다. (기본값: `false`)

**`auth-dir`** : 세션 인증파일(.cert) 경로.

**`file-dir`** : RCS MMS 이미지 파일 저장 경로. 절대경로 사용 시 빈 문자열로 둡니다.

**`filelist-check-interval`** : 업로드된 첨부파일 정보 캐시 유지시간. (단위: 초)

**`retry-report-interval`** : 발송 결과 재요청 주기. (단위: 밀리초)

* 발송 상태가 "전송대기" 또는 "전송중"인 메시지에 대해 결과를 재조회하는 간격.

**`otp`** : 암복호화 KEY. DB 패스워드, 세션 패스워드 등 모든 암호화 항목에 동일하게 사용됩니다.
