---
description: Odyssey가 수집한 운영 지표와 에러 정보를 모노커뮤니케이션즈 통합 관제 플랫폼 Poseidon으로 전송하도록 설정합니다.
---

# 16. Poseidon 모니터링 연동

**Poseidon**은 ㈜모노커뮤니케이션즈가 운영하는 통합 모니터링 플랫폼입니다. 고객사에 설치된 Odyssey가 `발송 성공·실패·큐 적재량, DB·JVM·CPU 상태, 에러 로그` 등의 운영 메트릭을 주기적으로 **Poseidon**으로 전송하고, 이를 수집·축적하여 AI 분석을 결합해 **장애 인지, 원인 분석, 선제 조치**에 활용합니다.



```yml
poseidon:
  enabled: true  # 연동 사용 여부
  url: http://{{MONO_IP}}:{{MONO_PORT}}/api/v1/odyssey-instances
  auth-key: {{발급받은 Auth 키}}
  contact-email: {{email}}
  heartbeat:
    interval-ms: 10000
  cypher:
    enabled: true
    coalesce-window-ms: 8000
```

<table><thead><tr><th width="216">옵션</th><th width="122">기본값</th><th>설명</th></tr></thead><tbody><tr><td><strong><code>poseidon.enabled</code></strong></td><td><mark style="color:red;"><code>true</code></mark></td><td>연동 활성화 여부 <mark style="color:red;"><code>false</code></mark>면 <mark style="color:red;"><code>url</code></mark> 설정과 무관하게 전송을 전면 중단</td></tr><tr><td><strong><code>poseidon.url</code></strong></td><td>-</td><td><p>Poseidon API 엔드포인트 URL</p><p>(MONO_IP<strong>: </strong><mark style="color:red;"><strong>4.217.193.23</strong></mark><strong> /</strong> MONO_PORT<strong>: </strong><mark style="color:red;"><strong>8181</strong></mark>)</p></td></tr><tr><td><strong><code>poseidon.auth-key</code></strong></td><td>-</td><td><strong>Poseidon</strong> 인증 키. (<mark style="color:red;">발급된 API Key</mark>)</td></tr><tr><td><strong><code>poseidon.contact-email</code></strong></td><td>-</td><td>장애 발생 시 연락받을 담당자 이메일 (고객사)</td></tr><tr><td><strong><code>heartbeat.interval-ms</code></strong></td><td><mark style="color:red;"><code>10000(10초)</code></mark></td><td>하트비트 전송 주기</td></tr><tr><td><strong><code>cypher.enabled</code></strong></td><td><mark style="color:red;"><code>true</code></mark></td><td>오류 자동 수집(내장 Cypher) 사용 여부</td></tr><tr><td><strong><code>cypher.coalesce-window-ms</code></strong></td><td><mark style="color:red;"><code>8000(8초)</code></mark></td><td>동일 오류 폭주 시 묶음 처리 윈도</td></tr></tbody></table>

{% hint style="info" %}
<mark style="color:red;">`url`</mark>, <mark style="color:red;">`auth-key`</mark> 운영 대시보드 접속 정보는 운영 환경별로 다르게 발급됩니다. 정확한 값은 별도 안내드립니다. 인증 키는 인스턴스 단위로 발급되며 재발급 시 기존 키는 폐기되므로, 설정 파일 외부로 노출되지 않도록 관리해 주십시오.
{% endhint %}

***

{% hint style="info" %}
연동을 사용하지 않는 경우 `poseidon.enabled: false` 로 설정하거나 `poseidon` 블록을 주석 처리하면 됩니다. \
이 상태에서는 Poseidon 으로의 외부 호출이 일절 발생하지 않습니다.
{% endhint %}

{% hint style="info" %}
오류 수집만 제외하고 지표 전송은 유지하려면 `poseidon.cypher.enabled: false` 로 설정하십시오. 하트비트와 메트릭 전송은 그대로 동작합니다.
{% endhint %}

{% hint style="info" %}
Poseidon 연동을 사용하는 경우 **고객사 방화벽에 Poseidon 서버 IP를 등록**해 주셔야 합니다. Odyssey가 주기적으로 외부의 Poseidon 클라우드(`poseidon.url` 항목에 명시된 호스트)로 HTTPS 요청(하트비트, 알림)을 송신해야 하므로 outbound 통신이 차단되어 있는 경우 연동이 동작하지 않습니다.  ([25-2..md](../../part-4./25.-poseidon/25-2..md "mention") 참고)
{% endhint %}
