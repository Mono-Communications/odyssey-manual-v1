# 19. 테이블 레이아웃 (MySQL)

Odyssey 최초 기동 시 `common.tables.table-name` 에 지정된 이름으로 테이블이 자동 생성됩니다. 아래는 발송 테이블(`rv-submit`, 기본 `ODYSSEY`)의 컬럼 레이아웃입니다.

| 컬럼명                | 데이터 타입                     | NN                             | 기본값                          | 설명                   |
| ------------------ | -------------------------- | ------------------------------ | ---------------------------- | -------------------- |
| MSG\_ID            | BIGINT(20) AUTO\_INCREMENT | Y                              | 메시지당 유니크한 번호 (PK)            |                      |
| LB\_ID             | BIGINT(20)                 | Y                              | 0                            | 로드밸런싱 ID (HA 분산 처리용) |
| SUBJECT            | VARCHAR(40)                | 메시지 제목                         |                              |                      |
| MSG\_TYPE          | TINYINT(2)                 | Y                              | 1차 메시지 구분 (아래 코드 표 참고)       |                      |
| MSG\_TYPE\_SECOND  | TINYINT(2)                 | Y                              | 0                            | 2차 메시지 구분 (FALLBACK) |
| MSG\_TYPE\_THIRD   | TINYINT(2)                 | Y                              | 0                            | 3차 메시지 구분 (FALLBACK) |
| STATUS             | SMALLINT                   | 0                              | 메시지 상태 (아래 표 참고)             |                      |
| SCHEDULE\_TIME     | VARCHAR(16)                | Y                              | 발송 시작 시각 (YYYYMMDDHH24MISS)  |                      |
| SUBMIT\_TIME       | VARCHAR(16)                | Y                              | 메시지 등록 시각 (YYYYMMDDHH24MISS) |                      |
| MESSAGE            | TEXT                       | 메시지 내용                         |                              |                      |
| CALLBACK\_NUM      | VARCHAR(20)                | Y                              | 회신번호 (특수문자 제외)               |                      |
| RCPT\_DATA         | VARCHAR(20)                | Y                              | 수신번호 (특수문자 제외)               |                      |
| FILE\_COUNT        | TINYINT(1)                 | 0                              | MMS 첨부 파일 개수                 |                      |
| FILE\_NAME1        | VARCHAR(128)               | MMS 첨부 파일 1                    |                              |                      |
| FILE\_NAME2        | VARCHAR(128)               | MMS 첨부 파일 2                    |                              |                      |
| FILE\_NAME3        | VARCHAR(128)               | MMS 첨부 파일 3                    |                              |                      |
| HEADER             | TINYINT(1)                 | CPAAS HEADER (광고 표기)           |                              |                      |
| FOOTER             | VARCHAR(20)                | CPAAS FOOTER (수신거부 번호)         |                              |                      |
| CDR\_ID            | VARCHAR(20)                | 과금 ID                          |                              |                      |
| RESULT             | MEDIUMINT(6)               | 전송 결과 코드 (SMS/LMS/MMS)         |                              |                      |
| RCS\_RESULT        | MEDIUMINT(6)               | 전송 결과 코드 (RCS)                 |                              |                      |
| KKO\_RESULT        | MEDIUMINT(6)               | 전송 결과 코드 (KAKAO)               |                              |                      |
| RESULT\_DESC       | VARCHAR(200)               | 결과코드 상세 내용                     |                              |                      |
| DELIVER\_TIME      | VARCHAR(16)                | 전송 시각 (마지막 발송)                 |                              |                      |
| REPORT\_RECV\_TIME | VARCHAR(16)                | 리포트 수신 시각                      |                              |                      |
| TELCOINFO          | VARCHAR(4)                 | 수신자 이통사 정보                     |                              |                      |
| FAIL\_SEND         | VARCHAR(1)                 | 'N'                            | 실패 재발송(FALLBACK) 여부 (Y/N)    |                      |
| K\_TMPLCODE        | VARCHAR(30)                | 알림톡 템플릿 코드                     |                              |                      |
| K\_MESSAGE         | TEXT                       | 알림톡 메시지 내용                     |                              |                      |
| K\_OPTION          | TEXT                       | 알림톡 button(JSON)               |                              |                      |
| K\_SERIAL\_NM      | VARCHAR(40)                | 알림톡 시리얼명                       |                              |                      |
| K\_ADFLAG          | VARCHAR(1)                 | 'N'                            | 알림톡 광고 문구 여부 (Y/N)           |                      |
| K\_SENDERKEY       | VARCHAR(40)                | 알림톡 발신 프로필 키                   |                              |                      |
| R\_MESSAGEBASEID   | VARCHAR(40)                | RCS messageBaseId              |                              |                      |
| R\_BODY            | TEXT                       | RCS body (JSON)                |                              |                      |
| R\_BUTTON          | TEXT                       | RCS button (JSON)              |                              |                      |
| R\_HEADER          | TINYINT(1)                 | RCS 광고 문구 여부 (0/1)             |                              |                      |
| R\_FOOTER          | VARCHAR(20)                | RCS 수신거부 번호 (R\_HEADER=1 시 필수) |                              |                      |
| R\_COPYALLOWED     | VARCHAR(1)                 | 'N'                            | RCS 메시지 복사 허용 여부 (Y/N)       |                      |
| R\_QUERYID         | VARCHAR(60)                | RCS 리포트 요청 queryId             |                              |                      |
| RESERVED01         | VARCHAR(60)                | 예약 필드 1                        |                              |                      |
| RESERVED02         | VARCHAR(60)                | 예약 필드 2                        |                              |                      |
| RESERVED03         | VARCHAR(60)                | 예약 필드 3                        |                              |                      |
| KISA\_ORIG\_CODE   | VARCHAR(9)                 | KISA 코드                        |                              |                      |
| R\_AGENCYID        | VARCHAR(60)                | RCS agencyId                   |                              |                      |
| R\_AGENCYKEY       | VARCHAR(256)               | RCS agencyKey                  |                              |                      |
| R\_BRANDKEY        | VARCHAR(256)               | RCS brandKey                   |                              |                      |
| R\_CDR\_ID         | VARCHAR(20)                | RCS 과금 ID                      |                              |                      |
| TRACKING\_ID       | VARCHAR(40)                | 리포트 요청 TRACKING ID             |                              |                      |
| TOKEN              | VARCHAR(100)               | 리포트 요청 TOKEN                   |                              |                      |
| C\_STATUS          | VARCHAR(1)                 | CPaaS 전송 결과 STATUS             |                              |                      |
| SUB\_KEY           | VARCHAR(100)               | CPAAS 부서/과금 분리 코드              |                              |                      |
