---
description: KT CPaaS API
---

# 14-4. cpaas.sessions

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

<table><thead><tr><th width="159.4000244140625">옵션</th><th width="294.7999267578125">설명</th><th>권장값</th></tr></thead><tbody><tr><td><strong><code>seq</code></strong></td><td>세션 일련번호</td><td>1, 2, 3 …</td></tr><tr><td><strong><code>send-url</code></strong></td><td>CPaaS 발송 API URL</td><td>운영: <mark style="color:red;"><code>https://api.communis.kt.com/cpaas/v2.0</code></mark></td></tr><tr><td><strong><code>report-url</code></strong></td><td>CPaaS 결과 조회 API URL</td><td>운영: <mark style="color:red;"><code>https://api.communis.kt.com/cpaas/v2.0</code></mark></td></tr><tr><td><strong><code>api-id</code></strong></td><td>CPaaS API 사용 ID</td><td>발급받은 값</td></tr><tr><td><strong><code>api-pw</code></strong></td><td>CPaaS API 사용 패스워드</td><td>암호화 적용 권장</td></tr><tr><td><strong><code>sender-key</code></strong></td><td>카카오 SENDER KEY</td><td>발송 테이블 <mark style="color:red;"><code>K_SENDERKEY</code></mark> 비어 있는 경우 fallback</td></tr><tr><td><strong><code>alimtalk-param</code></strong></td><td>카카오 알림톡 치환 문자열만 입력하는 발송 방식 사용 여부</td><td>일반 발송 <mark style="color:red;"><code>false</code></mark> (<a data-mention href="../../part-3./17.-insert/">17.-insert</a> 참고)</td></tr><tr><td><strong><code>expiry-option</code></strong></td><td>메시지 결과 처리 옵션 (RCS와 동일)</td><td><mark style="color:red;"><code>2</code></mark> (통신사 정책 시간)</td></tr><tr><td><strong><code>agency-id</code></strong></td><td>대행사 ID</td><td><mark style="color:red;"><code>ktbizrcs</code></mark></td></tr><tr><td><strong><code>report-cycle</code></strong></td><td>리포트 조회 주기 (단위: 밀리초)</td><td><mark style="color:red;"><code>5000</code></mark></td></tr><tr><td><strong><code>max-cnt</code></strong></td><td>초당 발송 건수</td><td>CPaaS 계약 한도와 일치 (기본 <mark style="color:red;"><code>20</code></mark>)</td></tr><tr><td><strong><code>worker-count</code></strong></td><td>세션당 병렬 worker 슬롯 수</td><td><mark style="color:red;"><code>1</code></mark> (기본) ~ <mark style="color:red;"><code>5</code></mark> (응답 지연 시)</td></tr></tbody></table>
