---
description: KT RCS Hermes API
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

<table><thead><tr><th width="141">옵션</th><th width="295">설명</th><th>권장값</th></tr></thead><tbody><tr><td>seq</td><td>세션 일련번호</td><td>1, 2, 3 …</td></tr><tr><td>send-url</td><td>메시지 발송 API URL</td><td><p>운영: https://agency.hermes.kt.com/corp/v1</p><p>개발: https://agency-stg.hermes.kt.com/corp/v1</p></td></tr><tr><td>report-url</td><td>메시지 리포트 API URL</td><td><p>운영: https://query.hermes.kt.com/corp/v1</p><p>개발: https://query-stg.hermes.kt.com/corp/v1</p></td></tr><tr><td>rcs-stat-url</td><td>RCS 고객반응 통계 API URL</td><td>rcs-stat-info=true 인 경우만 입력</td></tr><tr><td>rcs-stat-id</td><td>RCS Biz Center 가입 ID</td><td>rcs-stat-info=true 인 경우만 입력</td></tr><tr><td>rcs-stat-secret</td><td>RCS Biz Center API KEY (자동 생성)</td><td>rcs-stat-info=true 인 경우만 입력</td></tr><tr><td>rcs-id</td><td>KT RCS 청약 ID</td><td>발급받은 값</td></tr><tr><td>rcs-secret</td><td>KT RCS SECRET 키</td><td>암호화 적용 권장</td></tr><tr><td>webhook-port</td><td>리포트 수신 방식</td><td>아래 webhook-port 설명 참고</td></tr><tr><td>agencyid</td><td>대행사 ID</td><td>운영: ktbizrcs / 개발: ktrcsdev</td></tr><tr><td>expiry-option</td><td>메시지 결과 처리 옵션</td><td>2 (통신사 정책시간)</td></tr><tr><td>report-cycle</td><td>API 방식 리포트 조회 주기 (ms)</td><td>5000</td></tr><tr><td>max-cnt</td><td>초당 발송 건수</td><td>KT RCS 계약 한도와 일치 (기본 30)</td></tr></tbody></table>

#### `webhook-port` — 리포트 수신 방식

<table><thead><tr><th width="174.60003662109375">값</th><th width="115.99993896484375">방식</th><th>동작</th></tr></thead><tbody><tr><td>포트번호 (예: 8443)</td><td>WEBHOOK</td><td>KT가 해당 포트로 리포트를 push (inbound 방화벽 허용 필요)</td></tr><tr><td>빈 문자열 ('')</td><td>API</td><td>Odyssey가 report-cycle 주기로 결과를 pull</td></tr></tbody></table>

#### `expiry-option` — 결과 WEBHOOK 유효 시간

<table><thead><tr><th width="135.60003662109375">값</th><th>의미</th></tr></thead><tbody><tr><td>1</td><td>최대 3일까지 결과 WEBHOOK 전송</td></tr><tr><td>2</td><td>통신사 정책 시간까지 결과 WEBHOOK 전송 (10초 ~ 3분, 권장)</td></tr></tbody></table>
