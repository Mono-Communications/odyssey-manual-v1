# rcs.sessions (KT RCS Hermes API)

```yaml
rcs:
  sessions:
    - seq: 1
      send-url: https://agency.hermes.kt.com/corp/v1
      report-url: https://query.hermes.kt.com/corp/v1
      rcs-stat-url: https://api.rcsbizcenter.com/api/1.1
      rcs-stat-id: {{stat_id}}
      rcs-stat-secret: {{stat_secret}}
      rcs-id: {{rcs_id}}
      rcs-secret: {{rcs_pw}}
      webhook-port: ''
      agencyid: ktbizrcs
      expiry-option: 2
      report-cycle: 5000
      max-cnt: 30
```

| 옵션              | 설명                             | 권장값                                                                                     |
| --------------- | ------------------------------ | --------------------------------------------------------------------------------------- |
| seq             | 세션 일련번호                        | 1, 2, 3 …                                                                               |
| send-url        | 메시지 발송 API URL                 | 운영: https://agency.hermes.kt.com/corp/v1 / 개발: https://agency-stg.hermes.kt.com/corp/v1 |
| report-url      | 메시지 리포트 API URL                | 운영: https://query.hermes.kt.com/corp/v1 / 개발: https://query-stg.hermes.kt.com/corp/v1   |
| rcs-stat-url    | RCS 고객반응 통계 API URL            | rcs-stat-info=true 인 경우만 입력                                                             |
| rcs-stat-id     | RCS Biz Center 가입 ID           | rcs-stat-info=true 인 경우만 입력                                                             |
| rcs-stat-secret | RCS Biz Center API KEY (자동 생성) | rcs-stat-info=true 인 경우만 입력                                                             |
| rcs-id          | KT RCS 청약 ID                   | 발급받은 값                                                                                  |
| rcs-secret      | KT RCS SECRET 키                | 암호화 적용 권장                                                                               |
| webhook-port    | 리포트 수신 방식                      | 아래 webhook-port 설명 참고                                                                   |
| agencyid        | 대행사 ID                         | 운영: ktbizrcs / 개발: ktrcsdev                                                             |
| expiry-option   | 메시지 결과 처리 옵션                   | 2 (통신사 정책시간)                                                                            |
| report-cycle    | API 방식 리포트 조회 주기 (ms)          | 5000                                                                                    |
| max-cnt         | 초당 발송 건수                       | KT RCS 계약 한도와 일치 (기본 30)                                                                |

#### `webhook-port` — 리포트 수신 방식

| 값              | 방식      | 동작                                       |
| -------------- | ------- | ---------------------------------------- |
| 포트번호 (예: 8443) | WEBHOOK | KT가 해당 포트로 리포트를 push (inbound 방화벽 허용 필요) |
| 빈 문자열 ('')     | API     | Odyssey가 report-cycle 주기로 결과를 pull       |

#### `expiry-option` — 결과 WEBHOOK 유효 시간

| 값 | 의미                                        |
| - | ----------------------------------------- |
| 1 | 최대 3일까지 결과 WEBHOOK 전송                     |
| 2 | 통신사 정책 시간까지 결과 WEBHOOK 전송 (10초 \~ 3분, 권장) |
