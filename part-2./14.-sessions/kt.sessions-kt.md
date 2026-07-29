# kt.sessions (KT 크로샷 직접 연동 - 문자)

```yaml
kt:
  socket:
    runtime: netty # 소켓 런타임 (netty 권장)
  sessions:
    - seq: 1
      rcs-ip: rcs.xroshot.com
      sp-id: {{xroshot_id}}
      sp-pwd: {{xroshot_pw}}
      end-user: {{user}}
      auth-file: {{auth_file_name}}
      max-cnt: 200
      sms: true
      lms: true
      mms: true
```

| 옵션              | 설명                             | 권장값                                                                  |
| --------------- | ------------------------------ | -------------------------------------------------------------------- |
| seq             | 세션 일련번호 (다중 세션 시 1, 2, 3 …)    | 1                                                                    |
| rcs-ip          | 크로샷 센터 IP:PORT                 | 1센터: rcs.xroshot.com / 2센터: rcs2.xroshot.com / 차세대: info.xroshot.com |
| sp-id           | 크로샷 ServiceProvider 아이디        | 발급받은 값                                                               |
| sp-pwd          | 크로샷 패스워드                       | 암호화 적용 권장                                                            |
| end-user        | 크로샷 EndUser ID                 | 발급받은 값                                                               |
| auth-file       | 세션 인증파일 명 (.cert, **대소문자 구분**) | auth/ 폴더 파일명과 정확히 일치                                                 |
| max-cnt         | 초당 발송 건수                       | KT 계약 한도와 일치 (기본 200)                                                |
| sms / lms / mms | 해당 세션의 메시지 종류 사용 여부            | true / false                                                         |
