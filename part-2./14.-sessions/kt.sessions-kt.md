---
description: KT 크로샷 직접 연동 - 문자
---

# 14-1. kt.sessions

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
      vms: true
```

<table><thead><tr><th width="172.20001220703125">옵션</th><th width="323">설명</th><th>권장값</th></tr></thead><tbody><tr><td><strong><code>seq</code></strong></td><td>세션 일련번호 (다중 세션 시 1, 2, 3 …)</td><td><mark style="color:red;"><code>1</code></mark></td></tr><tr><td><strong><code>rcs-ip</code></strong></td><td>크로샷 센터 IP:PORT</td><td><p>1센터: <mark style="color:red;"><code>rcs.xroshot.com</code></mark></p><p>2센터: <mark style="color:red;"><code>rcs2.xroshot.com</code></mark></p><p>차세대: <mark style="color:red;"><code>info.xroshot.com</code></mark></p></td></tr><tr><td><strong><code>sp-id</code></strong></td><td>크로샷 ServiceProvider 아이디</td><td>발급받은 값</td></tr><tr><td><strong><code>sp-pwd</code></strong></td><td>크로샷 패스워드</td><td>암호화 적용 권장</td></tr><tr><td><strong><code>end-user</code></strong></td><td>크로샷 EndUser ID</td><td>발급받은 값</td></tr><tr><td><strong><code>auth-file</code></strong></td><td>세션 인증파일 명 (.cert, <strong>대소문자 구분</strong>)</td><td><mark style="color:red;"><code>auth/</code></mark> 폴더 파일명과 정확히 일치</td></tr><tr><td><strong><code>max-cnt</code></strong></td><td>초당 발송 건수</td><td>KT 계약 한도와 일치 (기본 200)</td></tr><tr><td><strong><code>sms / lms / mms / vms</code></strong></td><td>해당 세션의 메시지 종류 사용 여부</td><td><mark style="color:red;"><code>true</code></mark>/ <mark style="color:red;"><code>false</code></mark></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>
