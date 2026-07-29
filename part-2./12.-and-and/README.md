# 12. 테이블명 & 건수 & 주기 설정

`common.tables` 영역에서 Odyssey가 사용할 테이블명, 서비스별 초당 발송 건수, 폴링 주기를 설정합니다.

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
      rcs: 120
      kakao: 400
      fetch: 1000
    cycle:
      fetch: 1000
      db-check-interval: 30000
```
