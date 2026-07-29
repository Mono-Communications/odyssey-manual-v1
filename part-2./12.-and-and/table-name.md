---
description: 자동 생성 테이블명
---

# 12-1. table-name

기본값을 그대로 사용하며, 고객사 DB에 같은 이름의 기존 테이블이 있는 경우에만 충돌 방지를 위해 변경합니다. **운영 중 변경 시 기존 발송 데이터와의 연결이 끊어지므로** 신규 환경 설치 시점에만 조정하세요.

```yaml
tables:
    table-name:
      rv-submit: ODYSSEY
      rv-submit-log: ODYSSEY_LOG
      rv-stat: ODYSSEY_STAT
      rv-file: ODYSSEY_RCSFILE
      rv-tmpl-stat: ODYSSEY_TEMPLATE_STAT
```

<table><thead><tr><th width="171.2000732421875">옵션</th><th width="286.599853515625">설명</th><th>권장값</th></tr></thead><tbody><tr><td>rv-submit</td><td>발송 테이블 (고객사 INSERT 대상)</td><td>ODYSSEY</td></tr><tr><td>rv-submit-log</td><td>발송 완료 메시지 이관 테이블</td><td>ODYSSEY_LOG</td></tr><tr><td>rv-stat</td><td>발송 통계 집계 테이블</td><td>ODYSSEY_STAT</td></tr><tr><td>rv-file</td><td>RCS 이미지 파일 테이블</td><td>ODYSSEY_RCSFILE</td></tr><tr><td>rv-tmpl-stat</td><td>템플릿별 발송 통계 테이블</td><td>ODYSSEY_TEMPLATE_STAT</td></tr></tbody></table>
