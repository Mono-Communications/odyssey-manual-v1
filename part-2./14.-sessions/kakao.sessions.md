---
description: 앰엔 카카오 직접 연동
---

# 14-3. kakao.sessions

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

<table><thead><tr><th width="163.4000244140625">옵션</th><th>설명</th><th>권장값</th></tr></thead><tbody><tr><td>seq</td><td>세션 일련번호</td><td>1</td></tr><tr><td>send-url</td><td>엠앤와이즈 발송 API URL</td><td>https://wt-api.carrym.com:8443/v3</td></tr><tr><td>report-url</td><td>엠앤와이즈 결과 조회 API URL</td><td>https://wt-api.carrym.com:8443/v3</td></tr><tr><td>api-id</td><td>엠앤와이즈 발급 API ID</td><td>발급받은 값</td></tr><tr><td>api-key</td><td>엠앤와이즈 발급 API KEY</td><td>발급받은 값</td></tr><tr><td>sender-key</td><td>카카오 SENDER KEY</td><td>발급받은 값</td></tr><tr><td>report-cycle</td><td>리포트 조회 주기 (ms, 문자열)</td><td>'5000'</td></tr><tr><td>max-cnt</td><td>초당 발송 건수</td><td>엠앤와이즈 계약 한도와 일치</td></tr></tbody></table>
