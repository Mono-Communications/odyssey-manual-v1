---
description: 서비스별 초당 발송 건수
---

# 12-2. fetch-count

각 서비스가 1초당 DB에서 가져와 발송할 최대 메시지 건수입니다. **각 세션의 `max-cnt` 합과 같거나 약간 크게** 설정하는 것이 원칙입니다.

```yaml
fetch-count:
      sms: 260
      lms: 300
      mms: 40
      vms: 20
      rcs: 120
      kakao: 400
      fetch: 1000
```

<table><thead><tr><th width="191.4000244140625">메시지 타입</th><th width="197.800048828125">권장 기본값</th><th>산출 근거</th></tr></thead><tbody><tr><td>sms</td><td>260</td><td>KT 크로샷 1세션 (200) + 여유</td></tr><tr><td>lms</td><td>300</td><td>KT 크로샷 1세션 (200~300)</td></tr><tr><td>mms</td><td>40</td><td>KT 크로샷 1세션 (30) + 여유</td></tr><tr><td>vms</td><td>20</td><td></td></tr><tr><td>rcs</td><td>120</td><td>KT RCS 1세션 (30) × 4</td></tr><tr><td>kakao</td><td>400</td><td>CPaaS 1세션 (20) × 20</td></tr><tr><td>fetch</td><td>1000</td><td>로그 이관 처리량</td></tr></tbody></table>
