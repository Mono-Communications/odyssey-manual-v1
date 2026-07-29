# 10. DB 설정

`application-HA.yaml`의 `spring.datasource.hikari` 영역에서 데이터베이스 연결 정보와 운영 옵션을 설정합니다.

```yaml
spring:
  datasource:
    hikari:
      driver-class-name: com.mysql.cj.jdbc.Driver
      jdbc-url: jdbc:mysql://{{ip}}:{{port}}/{{database}}?useUnicode=true&characterEncoding=UTF-8&useSSL=false&allowPublicKeyRetrieval=true
      username: {{id}}
      password: {{pw}}
      limit: 24
      backup: FIXED
      charset: UTF-8|UTF-8
```

### 항목별 설명

| 항목                | 설명                   | 권장값                                 |
| ----------------- | -------------------- | ----------------------------------- |
| driver-class-name | JDBC 드라이버 클래스명       | com.mysql.cj.jdbc.Driver (MySQL 고정) |
| jdbc-url          | DB 접속 URL            | 운영 환경 IP/포트로 치환                     |
| username          | DB 접속 계정명            | 고객사 DB 계정                           |
| password          | DB 접속 패스워드           | 암호화 적용 권장                           |
| limit             | 메시지 발송 타임아웃 (단위: 시간) | 12 (일반 환경)                          |
| backup            | 로그 테이블 생성 방식 (대문자)   | FIXED (소규모) / MONTHLY (중·대량)        |
| charset           | 인코딩\|디코딩 설정          | UTF-8\|UTF-8                        |
