---
description: 엠앤와이즈 카카오 직접 연동
---

# 14-3. kakao.sessions

<mark style="color:green;">`common.transmission.kakao = MN`</mark> 인 경우에 사용합니다. CPaaS 경유 카카오 발송을 사용한다면 본 영역은 비워두어도 됩니다.

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

<table><thead><tr><th width="163.4000244140625">옵션</th><th>설명</th><th>권장값</th></tr></thead><tbody><tr><td><strong><code>seq</code></strong></td><td>세션 일련번호</td><td><mark style="color:red;"><code>1</code></mark></td></tr><tr><td><strong><code>send-url</code></strong></td><td>엠앤와이즈 발송 API URL</td><td><mark style="color:red;"><code>https://wt-api.carrym.com:8443/v3</code></mark></td></tr><tr><td><strong><code>report-url</code></strong></td><td>엠앤와이즈 결과 조회 API URL</td><td><mark style="color:red;"><code>https://wt-api.carrym.com:8443/v3</code></mark></td></tr><tr><td><strong><code>api-id</code></strong></td><td>엠앤와이즈 발급 API ID</td><td>발급받은 값</td></tr><tr><td><strong><code>api-key</code></strong></td><td>엠앤와이즈 발급 API KEY</td><td>발급받은 값</td></tr><tr><td><strong><code>sender-key</code></strong></td><td>카카오 SENDER KEY</td><td>발급받은 값</td></tr><tr><td><strong><code>report-cycle</code></strong></td><td>리포트 조회 주기 (ms, 문자열)</td><td><mark style="color:red;"><code>'5000'</code></mark></td></tr><tr><td><strong><code>max-cnt</code></strong></td><td>초당 발송 건수</td><td>엠앤와이즈 계약 한도와 일치</td></tr></tbody></table>
