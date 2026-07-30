# 12. 테이블명 & 건수 & 주기 설정

<mark style="color:red;">`common.tables`</mark> 영역에서 Odyssey가 사용할 테이블명, 서비스별 초당 발송 건수, 폴링 주기를 설정합니다.

```yaml
common:
  tables:
    table-name:
      rv-submit: ODYSSEY
      rv-submit-log: ODYSSEY_LOG
      rv-stat: ODYSSEY_STAT
      rv-file: ODYSSEY_RCSFILE
      rv-tmpl-stat: ODYSSEY_TEMPLATE_STAT
    fetch-count:
      sms: 260
      lms: 300
      mms: 40
      vms: 20
      rcs: 120
      kakao: 400
      fetch: 1000
    cycle:
      fetch: 1000
      db-check-interval: 30000
```

## <mark style="color:blue;">항목 별 설명</mark>

***

<table><thead><tr><th width="130.20001220703125">그룹</th><th width="136.800048828125">옵션</th><th width="242.599853515625">설명</th><th>권장값</th></tr></thead><tbody><tr><td><strong><code>table-name</code></strong></td><td><strong><code>rv-submit</code></strong></td><td>발송 테이블 (고객사 INSERT 대상)</td><td><mark style="color:red;"><strong><code>ODYSSEY</code></strong></mark></td></tr><tr><td><strong><code>table-name</code></strong></td><td><strong><code>rv-submit-log</code></strong></td><td>발송 완료 메시지 이관 테이블</td><td><mark style="color:red;"><strong><code>ODYSSEY_LOG</code></strong></mark></td></tr><tr><td><strong><code>table-name</code></strong></td><td><strong><code>rv-stat</code></strong></td><td>발송 통계 집계 테이블</td><td><mark style="color:red;"><strong><code>ODYSSEY_STAT</code></strong></mark></td></tr><tr><td><strong><code>table-name</code></strong></td><td><strong><code>rv-file</code></strong></td><td>RCS 이미지 파일 테이블</td><td><mark style="color:red;"><strong><code>ODYSSEY_RCSFILE</code></strong></mark></td></tr><tr><td><strong><code>table-name</code></strong></td><td><strong><code>rv-tmpl-stat</code></strong></td><td>템플릿별 발송 통계 테이블</td><td><mark style="color:red;"><strong><code>ODYSSEY_TEMPLATE_STAT</code></strong></mark></td></tr><tr><td><strong><code>fetch-count</code></strong></td><td><strong><code>sms ~ kakao</code></strong></td><td>메시지 타입별 초당 발송 건수</td><td><a href="fetch-count.md">12-2. fetch-count</a> 참고</td></tr><tr><td><strong><code>fetch-count</code></strong></td><td><strong><code>fetch</code></strong></td><td>로그 이관 초당 처리 건수</td><td><mark style="color:red;"><strong><code>1000</code></strong></mark></td></tr><tr><td><strong><code>cycle0</code></strong></td><td><strong><code>fetch</code></strong></td><td>메시지 폴링 주기 (ms)</td><td><mark style="color:red;"><strong><code>1000</code></strong></mark></td></tr><tr><td><strong><code>cycle</code></strong></td><td><strong><code>db-check-interval</code></strong></td><td>DB 연결 체크 주기 (ms)</td><td><mark style="color:red;"><strong><code>30000</code></strong></mark></td></tr></tbody></table>

**참고:** 위 테이블 5종 + `ha_lease`, `PAUSE_INFO` 테이블은 Odyssey 최초 기동 시 자동 생성됩니다. 운영 환경에서는 미리 DB CREATE/INSERT/SELECT 권한을 부여해 두시기 바랍니다.

{% hint style="info" %}
위 테이블 5종 + <mark style="color:red;">`ha_lease`</mark>, <mark style="color:red;">`PAUSE_INFO`</mark> 테이블은 Odyssey 최초 기동 시 자동 생성됩니다. 운영 환경에서는 미리 DB CREATE/INSERT/SELECT 권한을 부여해 두시기 바랍니다.
{% endhint %}



### <mark style="color:blue;">table-name</mark> - 자동 생성 테이블명

***

기본값을 그대로 사용하며, 고객사 DB에 같은 이름의 기존 테이블이 있는 경우에만 충돌 방지를 위해 변경합니다. 운영 중 변경 시 기존 발송 데이터와의 연결이 끊어지므로 신규 환경 설치 시점에만 조정하세요.



### <mark style="color:blue;">**fetch-count**</mark>**&#x20;- 서비스별 초당 발송 건수**



