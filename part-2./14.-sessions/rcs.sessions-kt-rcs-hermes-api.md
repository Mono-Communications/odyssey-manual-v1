---
description: KT RCS 직접 연동
---

# 14-2. rcs.sessions

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

<table><thead><tr><th width="141">옵션</th><th width="258">설명</th><th>권장값</th></tr></thead><tbody><tr><td><strong><code>seq</code></strong></td><td>세션 일련번호</td><td>1, 2, 3 …</td></tr><tr><td><strong><code>send-url</code></strong></td><td>메시지 발송 API URL</td><td><p>운영: <mark style="color:red;"><code>https://agency.hermes.kt.com/corp/v1</code></mark></p><p>개발: <mark style="color:red;"><code>https://agency-stg.hermes.kt.com/corp/v1</code></mark></p></td></tr><tr><td><strong><code>report-url</code></strong></td><td>메시지 리포트 API URL</td><td><p>운영: <mark style="color:red;"><code>https://query.hermes.kt.com/corp/v1</code></mark></p><p>개발: <mark style="color:red;"><code>https://query-stg.hermes.kt.com/corp/v1</code></mark></p></td></tr><tr><td><strong><code>rcs-stat-url</code></strong></td><td>RCS 고객반응 통계 API URL</td><td><mark style="color:red;"><code>rcs-stat-info=true</code></mark> 인 경우만 입력</td></tr><tr><td><strong><code>rcs-stat-id</code></strong></td><td>RCS Biz Center 가입 ID</td><td><mark style="color:red;"><code>rcs-stat-info=true</code></mark> 인 경우만 입력</td></tr><tr><td><strong><code>rcs-stat-secret</code></strong></td><td>RCS Biz Center API KEY (자동 생성)</td><td><mark style="color:red;"><code>rcs-stat-info=true</code></mark> 인 경우만 입력</td></tr><tr><td><strong><code>rcs-id</code></strong></td><td>KT RCS 청약 ID</td><td>발급받은 값</td></tr><tr><td><strong><code>rcs-secret</code></strong></td><td>KT RCS SECRET 키</td><td>암호화 적용 권장</td></tr><tr><td><strong><code>webhook-port</code></strong></td><td>리포트 수신 방식</td><td>아래 webhook-port 설명 참고</td></tr><tr><td><strong><code>agencyid</code></strong></td><td>대행사 ID</td><td>운영: <mark style="color:red;"><code>ktbizrcs</code></mark> / 개발: <mark style="color:red;"><code>ktrcsdev</code></mark></td></tr><tr><td><strong><code>expiry-option</code></strong></td><td>메시지 결과 처리 옵션</td><td><mark style="color:red;"><code>2</code></mark> (통신사 정책시간)</td></tr><tr><td><strong><code>report-cycle</code></strong></td><td>API 방식 리포트 조회 주기 (ms)</td><td><mark style="color:red;"><code>5000</code></mark></td></tr><tr><td><strong><code>max-cnt</code></strong></td><td>초당 발송 건수</td><td>KT RCS 계약 한도와 일치 (기본 <mark style="color:red;"><code>30</code></mark>)</td></tr></tbody></table>

#### **`webhook-port`** — 리포트 수신 방식

<table><thead><tr><th width="174.60003662109375">값</th><th width="115.99993896484375">방식</th><th>동작</th></tr></thead><tbody><tr><td>포트번호 (예: <strong><code>8443</code></strong>)</td><td>WEBHOOK</td><td>KT가 해당 포트로 리포트를 push (inbound 방화벽 허용 필요)</td></tr><tr><td>빈 문자열 (<strong><code>''</code></strong>)</td><td>API</td><td>Odyssey가 <mark style="color:red;"><code>report-cycle</code></mark> 주기로 결과를 pull</td></tr></tbody></table>

#### **`expiry-option`** — 결과 WEBHOOK 유효 시간

<table><thead><tr><th width="135.60003662109375">값</th><th>의미</th></tr></thead><tbody><tr><td><strong><code>1</code></strong></td><td>최대 3일까지 결과 WEBHOOK 전송</td></tr><tr><td><strong><code>2</code></strong></td><td>통신사 정책 시간까지 결과 WEBHOOK 전송 (10초 ~ 3분, 권장)</td></tr></tbody></table>
