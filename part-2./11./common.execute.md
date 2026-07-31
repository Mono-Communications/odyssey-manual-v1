# 11-1. common.execute (사용 메시지 종류)

```yml
execute:
  sms: true
  lms: true
  mms: true
  vms: true
  rcs: true
  kakao: true
  fetch: true
```

<table><thead><tr><th width="213">옵션</th><th>설명</th></tr></thead><tbody><tr><td><strong><code>sms</code></strong></td><td>SMS 발송 사용 여부. (true/false)</td></tr><tr><td><strong><code>lms</code></strong></td><td>LMS 발송 사용 여부. (true/false)</td></tr><tr><td><strong><code>mms</code></strong></td><td>MMS 발송 사용 여부. (true/false)</td></tr><tr><td><strong><code>vms</code></strong></td><td>VMS 발송 사용 여부. (true/false)</td></tr><tr><td><strong><code>rcs</code></strong></td><td>RCS 발송 사용 여부. (true/false)</td></tr><tr><td><strong><code>kakao</code></strong></td><td>카카오 알림톡/친구톡 발송 사용 여부. (true/false)</td></tr><tr><td><strong><code>fetch</code></strong></td><td>로그 테이블 백업(이관) 기능 사용 여부. (true/false)</td></tr></tbody></table>

{% hint style="info" %}
<mark style="color:$primary;">**언제 바꾸나요?**</mark>

사용하지 않는 메시지 종류는 `false`로 두면 불필요한 DB 폴링이 줄어 DB 부하가 낮아집니다. `fetch`(로그 이관)는 HA 운영 시 `true` 권장 — 메인 발송 테이블이 비대해지는 것을 막아줍니다.
{% endhint %}
