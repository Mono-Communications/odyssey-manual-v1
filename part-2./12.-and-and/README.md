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
      vms: 20
      rcs: 120
      kakao: 400
      fetch: 1000
    cycle:
      fetch: 1000
      db-check-interval: 30000
```



## 항목 별 설명

<table><thead><tr><th width="130.20001220703125">그룹</th><th width="136.800048828125">옵션</th><th width="242.599853515625">설명</th><th>권장값</th></tr></thead><tbody><tr><td>table-name</td><td>rv-submit</td><td>발송 테이블 (고객사 INSERT 대상)</td><td>ODYSSEY</td></tr><tr><td>table-name</td><td>rv-submit-log</td><td>발송 완료 메시지 이관 테이블</td><td>ODYSSEY_LOG</td></tr><tr><td>table-name</td><td>rv-stat</td><td>발송 통계 집계 테이블</td><td>ODYSSEY_STAT</td></tr><tr><td>table-name</td><td>rv-file</td><td>RCS 이미지 파일 테이블</td><td>ODYSSEY_RCSFILE</td></tr><tr><td>table-name</td><td>rv-tmpl-stat</td><td>템플릿별 발송 통계 테이블</td><td>ODYSSEY_TEMPLATE_STAT</td></tr><tr><td>fetch-count</td><td>sms ~ kakao</td><td>메시지 타입별 초당 발송 건수</td><td><a href="fetch-count.md">12-2. fetch-count</a> 참고</td></tr><tr><td>fetch-count</td><td>fetch</td><td>로그 이관 초당 처리 건수</td><td>1000</td></tr><tr><td>cycle</td><td>fetch</td><td>메시지 폴링 주기 (ms)</td><td>1000</td></tr><tr><td>cycle</td><td>db-check-interval</td><td>DB 연결 체크 주기 (ms)</td><td>30000</td></tr></tbody></table>

