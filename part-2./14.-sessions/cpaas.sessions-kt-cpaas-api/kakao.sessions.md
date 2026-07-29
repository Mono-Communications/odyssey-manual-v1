# kakao.sessions (엠앤와이즈 카카오 직접 연동)

`common.transmission.kakao = MN` 인 경우에 사용합니다. CPaaS 경유 카카오 발송을 사용한다면 본 영역은 비워두어도 됩니다.

```yaml
kakao:
  sessions:
    - seq: 1
      send-url: https://wt-api.carrym.com:8443/v3
      report-url: https://wt-api.carrym.com:8443/v3
      api-id: ''
      api-key: ''
      sender-key: ''
      report-cycle: '5000'
      max-cnt: 0
```

| 옵션           | 설명                  | 권장값                               |
| ------------ | ------------------- | --------------------------------- |
| seq          | 세션 일련번호             | 1                                 |
| send-url     | 엠앤와이즈 발송 API URL    | https://wt-api.carrym.com:8443/v3 |
| report-url   | 엠앤와이즈 결과 조회 API URL | https://wt-api.carrym.com:8443/v3 |
| api-id       | 엠앤와이즈 발급 API ID     | 발급받은 값                            |
| api-key      | 엠앤와이즈 발급 API KEY    | 발급받은 값                            |
| sender-key   | 카카오 SENDER KEY      | 발급받은 값                            |
| report-cycle | 리포트 조회 주기 (ms, 문자열) | '5000'                            |
| max-cnt      | 초당 발송 건수            | 엠앤와이즈 계약 한도와 일치                   |
