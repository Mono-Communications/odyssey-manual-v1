# 11. 사용 서비스

`common.execute` 와 `common.transmission` 영역에서 사용할 메시지 종류와 발송 경로를 설정합니다.

```yaml
common:
  execute:
    sms: true
    lms: true
    mms: true
    vms: true
    rcs: true
    kakao: true
    fetch: true
  transmission:
    msg: KT
    rcs: KT
    kakao: CPAAS
```

### common.execute (사용 메시지 종류) <a href="#commonexecute" id="commonexecute"></a>

| 옵션      | 설명                                   |
| ------- | ------------------------------------ |
| `sms`   | SMS 발송 사용 여부. (true/false)           |
| `lms`   | LMS 발송 사용 여부. (true/false)           |
| `mms`   | MMS 발송 사용 여부. (true/false)           |
| `rcs`   | RCS 발송 사용 여부. (true/false)           |
| `kakao` | 카카오 알림톡/친구톡 발송 사용 여부. (true/false)   |
| `fetch` | 로그 테이블 백업(이관) 기능 사용 여부. (true/false) |

{% hint style="info" %}
_**언제 바꾸나요?**_

사용하지 않는 메시지 종류는 `false`로 두면 불필요한 DB 폴링이 줄어 DB 부하가 낮아집니다. `fetch`(로그 이관)는 HA 운영 시 `true` 권장 — 메인 발송 테이블이 비대해지는 것을 막아줍니다.
{% endhint %}

### common.transmission (발송 경로 선택) <a href="#commontransmission" id="commontransmission"></a>

각 메시지 그룹별로 어떤 게이트웨이를 통해 발송할지 지정합니다.

**`msg`** — 문자(SMS/LMS/MMS) 발송 경로

| 값     | 의미                 |
| ----- | ------------------ |
| KT    | KT 크로샷(직접 연동)으로 발송 |
| CPAAS | CPaaS API를 통해 발송   |

**`rcs`** — RCS 발송 경로

| 값     | 의미                    |
| ----- | --------------------- |
| KT    | KT RCS Hermes API로 발송 |
| CPAAS | CPaaS API를 통해 발송      |

**`kakao`** — 카카오 알림톡/친구톡 발송 경로

| 값     | 의미               |
| ----- | ---------------- |
| MN    | 엠앤와이즈 API로 발송    |
| CPAAS | CPaaS API를 통해 발송 |

{% hint style="info" %}
계약된 발송 경로와 **반드시 일치**해야 합니다. 경로가 이중화된 경우(KT 기본, CPaaS 백업 등) 장애 시에만 수동 변경하며, 평상시에는 계약 주 경로를 유지합니다.
{% endhint %}
