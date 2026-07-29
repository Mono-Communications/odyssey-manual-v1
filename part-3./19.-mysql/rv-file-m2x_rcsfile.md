# rv-file (M2X\_RCSFILE) 테이블

| 컬럼명          | 데이터 타입                     | NN                     | 기본값                 | 설명 |
| ------------ | -------------------------- | ---------------------- | ------------------- | -- |
| ID           | BIGINT(20) AUTO\_INCREMENT | Y                      | 첨부파일 유니크 번호 (PK)    |    |
| FILE\_PATH   | VARCHAR(200)               | Y                      | 발송테이블에 사용된 파일 경로    |    |
| DESCRIPTION  | VARCHAR(500)               | 파일 최종 수정 정보 (동명 파일 대비) |                     |    |
| STATUS       | SMALLINT                   | 0                      | 0=대기, 2=치환 가능, 3=실패 |    |
| FILEID       | VARCHAR(64)                | 자동 업로드된 파일 ID          |                     |    |
| SUBMIT\_TIME | VARCHAR(16)                | Y                      | 등록 시각               |    |
| UPLOAD\_TIME | VARCHAR(16)                | 업로드 시각                 |                     |    |
| EXPIRY\_TIME | VARCHAR(16)                | 만료 시각                  |                     |    |
| RESULT       | INT(6)                     | -2                     | 업로드 결과값             |    |
| RESULT\_DESC | VARCHAR(1000)              | 결과값 상세                 |                     |    |
| RCS\_ID      | VARCHAR(20)                | 발송 세션 RCS\_ID          |                     |    |
