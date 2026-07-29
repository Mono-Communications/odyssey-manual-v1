# 항목별 설명

| 그룹          | 옵션                | 설명                     | 권장값                     |
| ----------- | ----------------- | ---------------------- | ----------------------- |
| table-name  | rv-submit         | 발송 테이블 (고객사 INSERT 대상) | ODYSSEY                 |
| table-name  | rv-submit-log     | 발송 완료 메시지 이관 테이블       | ODYSSEY\_LOG            |
| table-name  | rv-stat           | 발송 통계 집계 테이블           | ODYSSEY\_STAT           |
| table-name  | rv-file           | RCS 이미지 파일 테이블         | ODYSSEY\_RCSFILE        |
| table-name  | rv-tmpl-stat      | 템플릿별 발송 통계 테이블         | ODYSSEY\_TEMPLATE\_STAT |
| fetch-count | sms \~ kakao      | 메시지 타입별 초당 발송 건수       | 아래 fetch-count 표 참고     |
| fetch-count | fetch             | 로그 이관 초당 처리 건수         | 1000                    |
| cycle       | fetch             | 메시지 폴링 주기 (ms)         | 1000                    |
| cycle       | db-check-interval | DB 연결 체크 주기 (ms)       | 30000                   |
