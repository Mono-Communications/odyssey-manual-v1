# cpaas.sessions (KT CPaaS API)

```yaml
cpaas:
  sessions:
    - seq: 1
      send-url: https://api.communis.kt.com/cpaas/v2.0
      report-url: https://api.communis.kt.com/cpaas/v2.0
      api-id: {{communis_id}}
      api-pw: {{communis_pw}}
      sender-key: {{kakao_senderkey}}
      alimtalk-param: false
      expiry-option: 2
      agency-id: ktbizrcs
      report-cycle: 5000
      max-cnt: 20
      worker-count: 5
```

| 옵션             | 설명                               | 권장값                                        |
| -------------- | -------------------------------- | ------------------------------------------ |
| seq            | 세션 일련번호                          | 1, 2, 3 …                                  |
| send-url       | CPaaS 발송 API URL                 | 운영: https://api.communis.kt.com/cpaas/v2.0 |
| report-url     | CPaaS 결과 조회 API URL              | 운영: https://api.communis.kt.com/cpaas/v2.0 |
| api-id         | CPaaS API 사용 ID                  | 발급받은 값                                     |
| api-pw         | CPaaS API 사용 패스워드                | 암호화 적용 권장                                  |
| sender-key     | 카카오 SENDER KEY                   | 발송 테이블 K\_SENDERKEY 비어 있는 경우 fallback      |
| alimtalk-param | 카카오 알림톡 치환 문자열만 입력하는 발송 방식 사용 여부 | 일반 발송 false                                |
| expiry-option  | 메시지 결과 처리 옵션 (RCS와 동일)           | 2 (통신사 정책 시간)                              |
| agency-id      | 대행사 ID                           | ktbizrcs                                   |
| report-cycle   | 리포트 조회 주기 (단위: 밀리초)              | 5000                                       |
| max-cnt        | 초당 발송 건수                         | CPaaS 계약 한도와 일치 (기본 20)                    |
| worker-count   | 세션당 병렬 worker 슬롯 수               | 1 (기본) \~ 5 (응답 지연 시)                      |
