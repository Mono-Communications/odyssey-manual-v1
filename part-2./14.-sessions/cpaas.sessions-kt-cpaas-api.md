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

<table><thead><tr><th width="159.4000244140625">옵션</th><th width="294.7999267578125">설명</th><th>권장값</th></tr></thead><tbody><tr><td>seq</td><td>세션 일련번호</td><td>1, 2, 3 …</td></tr><tr><td>send-url</td><td>CPaaS 발송 API URL</td><td>운영: https://api.communis.kt.com/cpaas/v2.0</td></tr><tr><td>report-url</td><td>CPaaS 결과 조회 API URL</td><td>운영: https://api.communis.kt.com/cpaas/v2.0</td></tr><tr><td>api-id</td><td>CPaaS API 사용 ID</td><td>발급받은 값</td></tr><tr><td>api-pw</td><td>CPaaS API 사용 패스워드</td><td>암호화 적용 권장</td></tr><tr><td>sender-key</td><td>카카오 SENDER KEY</td><td>발송 테이블 K_SENDERKEY 비어 있는 경우 fallback</td></tr><tr><td>alimtalk-param</td><td>카카오 알림톡 치환 문자열만 입력하는 발송 방식 사용 여부</td><td>일반 발송 false</td></tr><tr><td>expiry-option</td><td>메시지 결과 처리 옵션 (RCS와 동일)</td><td>2 (통신사 정책 시간)</td></tr><tr><td>agency-id</td><td>대행사 ID</td><td>ktbizrcs</td></tr><tr><td>report-cycle</td><td>리포트 조회 주기 (단위: 밀리초)</td><td>5000</td></tr><tr><td>max-cnt</td><td>초당 발송 건수</td><td>CPaaS 계약 한도와 일치 (기본 20)</td></tr><tr><td>worker-count</td><td>세션당 병렬 worker 슬롯 수</td><td>1 (기본) ~ 5 (응답 지연 시)</td></tr></tbody></table>
