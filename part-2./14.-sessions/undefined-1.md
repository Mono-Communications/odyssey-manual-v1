# 14-5. 게이트웨이 별 권장 설정

<table><thead><tr><th width="217.800048828125">메시지 종류</th><th width="214.9998779296875">사용 게이트웨이</th><th width="173">설정해야 할 세션 영역</th><th>max-cnt 기본</th></tr></thead><tbody><tr><td>SMS / LMS / MMS / VMS</td><td>KT Xroshot (직접 연동)</td><td>kt.sessions</td><td>200</td></tr><tr><td>SMS / LMS / MMS</td><td>KT CPaaS</td><td>cpaas.sessions</td><td>20</td></tr><tr><td>RCS</td><td>KT RCS Hermes</td><td>rcs.sessions</td><td>30</td></tr><tr><td>RCS</td><td>KT CPaaS</td><td>cpaas.sessions</td><td>20</td></tr><tr><td>카카오 알림톡/친구톡</td><td>엠앤와이즈</td><td>kakao.sessions</td><td>(계약값)</td></tr><tr><td>카카오 알림톡/친구톡</td><td>KT CPaaS</td><td>cpaas.sessions</td><td>20</td></tr></tbody></table>

{% hint style="warning" %}
**모든 세션의 `max-cnt`는 게이트웨이와 계약한 초당 발송 한도와 정확히 일치해야 합니다.** 처리량을 늘리려면 `max-cnt`를 키우는 것이 아니라 **세션을 추가**하거나 **계약 한도를 상향**합니다.
{% endhint %}

{% hint style="info" %}
**자주 하는 실수**

1. **`max-cnt`를 계약 한도보다 크게 설정** — 게이트웨이가 초과분을 차단하여 일정 시간 발송이 실패합니다. 계약값과 정확히 동일하게 설정하세요.
2. **`auth-file` 대소문자 불일치** — Linux 환경에서 `auth-file: test391.cert`와 실제 파일 `Test391.cert`는 다른 파일로 인식됩니다.
3. **`webhook-port` 입력 시 inbound 방화벽 미허용** — KT RCS WEBHOOK 방식 사용 시 해당 포트로 inbound 패킷이 들어와야 합니다.
4. **사용하지 않는 세션 영역을 빈 값으로 둠** — 사용하지 않는 영역은 통째로 주석 처리하거나 삭제하세요.
{% endhint %}
