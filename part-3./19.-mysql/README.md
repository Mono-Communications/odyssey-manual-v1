# 19. 테이블 레이아웃

{% hint style="info" %}
컬럼의 데이터 타입은 DBMS 에 따라 다릅니다. DBMS 별 데이터 타입은 표 아래의 [DBMS 별 테이블 생성문](#create-table) 에서 확인하세요.
{% endhint %}

Odyssey 최초 기동 시 <mark style="color:green;">**`common.tables.table-name`**</mark> 에 지정된 이름으로 테이블이 자동 생성됩니다. 아래는 발송 테이블(<mark style="color:red;">**`rv-submit`**</mark> — 기본 `ODYSSEY`)의 컬럼 레이아웃입니다.

<table><thead><tr><th width="169.79998779296875">컬럼명</th><th width="171">데이터 타입</th><th width="72.4000244140625">NN</th><th width="90">기본값</th><th>설명</th></tr></thead><tbody><tr><td><strong><code>MSG_ID</code></strong></td><td>BIGINT(20) AUTO_INCREMENT</td><td>Y</td><td></td><td>메시지당 유니크한 번호 (PK)</td></tr><tr><td><strong><code>LB_ID</code></strong></td><td>BIGINT(20)</td><td>Y</td><td>0</td><td>로드밸런싱 ID (HA 분산 처리용)</td></tr><tr><td><strong><code>SUBJECT</code></strong></td><td>VARCHAR(40)</td><td></td><td></td><td>메시지 제목</td></tr><tr><td><strong><code>MSG_TYPE</code></strong></td><td>TINYINT(2)</td><td>Y</td><td></td><td>1차 메시지 구분<br>(<a href="../18.-msg_type-status.md">18. MSG_TYPE / STATUS 코드</a> 참고)</td></tr><tr><td><strong><code>MSG_TYPE_SECOND</code></strong></td><td>TINYINT(2)</td><td>Y</td><td>0</td><td>2차 메시지 구분 (FALLBACK)</td></tr><tr><td><strong><code>MSG_TYPE_THIRD</code></strong></td><td>TINYINT(2)</td><td>Y</td><td>0</td><td>3차 메시지 구분 (FALLBACK)</td></tr><tr><td><strong><code>STATUS</code></strong></td><td>SMALLINT</td><td></td><td>0</td><td>메시지 상태 (<a href="../18.-msg_type-status.md">18. MSG_TYPE / STATUS 코드</a> 참고)</td></tr><tr><td><strong><code>SCHEDULE_TIME</code></strong></td><td>VARCHAR(16)</td><td>Y</td><td></td><td>발송 시작 시각 (YYYYMMDDHH24MISS)</td></tr><tr><td><strong><code>SUBMIT_TIME</code></strong></td><td>VARCHAR(16)</td><td>Y</td><td></td><td>메시지 등록 시각 (YYYYMMDDHH24MISS)</td></tr><tr><td><strong><code>MESSAGE</code></strong></td><td>TEXT</td><td></td><td></td><td>메시지 내용</td></tr><tr><td><strong><code>CALLBACK_NUM</code></strong></td><td>VARCHAR(20)</td><td>Y</td><td></td><td>회신번호 (특수문자 제외)</td></tr><tr><td><strong><code>RCPT_DATA</code></strong></td><td>VARCHAR(20)</td><td>Y</td><td></td><td>수신번호 (특수문자 제외)</td></tr><tr><td><strong><code>FILE_COUNT</code></strong></td><td>TINYINT(1)</td><td></td><td>0</td><td>MMS 첨부 파일 개수</td></tr><tr><td><strong><code>FILE_NAME1</code></strong></td><td>VARCHAR(128)</td><td></td><td></td><td>첨부 파일 1</td></tr><tr><td><strong><code>FILE_NAME2</code></strong></td><td>VARCHAR(128)</td><td></td><td></td><td>첨부 파일 2</td></tr><tr><td><strong><code>FILE_NAME3</code></strong></td><td>VARCHAR(128)</td><td></td><td></td><td>첨부 파일 3</td></tr><tr><td><strong><code>CDR_ID</code></strong></td><td>VARCHAR(20)</td><td></td><td></td><td>과금 ID</td></tr><tr><td><strong><code>RESULT</code></strong></td><td>MEDIUMINT(6)</td><td></td><td>성공 : 0</td><td>전송 결과 코드 (SMS/LMS/MMS/VMS)</td></tr><tr><td><strong><code>RCS_RESULT</code></strong></td><td>MEDIUMINT(6)</td><td></td><td></td><td>전송 결과 코드 (RCS)</td></tr><tr><td><strong><code>KKO_RESULT</code></strong></td><td>MEDIUMINT(6)</td><td></td><td></td><td>전송 결과 코드 (KAKAO)</td></tr><tr><td><strong><code>RESULT_DESC</code></strong></td><td>VARCHAR(200)</td><td></td><td></td><td>결과코드 상세 내용</td></tr><tr><td><strong><code>DELIVER_TIME</code></strong></td><td>VARCHAR(16)</td><td></td><td></td><td>전송 시각 (마지막 발송)</td></tr><tr><td><strong><code>REPORT_RECV_TIME</code></strong></td><td>VARCHAR(16)</td><td></td><td></td><td>리포트 수신 시각</td></tr><tr><td><strong><code>TELCOINFO</code></strong></td><td>VARCHAR(4)</td><td></td><td></td><td>수신자 이통사 정보</td></tr><tr><td><strong><code>FAIL_SEND</code></strong></td><td>VARCHAR(1)</td><td></td><td>'N'</td><td>실패 재발송(FALLBACK) 여부 (Y/N)</td></tr><tr><td><strong><code>K_TMPLCODE</code></strong></td><td>VARCHAR(30)</td><td></td><td></td><td>알림톡 템플릿 코드</td></tr><tr><td><strong><code>K_MESSAGE</code></strong></td><td>TEXT</td><td></td><td></td><td>알림톡 메시지 내용</td></tr><tr><td><strong><code>K_OPTION</code></strong></td><td>TEXT</td><td></td><td></td><td>알림톡 button 등 옵션(JSON)<br>- alimtalk-param : false 일 때</td></tr><tr><td><strong><code>K_SERIAL_NM</code></strong></td><td>VARCHAR(40)</td><td></td><td></td><td>알림톡 시리얼명</td></tr><tr><td><strong><code>K_ADFLAG</code></strong></td><td>VARCHAR(1)</td><td></td><td>'N'</td><td>알림톡 광고 문구 여부 (Y/N)</td></tr><tr><td><strong><code>K_SENDERKEY</code></strong></td><td>VARCHAR(40)</td><td></td><td></td><td>알림톡 발신 프로필 키</td></tr><tr><td><strong><code>R_MESSAGEBASEID</code></strong></td><td>VARCHAR(40)</td><td></td><td></td><td>RCS messageBaseId</td></tr><tr><td><strong><code>R_BODY</code></strong></td><td>TEXT</td><td></td><td></td><td>RCS body (JSON)</td></tr><tr><td><strong><code>R_BUTTON</code></strong></td><td>TEXT</td><td></td><td></td><td>RCS button (JSON)</td></tr><tr><td><strong><code>R_HEADER</code></strong></td><td>TINYINT(1)</td><td></td><td></td><td>RCS 광고 문구 여부 (0/1)</td></tr><tr><td><strong><code>R_FOOTER</code></strong></td><td>VARCHAR(20)</td><td></td><td></td><td>RCS 수신거부 번호 (R_HEADER=1 시 필수)</td></tr><tr><td><strong><code>R_COPYALLOWED</code></strong></td><td>VARCHAR(1)</td><td></td><td>'N'</td><td>RCS 메시지 복사 허용 여부 (Y/N)</td></tr><tr><td><strong><code>R_QUERYID</code></strong></td><td>VARCHAR(60)</td><td></td><td></td><td>RCS 리포트 요청 queryId</td></tr><tr><td><strong><code>RESERVED01</code></strong></td><td>VARCHAR(60)</td><td></td><td></td><td>예약 필드 1</td></tr><tr><td><strong><code>RESERVED02</code></strong></td><td>VARCHAR(60)</td><td></td><td></td><td>예약 필드 2</td></tr><tr><td><strong><code>RESERVED03</code></strong></td><td>VARCHAR(60)</td><td></td><td></td><td>예약 필드 3</td></tr><tr><td><strong><code>KISA_ORIG_CODE</code></strong></td><td>VARCHAR(9)</td><td></td><td></td><td>KISA 코드</td></tr><tr><td><strong><code>R_AGENCYID</code></strong></td><td>VARCHAR(60)</td><td></td><td></td><td>RCS agencyId</td></tr><tr><td><strong><code>R_AGENCYKEY</code></strong></td><td>VARCHAR(256)</td><td></td><td></td><td>RCS agencyKey</td></tr><tr><td><strong><code>R_BRANDKEY</code></strong></td><td>VARCHAR(256)</td><td></td><td></td><td>RCS brandKey</td></tr><tr><td><strong><code>R_CDR_ID</code></strong></td><td>VARCHAR(20)</td><td></td><td></td><td>RCS 과금 ID</td></tr><tr><td><strong><code>TRACKING_ID</code></strong></td><td>VARCHAR(40)</td><td></td><td></td><td>리포트 요청 TRACKING ID</td></tr><tr><td><strong><code>TOKEN</code></strong></td><td>VARCHAR(100)</td><td></td><td></td><td>리포트 요청 TOKEN</td></tr><tr><td><strong><code>C_STATUS</code></strong></td><td>VARCHAR(1)</td><td></td><td></td><td>CPaaS 전송 결과 STATUS</td></tr><tr><td><strong><code>SUB_KEY</code></strong></td><td>VARCHAR(100)</td><td></td><td></td><td>CPAAS 부서/과금 분리 코드</td></tr><tr><td><strong><code>C_TMPL_ID</code></strong></td><td>VARCHAR(80)</td><td></td><td></td><td>CPaaS 템플릿 ID 기반 발송 (SMS/LMS/MMS) 의 templateId</td></tr><tr><td><strong><code>GSMS_TYPE</code></strong></td><td>TINYINT(1)</td><td></td><td>0</td><td>GSMS 문자열 타입<br>0 : unicode / 1 : text</td></tr></tbody></table>

## <mark style="color:blue;">DBMS 별 테이블 생성문</mark> <a href="#create-table" id="create-table"></a>

Odyssey 가 최초 기동 때 발송 테이블을 만드는 생성문입니다. <mark style="color:red;">**`config/mapper/{{DBMS}}/table.xml`**</mark> 의 `createSubmitTable` 내용이며, 테이블 이름은 기본값 `ODYSSEY` 로 표기했습니다.

{% hint style="info" %}
테이블은 Odyssey 가 자동으로 만듭니다. 아래 생성문을 직접 실행할 필요는 없습니다. Oracle 은 **`MSG_ID`** 자동 증가를 위해 시퀀스와 트리거를 함께 만듭니다.
{% endhint %}

{% tabs %}
{% tab title="MySQL" %}
```sql
CREATE TABLE IF NOT EXISTS ODYSSEY (
    MSG_ID BIGINT(20) NOT NULL AUTO_INCREMENT COMMENT '메시지당 유니크한 번호',
    LB_ID BIGINT(20) NOT NULL DEFAULT '0' COMMENT '로드밸런싱 아이디',
    SUBJECT VARCHAR(40) DEFAULT NULL COMMENT '메시지 제목',
    MSG_TYPE TINYINT(2) NOT NULL COMMENT '첫번째 메시지 구분 1=SMS, 2=LMS, 3=MMS, 4=VMS, 6=A_KAKAO, 7=F_KAKAO, 8=AI_KAKAO, 9=RCSSMS, 10=RCSLMS, 11=RCSMMS, 12=RCSTMPL, 13=RCSITMPL, 22=GSMS',
    MSG_TYPE_SECOND TINYINT(2) NOT NULL DEFAULT '0' COMMENT '두번째 메시지 구분 1=SMS, 2=LMS, 3=MMS, 4=VMS, 6=A_KAKAO, 7=F_KAKAO, 8=AI_KAKAO, 9=RCSSMS, 10=RCSLMS, 11=RCSMMS, 12=RCSTMPL, 13=RCSITMPL, 22=GSMS',
    MSG_TYPE_THIRD TINYINT(2) NOT NULL DEFAULT '0' COMMENT '세번째 메시지 구분 1=SMS, 2=LMS, 3=MMS, 4=VMS, 6=A_KAKAO, 7=F_KAKAO, 8=AI_KAKAO, 9=RCSSMS, 10=RCSLMS, 11=RCSMMS, 12=RCSTMPL, 13=RCSITMPL, 22=GSMS',
    STATUS SMALLINT DEFAULT '0' COMMENT '메시지 상태 0=전송대기, 1=전송중, 2=전송완료, ...',
    SCHEDULE_TIME VARCHAR(16) NOT NULL COMMENT '메시지전송 시작 시간(YYYYMMDDHH24MISS)',
    SUBMIT_TIME VARCHAR(16) NOT NULL COMMENT '메시지 등록 시간(YYYYMMDDHH24MISS)',
    MESSAGE TEXT COMMENT '메시지 내용',
    CALLBACK_NUM VARCHAR(20) NOT NULL COMMENT '회신번호(특수 기호 제외)',
    RCPT_DATA VARCHAR(20) NOT NULL COMMENT '수신번호(특수 기호 제외)',
    FILE_COUNT TINYINT(1) DEFAULT '0' COMMENT 'MMS 전송 파일 개수',
    FILE_NAME1 VARCHAR(128) DEFAULT NULL COMMENT 'MMS 전송 파일 1',
    FILE_NAME2 VARCHAR(128) DEFAULT NULL COMMENT 'MMS 전송 파일 2',
    FILE_NAME3 VARCHAR(128) DEFAULT NULL COMMENT 'MMS 전송 파일 3',
    CDR_ID VARCHAR(20) DEFAULT NULL COMMENT '과금 아이디',
    RESULT MEDIUMINT(6) DEFAULT NULL COMMENT '전송결과코드(SMS/LMS/MMS)',
    RCS_RESULT MEDIUMINT(6) DEFAULT NULL COMMENT '전송결과코드(RCS)',
    KKO_RESULT MEDIUMINT(6) DEFAULT NULL COMMENT '전송결과코드(KAKAO)',
    RESULT_DESC VARCHAR(200) DEFAULT NULL COMMENT '결과코드 상세 내용',
    DELIVER_TIME VARCHAR(16) DEFAULT NULL COMMENT '전송시간(마지막 전달 메시지)(YYYYMMDDHH24MISS)',
    REPORT_RECV_TIME VARCHAR(16) DEFAULT NULL COMMENT '리포트 수신 시간(마지막 전달 메시지)(YYYYMMDDHH24MISS)',
    TELCOINFO VARCHAR(4) DEFAULT NULL COMMENT '수신자 이통사 정보',
    FAIL_SEND VARCHAR(1) DEFAULT 'N' COMMENT '실패 재발송 여부(Y/N)',
    K_TMPLCODE VARCHAR(30) DEFAULT NULL COMMENT '알림톡 전용 알림톡 템플릿 코드',
    K_MESSAGE TEXT COMMENT '알림톡 전용 알림톡 메시지 내용',
    K_OPTION TEXT COMMENT '알림톡 전용 알림톡 button - json 포맷',
    K_SERIAL_NM VARCHAR(40),
    K_ADFLAG VARCHAR(1) DEFAULT 'N' COMMENT '알림톡 전용 광고 문구 여부(Y/N)',
    K_SENDERKEY VARCHAR(40) DEFAULT NULL COMMENT '알림톡 발신 프로필 키',
    R_MESSAGEBASEID VARCHAR(40) DEFAULT NULL COMMENT 'RCS 전용 RCS messageBaseId',
    R_BODY TEXT COMMENT 'RCS 전용 RCS body - json 포맷',
    R_BUTTON TEXT COMMENT 'RCS 전용 RCS button - json 포맷',
    R_HEADER TINYINT(1) DEFAULT 0 COMMENT 'RCS 전용 RCS 광고 문구 여부 (0/1)',
    R_FOOTER VARCHAR(20) DEFAULT NULL COMMENT 'RCS 전용 RCS 수신거부 전화번호 R_HEADER가 0인 경우 입력불가, R_HEADER가 1인 경우 필수',
    R_COPYALLOWED VARCHAR(1) DEFAULT 'N' COMMENT 'RCS 전용 RCS 단말의 메시지 복사 기능 허용 여부(Y/N)',
    R_QUERYID VARCHAR(60) DEFAULT NULL COMMENT 'RCS 전용 RCS queryId',
    RESERVED01 VARCHAR(60) DEFAULT NULL COMMENT '예약필드1',
    RESERVED02 VARCHAR(60) DEFAULT NULL COMMENT '예약필드2',
    RESERVED03 VARCHAR(60) DEFAULT NULL COMMENT '예약필드3',
    KISA_ORIG_CODE VARCHAR(9) DEFAULT NULL COMMENT 'KISA 코드',
    R_AGENCYID VARCHAR(60) DEFAULT NULL COMMENT 'RCS 전용 RCS agencyId',
    R_AGENCYKEY VARCHAR(256) DEFAULT NULL COMMENT 'AGENCYKEY',
    R_BRANDKEY VARCHAR(256) DEFAULT NULL COMMENT 'BRANDKEY',
    R_CDR_ID VARCHAR(20) DEFAULT NULL COMMENT 'RCS 과금 아이디',
    TRACKING_ID VARCHAR(40) DEFAULT NULL COMMENT '리포트 요청 TRACKING ID',
    TOKEN VARCHAR(100) DEFAULT NULL COMMENT '리포트 요청 TOKEN',
    C_STATUS VARCHAR(1) DEFAULT NULL,
    SUB_KEY VARCHAR(100) DEFAULT NULL COMMENT '부서 ID',
    C_TMPL_ID VARCHAR(80) DEFAULT NULL COMMENT 'CPaaS 템플릿ID 기반 발송 (SMS/LMS/MMS) - templateId',
    GSMS_TYPE TINYINT(1) DEFAULT '0' COMMENT 'GSMS 전용 문자열 타입 (0=unicode / 1=text)',
    PRIMARY KEY (MSG_ID),
    KEY IDX_M2X_SUBMIT_1 (STATUS, MSG_TYPE, SCHEDULE_TIME, MSG_ID),
    KEY IDX_M2X_SUBMIT_2 (STATUS, MSG_TYPE_SECOND, SCHEDULE_TIME, MSG_ID),
    KEY IDX_M2X_SUBMIT_3 (STATUS, MSG_TYPE_THIRD, SCHEDULE_TIME, MSG_ID),
    KEY IDX_M2X_SUBMIT_4 (TRACKING_ID, STATUS),
    KEY IDX_M2X_SUBMIT_5 (C_STATUS, STATUS, REPORT_RECV_TIME, MSG_ID),
    KEY IDX_M2X_SUBMIT_6 (MSG_ID, STATUS),
    KEY IDX_M2X_SUBMIT_FETCH_1 (LB_ID, STATUS, MSG_ID),
    KEY IDX_M2X_SUBMIT_EXPIRE_1 (LB_ID, SCHEDULE_TIME, MSG_ID)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci
```
{% endtab %}

{% tab title="MariaDB" %}
```sql
CREATE TABLE IF NOT EXISTS ODYSSEY (
    MSG_ID BIGINT(20) NOT NULL AUTO_INCREMENT COMMENT '메시지당 유니크한 번호',
    LB_ID BIGINT(20) NOT NULL DEFAULT '0' COMMENT '로드밸런싱 아이디',
    SUBJECT VARCHAR(40) DEFAULT NULL COMMENT '메시지 제목',
    MSG_TYPE TINYINT(2) NOT NULL COMMENT '첫번째 메시지 구분 1=SMS, 2=LMS, 3=MMS, 4=VMS, 6=A_KAKAO, 7=F_KAKAO, 8=AI_KAKAO, 9=RCSSMS, 10=RCSLMS, 11=RCSMMS, 12=RCSTMPL, 13=RCSITMPL, 22=GSMS',
    MSG_TYPE_SECOND TINYINT(2) NOT NULL DEFAULT '0' COMMENT '두번째 메시지 구분 1=SMS, 2=LMS, 3=MMS, 4=VMS, 6=A_KAKAO, 7=F_KAKAO, 8=AI_KAKAO, 9=RCSSMS, 10=RCSLMS, 11=RCSMMS, 12=RCSTMPL, 13=RCSITMPL, 22=GSMS',
    MSG_TYPE_THIRD TINYINT(2) NOT NULL DEFAULT '0' COMMENT '세번째 메시지 구분 1=SMS, 2=LMS, 3=MMS, 4=VMS, 6=A_KAKAO, 7=F_KAKAO, 8=AI_KAKAO, 9=RCSSMS, 10=RCSLMS, 11=RCSMMS, 12=RCSTMPL, 13=RCSITMPL, 22=GSMS',
    STATUS SMALLINT DEFAULT '0' COMMENT '메시지 상태 0=전송대기, 1=전송중, 2=전송완료, ...',
    SCHEDULE_TIME VARCHAR(16) NOT NULL COMMENT '메시지전송 시작 시간(YYYYMMDDHH24MISS)',
    SUBMIT_TIME VARCHAR(16) NOT NULL COMMENT '메시지 등록 시간(YYYYMMDDHH24MISS)',
    MESSAGE TEXT COMMENT '메시지 내용',
    CALLBACK_NUM VARCHAR(20) NOT NULL COMMENT '회신번호(특수 기호 제외)',
    RCPT_DATA VARCHAR(20) NOT NULL COMMENT '수신번호(특수 기호 제외)',
    FILE_COUNT TINYINT(1) DEFAULT '0' COMMENT 'MMS 전송 파일 개수',
    FILE_NAME1 VARCHAR(128) DEFAULT NULL COMMENT 'MMS 전송 파일 1',
    FILE_NAME2 VARCHAR(128) DEFAULT NULL COMMENT 'MMS 전송 파일 2',
    FILE_NAME3 VARCHAR(128) DEFAULT NULL COMMENT 'MMS 전송 파일 3',
    CDR_ID VARCHAR(20) DEFAULT NULL COMMENT '과금 아이디',
    RESULT MEDIUMINT(6) DEFAULT NULL COMMENT '전송결과코드(SMS/LMS/MMS)',
    RCS_RESULT MEDIUMINT(6) DEFAULT NULL COMMENT '전송결과코드(RCS)',
    KKO_RESULT MEDIUMINT(6) DEFAULT NULL COMMENT '전송결과코드(KAKAO)',
    RESULT_DESC VARCHAR(200) DEFAULT NULL COMMENT '결과코드 상세 내용',
    DELIVER_TIME VARCHAR(16) DEFAULT NULL COMMENT '전송시간(마지막 전달 메시지)(YYYYMMDDHH24MISS)',
    REPORT_RECV_TIME VARCHAR(16) DEFAULT NULL COMMENT '리포트 수신 시간(마지막 전달 메시지)(YYYYMMDDHH24MISS)',
    TELCOINFO VARCHAR(4) DEFAULT NULL COMMENT '수신자 이통사 정보',
    FAIL_SEND VARCHAR(1) DEFAULT 'N' COMMENT '실패 재발송 여부(Y/N)',
    K_TMPLCODE VARCHAR(30) DEFAULT NULL COMMENT '알림톡 전용 알림톡 템플릿 코드',
    K_MESSAGE TEXT COMMENT '알림톡 전용 알림톡 메시지 내용',
    K_OPTION TEXT COMMENT '알림톡 전용 알림톡 button - json 포맷',
    K_SERIAL_NM VARCHAR(40),
    K_ADFLAG VARCHAR(1) DEFAULT 'N' COMMENT '알림톡 전용 광고 문구 여부(Y/N)',
    K_SENDERKEY VARCHAR(40) DEFAULT NULL COMMENT '알림톡 발신 프로필 키',
    R_MESSAGEBASEID VARCHAR(40) DEFAULT NULL COMMENT 'RCS 전용 RCS messageBaseId',
    R_BODY TEXT COMMENT 'RCS 전용 RCS body - json 포맷',
    R_BUTTON TEXT COMMENT 'RCS 전용 RCS button - json 포맷',
    R_HEADER TINYINT(1) DEFAULT 0 COMMENT 'RCS 전용 RCS 광고 문구 여부 (0/1)',
    R_FOOTER VARCHAR(20) DEFAULT NULL COMMENT 'RCS 전용 RCS 수신거부 전화번호 R_HEADER가 0인 경우 입력불가, R_HEADER가 1인 경우 필수',
    R_COPYALLOWED VARCHAR(1) DEFAULT 'N' COMMENT 'RCS 전용 RCS 단말의 메시지 복사 기능 허용 여부(Y/N)',
    R_QUERYID VARCHAR(60) DEFAULT NULL COMMENT 'RCS 전용 RCS queryId',
    RESERVED01 VARCHAR(60) DEFAULT NULL COMMENT '예약필드1',
    RESERVED02 VARCHAR(60) DEFAULT NULL COMMENT '예약필드2',
    RESERVED03 VARCHAR(60) DEFAULT NULL COMMENT '예약필드3',
    KISA_ORIG_CODE VARCHAR(9) DEFAULT NULL COMMENT 'KISA 코드',
    R_AGENCYID VARCHAR(60) DEFAULT NULL COMMENT 'RCS 전용 RCS agencyId',
    R_AGENCYKEY VARCHAR(256) DEFAULT NULL COMMENT 'AGENCYKEY',
    R_BRANDKEY VARCHAR(256) DEFAULT NULL COMMENT 'BRANDKEY',
    R_CDR_ID VARCHAR(20) DEFAULT NULL COMMENT 'RCS 과금 아이디',
    TRACKING_ID VARCHAR(40) DEFAULT NULL COMMENT '리포트 요청 TRACKING ID',
    TOKEN VARCHAR(100) DEFAULT NULL COMMENT '리포트 요청 TOKEN',
    C_STATUS VARCHAR(1) DEFAULT NULL,
    SUB_KEY VARCHAR(100) DEFAULT NULL COMMENT '부서 ID',
    C_TMPL_ID VARCHAR(80) DEFAULT NULL COMMENT 'CPaaS 템플릿ID 기반 발송 (SMS/LMS/MMS) - templateId',
    GSMS_TYPE TINYINT(1) DEFAULT '0' COMMENT 'GSMS 전용 문자열 타입 (0=unicode / 1=text)',
    PRIMARY KEY (MSG_ID),
    KEY IDX_M2X_SUBMIT_1 (STATUS, MSG_TYPE, SCHEDULE_TIME, MSG_ID),
    KEY IDX_M2X_SUBMIT_2 (STATUS, MSG_TYPE_SECOND, SCHEDULE_TIME, MSG_ID),
    KEY IDX_M2X_SUBMIT_3 (STATUS, MSG_TYPE_THIRD, SCHEDULE_TIME, MSG_ID),
    KEY IDX_M2X_SUBMIT_4 (TRACKING_ID, STATUS),
    KEY IDX_M2X_SUBMIT_5 (C_STATUS, STATUS, REPORT_RECV_TIME, MSG_ID),
    KEY IDX_M2X_SUBMIT_6 (MSG_ID, STATUS),
    KEY IDX_M2X_SUBMIT_FETCH_1 (LB_ID, STATUS, MSG_ID),
    KEY IDX_M2X_SUBMIT_EXPIRE_1 (LB_ID, SCHEDULE_TIME, MSG_ID)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci
```
{% endtab %}

{% tab title="PostgreSQL" %}
```sql
CREATE TABLE IF NOT EXISTS ODYSSEY (
    MSG_ID          BIGSERIAL    PRIMARY KEY,
    LB_ID           BIGINT       NOT NULL DEFAULT 0,
    SUBJECT         VARCHAR(40),
    MSG_TYPE        SMALLINT     NOT NULL,
    MSG_TYPE_SECOND SMALLINT     NOT NULL DEFAULT 0,
    MSG_TYPE_THIRD  SMALLINT     NOT NULL DEFAULT 0,
    STATUS          SMALLINT     DEFAULT 0,
    SCHEDULE_TIME   VARCHAR(16)  NOT NULL,
    SUBMIT_TIME     VARCHAR(16)  NOT NULL,
    MESSAGE         TEXT,
    CALLBACK_NUM    VARCHAR(20)  NOT NULL,
    RCPT_DATA       VARCHAR(20)  NOT NULL,
    FILE_COUNT      SMALLINT     DEFAULT 0,
    FILE_NAME1      VARCHAR(128),
    FILE_NAME2      VARCHAR(128),
    FILE_NAME3      VARCHAR(128),
    CDR_ID          VARCHAR(20),
    RESULT          INTEGER,
    RCS_RESULT      INTEGER,
    KKO_RESULT      INTEGER,
    RESULT_DESC     VARCHAR(200),
    DELIVER_TIME    VARCHAR(16),
    REPORT_RECV_TIME VARCHAR(16),
    TELCOINFO       VARCHAR(4),
    FAIL_SEND       VARCHAR(1)   DEFAULT 'N',
    K_TMPLCODE      VARCHAR(30),
    K_MESSAGE       TEXT,
    K_OPTION        TEXT,
    K_SERIAL_NM     VARCHAR(40),
    K_ADFLAG        VARCHAR(1)   DEFAULT 'N',
    K_SENDERKEY     VARCHAR(40),
    R_MESSAGEBASEID VARCHAR(40),
    R_BODY          TEXT,
    R_BUTTON        TEXT,
    R_HEADER        SMALLINT     DEFAULT 0,
    R_FOOTER        VARCHAR(20),
    R_COPYALLOWED   VARCHAR(1)   DEFAULT 'N',
    R_QUERYID       VARCHAR(60),
    RESERVED01      VARCHAR(60),
    RESERVED02      VARCHAR(60),
    RESERVED03      VARCHAR(60),
    KISA_ORIG_CODE  VARCHAR(9),
    R_AGENCYID      VARCHAR(60),
    R_AGENCYKEY     VARCHAR(256),
    R_BRANDKEY      VARCHAR(256),
    R_CDR_ID        VARCHAR(20),
    TRACKING_ID     VARCHAR(40),
    TOKEN           VARCHAR(100),
    C_STATUS        VARCHAR(1),
    SUB_KEY         VARCHAR(100),
    C_TMPL_ID       VARCHAR(80),
    GSMS_TYPE      SMALLINT     DEFAULT 0
);
CREATE INDEX IF NOT EXISTS IDX_ODYSSEY_1 ON ODYSSEY (STATUS, MSG_TYPE, SCHEDULE_TIME, MSG_ID);
CREATE INDEX IF NOT EXISTS IDX_ODYSSEY_2 ON ODYSSEY (STATUS, MSG_TYPE_SECOND, SCHEDULE_TIME, MSG_ID);
CREATE INDEX IF NOT EXISTS IDX_ODYSSEY_3 ON ODYSSEY (STATUS, MSG_TYPE_THIRD, SCHEDULE_TIME, MSG_ID);
CREATE INDEX IF NOT EXISTS IDX_ODYSSEY_4 ON ODYSSEY (TRACKING_ID, STATUS);
CREATE INDEX IF NOT EXISTS IDX_ODYSSEY_5 ON ODYSSEY (C_STATUS, STATUS, REPORT_RECV_TIME, MSG_ID);
CREATE INDEX IF NOT EXISTS IDX_ODYSSEY_6 ON ODYSSEY (MSG_ID, STATUS);
CREATE INDEX IF NOT EXISTS IDX_ODYSSEY_FETCH_1 ON ODYSSEY (LB_ID, STATUS, MSG_ID);
CREATE INDEX IF NOT EXISTS IDX_ODYSSEY_EXPIRE_1 ON ODYSSEY (LB_ID, SCHEDULE_TIME, MSG_ID);
```
{% endtab %}

{% tab title="Oracle" %}
```sql
DECLARE
    v_new   BOOLEAN       := TRUE;
    v_table VARCHAR2(128) := 'ODYSSEY';
    v_idx   VARCHAR2(24)  := 'IX_' || SUBSTR(v_table, -LEAST(20, LENGTH(v_table)));
BEGIN
    BEGIN
        EXECUTE IMMEDIATE 'CREATE TABLE ODYSSEY (
    MSG_ID          NUMBER(20)    PRIMARY KEY,
    LB_ID           NUMBER(20)    DEFAULT 0 NOT NULL,
    SUBJECT         VARCHAR2(40),
    MSG_TYPE        NUMBER(3)     NOT NULL,
    MSG_TYPE_SECOND NUMBER(3)     DEFAULT 0 NOT NULL,
    MSG_TYPE_THIRD  NUMBER(3)     DEFAULT 0 NOT NULL,
    STATUS          SMALLINT      DEFAULT 0,
    SCHEDULE_TIME   VARCHAR2(16)  NOT NULL,
    SUBMIT_TIME     VARCHAR2(16)  NOT NULL,
    MESSAGE         CLOB,
    CALLBACK_NUM    VARCHAR2(20)  NOT NULL,
    RCPT_DATA       VARCHAR2(20)  NOT NULL,
    FILE_COUNT      NUMBER(3)     DEFAULT 0,
    FILE_NAME1      VARCHAR2(128),
    FILE_NAME2      VARCHAR2(128),
    FILE_NAME3      VARCHAR2(128),
    CDR_ID          VARCHAR2(20),
    RESULT          NUMBER(8),
    RCS_RESULT      NUMBER(8),
    KKO_RESULT      NUMBER(8),
    RESULT_DESC     VARCHAR2(200),
    DELIVER_TIME    VARCHAR2(16),
    REPORT_RECV_TIME VARCHAR2(16),
    TELCOINFO       VARCHAR2(4),
    FAIL_SEND       VARCHAR2(1)   DEFAULT ''N'',
    K_TMPLCODE      VARCHAR2(30),
    K_MESSAGE       CLOB,
    K_OPTION        CLOB,
    K_SERIAL_NM     VARCHAR2(40),
    K_ADFLAG        VARCHAR2(1)   DEFAULT ''N'',
    K_SENDERKEY     VARCHAR2(40),
    R_MESSAGEBASEID VARCHAR2(40),
    R_BODY          CLOB,
    R_BUTTON        CLOB,
    R_HEADER        NUMBER(3)     DEFAULT 0,
    R_FOOTER        VARCHAR2(20),
    R_COPYALLOWED   VARCHAR2(1)   DEFAULT ''N'',
    R_QUERYID       VARCHAR2(60),
    RESERVED01      VARCHAR2(60),
    RESERVED02      VARCHAR2(60),
    RESERVED03      VARCHAR2(60),
    KISA_ORIG_CODE  VARCHAR2(9),
    R_AGENCYID      VARCHAR2(60),
    R_AGENCYKEY     VARCHAR2(256),
    R_BRANDKEY      VARCHAR2(256),
    R_CDR_ID        VARCHAR2(20),
    TRACKING_ID     VARCHAR2(40),
    TOKEN           VARCHAR2(100),
    C_STATUS        VARCHAR2(1),
    SUB_KEY         VARCHAR2(100),
    C_TMPL_ID       VARCHAR2(80),
    GSMS_TYPE       NUMBER(3)     DEFAULT 0
)';
    EXCEPTION WHEN OTHERS THEN
        IF SQLCODE = -955 THEN v_new := FALSE; ELSE RAISE; END IF;
    END;
    IF v_new THEN
        BEGIN
            EXECUTE IMMEDIATE 'CREATE SEQUENCE SQ_ODYSSEY START WITH 1 INCREMENT BY 1';
        EXCEPTION WHEN OTHERS THEN
            IF SQLCODE != -955 THEN RAISE; END IF;
        END;
        EXECUTE IMMEDIATE 'CREATE OR REPLACE TRIGGER TR_ODYSSEY BEFORE INSERT ON ODYSSEY FOR EACH ROW WHEN (NEW.MSG_ID IS NULL) BEGIN SELECT SQ_ODYSSEY.NEXTVAL INTO :NEW.MSG_ID FROM DUAL; END;';
    END IF;
    -- 인덱스는 기존 테이블에도 보장한다. ORA-00955(이름 중복) / ORA-01408(같은 컬럼 조합 인덱스 존재)만 무시.
    BEGIN EXECUTE IMMEDIATE 'CREATE INDEX ' || v_idx || '_1 ON ' || v_table || ' (STATUS, MSG_TYPE, SCHEDULE_TIME, MSG_ID)'; EXCEPTION WHEN OTHERS THEN IF SQLCODE NOT IN (-955, -1408) THEN RAISE; END IF; END;
    BEGIN EXECUTE IMMEDIATE 'CREATE INDEX ' || v_idx || '_2 ON ' || v_table || ' (STATUS, MSG_TYPE_SECOND, SCHEDULE_TIME, MSG_ID)'; EXCEPTION WHEN OTHERS THEN IF SQLCODE NOT IN (-955, -1408) THEN RAISE; END IF; END;
    BEGIN EXECUTE IMMEDIATE 'CREATE INDEX ' || v_idx || '_3 ON ' || v_table || ' (STATUS, MSG_TYPE_THIRD, SCHEDULE_TIME, MSG_ID)'; EXCEPTION WHEN OTHERS THEN IF SQLCODE NOT IN (-955, -1408) THEN RAISE; END IF; END;
    BEGIN EXECUTE IMMEDIATE 'CREATE INDEX ' || v_idx || '_4 ON ' || v_table || ' (TRACKING_ID, STATUS)'; EXCEPTION WHEN OTHERS THEN IF SQLCODE NOT IN (-955, -1408) THEN RAISE; END IF; END;
    BEGIN EXECUTE IMMEDIATE 'CREATE INDEX ' || v_idx || '_5 ON ' || v_table || ' (C_STATUS, STATUS, REPORT_RECV_TIME, MSG_ID)'; EXCEPTION WHEN OTHERS THEN IF SQLCODE NOT IN (-955, -1408) THEN RAISE; END IF; END;
    BEGIN EXECUTE IMMEDIATE 'CREATE INDEX ' || v_idx || '_6 ON ' || v_table || ' (MSG_ID, STATUS)'; EXCEPTION WHEN OTHERS THEN IF SQLCODE NOT IN (-955, -1408) THEN RAISE; END IF; END;
    BEGIN EXECUTE IMMEDIATE 'CREATE INDEX ' || v_idx || '_F1 ON ' || v_table || ' (LB_ID, STATUS, MSG_ID)'; EXCEPTION WHEN OTHERS THEN IF SQLCODE NOT IN (-955, -1408) THEN RAISE; END IF; END;
    BEGIN EXECUTE IMMEDIATE 'CREATE INDEX ' || v_idx || '_E1 ON ' || v_table || ' (LB_ID, SCHEDULE_TIME, MSG_ID)'; EXCEPTION WHEN OTHERS THEN IF SQLCODE NOT IN (-955, -1408) THEN RAISE; END IF; END;
END;
```
{% endtab %}

{% tab title="SQL Server" %}
```sql
IF OBJECT_ID('ODYSSEY', 'U') IS NULL
CREATE TABLE ODYSSEY (
    MSG_ID          BIGINT          IDENTITY(1,1) PRIMARY KEY,
    LB_ID           BIGINT          NOT NULL DEFAULT 0,
    SUBJECT         NVARCHAR(40),
    MSG_TYPE        SMALLINT        NOT NULL,
    MSG_TYPE_SECOND SMALLINT        NOT NULL DEFAULT 0,
    MSG_TYPE_THIRD  SMALLINT        NOT NULL DEFAULT 0,
    STATUS          SMALLINT        DEFAULT 0,
    SCHEDULE_TIME   NVARCHAR(16)    NOT NULL,
    SUBMIT_TIME     NVARCHAR(16)    NOT NULL,
    MESSAGE         NVARCHAR(MAX),
    CALLBACK_NUM    NVARCHAR(20)    NOT NULL,
    RCPT_DATA       NVARCHAR(20)    NOT NULL,
    FILE_COUNT      SMALLINT        DEFAULT 0,
    FILE_NAME1      NVARCHAR(128),
    FILE_NAME2      NVARCHAR(128),
    FILE_NAME3      NVARCHAR(128),
    CDR_ID          NVARCHAR(20),
    RESULT          INT,
    RCS_RESULT      INT,
    KKO_RESULT      INT,
    RESULT_DESC     NVARCHAR(200),
    DELIVER_TIME    NVARCHAR(16),
    REPORT_RECV_TIME NVARCHAR(16),
    TELCOINFO       NVARCHAR(4),
    FAIL_SEND       NVARCHAR(1)     DEFAULT 'N',
    K_TMPLCODE      NVARCHAR(30),
    K_MESSAGE       NVARCHAR(MAX),
    K_OPTION        NVARCHAR(MAX),
    K_SERIAL_NM     NVARCHAR(40),
    K_ADFLAG        NVARCHAR(1)     DEFAULT 'N',
    K_SENDERKEY     NVARCHAR(40),
    R_MESSAGEBASEID NVARCHAR(40),
    R_BODY          NVARCHAR(MAX),
    R_BUTTON        NVARCHAR(MAX),
    R_HEADER        SMALLINT        DEFAULT 0,
    R_FOOTER        NVARCHAR(20),
    R_COPYALLOWED   NVARCHAR(1)     DEFAULT 'N',
    R_QUERYID       NVARCHAR(60),
    RESERVED01      NVARCHAR(60),
    RESERVED02      NVARCHAR(60),
    RESERVED03      NVARCHAR(60),
    KISA_ORIG_CODE  NVARCHAR(9),
    R_AGENCYID      NVARCHAR(60),
    R_AGENCYKEY     NVARCHAR(256),
    R_BRANDKEY      NVARCHAR(256),
    R_CDR_ID        NVARCHAR(20),
    TRACKING_ID     NVARCHAR(40),
    TOKEN           NVARCHAR(100),
    C_STATUS        NVARCHAR(1),
    SUB_KEY         NVARCHAR(100),
    C_TMPL_ID       NVARCHAR(80),
    GSMS_TYPE       SMALLINT        DEFAULT 0
);
IF NOT EXISTS (SELECT 1 FROM sys.indexes WHERE name = 'IDX_M2X_SUBMIT_1' AND object_id = OBJECT_ID('ODYSSEY'))
CREATE INDEX IDX_M2X_SUBMIT_1 ON ODYSSEY (STATUS, MSG_TYPE, SCHEDULE_TIME, MSG_ID);
IF NOT EXISTS (SELECT 1 FROM sys.indexes WHERE name = 'IDX_M2X_SUBMIT_2' AND object_id = OBJECT_ID('ODYSSEY'))
CREATE INDEX IDX_M2X_SUBMIT_2 ON ODYSSEY (STATUS, MSG_TYPE_SECOND, SCHEDULE_TIME, MSG_ID);
IF NOT EXISTS (SELECT 1 FROM sys.indexes WHERE name = 'IDX_M2X_SUBMIT_3' AND object_id = OBJECT_ID('ODYSSEY'))
CREATE INDEX IDX_M2X_SUBMIT_3 ON ODYSSEY (STATUS, MSG_TYPE_THIRD, SCHEDULE_TIME, MSG_ID);
IF NOT EXISTS (SELECT 1 FROM sys.indexes WHERE name = 'IDX_M2X_SUBMIT_4' AND object_id = OBJECT_ID('ODYSSEY'))
CREATE INDEX IDX_M2X_SUBMIT_4 ON ODYSSEY (TRACKING_ID, STATUS);
IF NOT EXISTS (SELECT 1 FROM sys.indexes WHERE name = 'IDX_M2X_SUBMIT_5' AND object_id = OBJECT_ID('ODYSSEY'))
CREATE INDEX IDX_M2X_SUBMIT_5 ON ODYSSEY (C_STATUS, STATUS, REPORT_RECV_TIME, MSG_ID);
IF NOT EXISTS (SELECT 1 FROM sys.indexes WHERE name = 'IDX_M2X_SUBMIT_6' AND object_id = OBJECT_ID('ODYSSEY'))
CREATE INDEX IDX_M2X_SUBMIT_6 ON ODYSSEY (MSG_ID, STATUS);
IF NOT EXISTS (SELECT 1 FROM sys.indexes WHERE name = 'IDX_M2X_SUBMIT_FETCH_1' AND object_id = OBJECT_ID('ODYSSEY'))
CREATE INDEX IDX_M2X_SUBMIT_FETCH_1 ON ODYSSEY (LB_ID, STATUS, MSG_ID);
IF NOT EXISTS (SELECT 1 FROM sys.indexes WHERE name = 'IDX_M2X_SUBMIT_EXPIRE_1' AND object_id = OBJECT_ID('ODYSSEY'))
CREATE INDEX IDX_M2X_SUBMIT_EXPIRE_1 ON ODYSSEY (LB_ID, SCHEDULE_TIME, MSG_ID);
```
{% endtab %}
{% endtabs %}

## <mark style="color:blue;">로그 테이블(rv-submit-log)의 MSG\_ID 기본 키</mark> <a href="#log-table-pk" id="log-table-pk"></a>

로그 테이블(**`rv-submit-log`** — 기본 `ODYSSEY_LOG`)의 컬럼은 발송 테이블과 같습니다. 다만 **`MSG_ID`** 기본 키(PK)는 버전에 따라 다릅니다.

| 로그 테이블을 만든 버전 | `MSG_ID` 기본 키 |
| -------------- | ------------- |
| 1.0.9 이하       | 있음            |
| 1.0.10 이상      | 없음            |

{% hint style="danger" %}
**Odyssey 1.0.9 까지는 로그 테이블의 `MSG_ID` 가 기본 키(PK)입니다.** 로그 테이블에 같은 **`MSG_ID`** 가 이미 있으면 다음 문제가 발생합니다.

* **1.0.9 이하** : 해당 메시지가 로그 테이블에 들어가지 않고 발송 테이블에서만 삭제됩니다. 오류 로그가 남지 않아 **발송 이력이 유실**됩니다.
* **1.0.10 이상** (기본 키가 남아 있는 로그 테이블) : 해당 메시지가 **`STATUS 9`** 로 발송 테이블에 남고, `[FetchPoller] archive 실패` 경고 로그가 기록됩니다. ([18. MSG\_TYPE / STATUS 코드](../18.-msg_type-status.md#status-9) 참고)
{% endhint %}

1.0.10 부터 새로 만들어지는 로그 테이블에는 기본 키가 없습니다. **이전 버전에서 만들어진 로그 테이블은 자동으로 바뀌지 않으므로**, 아래 SQL 로 기본 키를 삭제해 주세요.

* `ODYSSEY_LOG` 는 실제 로그 테이블 이름으로 바꿔서 실행합니다.
* **`backup`** 설정이 `YEAR` / `MONTHLY` / `DAILY` 이면 1.0.9 이하에서 만들어진 **기간별 로그 테이블마다** 실행합니다. (예: `ODYSSEY_LOG_202610`, `ODYSSEY_LOG_202611`) ([10. DB 설정](../../part-2./10.-db.md) 참고)
  * 로그 테이블은 메시지의 **`SCHEDULE_TIME`** 기준으로 정해집니다. 지난 기간의 로그 테이블에도 메시지가 들어갈 수 있으므로, 현재 기간의 테이블만이 아니라 **DB 에 남아 있는 지난 기간의 로그 테이블도 함께** 실행하세요.
  * 다른 DB 나 다른 이름으로 옮겨 보관 중이어서 Odyssey 가 더 이상 쓰지 않는 테이블은 실행하지 않아도 됩니다.

{% tabs %}
{% tab title="MySQL / MariaDB" %}
```sql
ALTER TABLE ODYSSEY_LOG DROP PRIMARY KEY;
```
{% endtab %}

{% tab title="Oracle" %}
```sql
ALTER TABLE ODYSSEY_LOG DROP PRIMARY KEY;
```
{% endtab %}

{% tab title="PostgreSQL" %}
```sql
-- 기본 키 제약 이름은 "소문자 테이블명_pkey" 입니다.
ALTER TABLE ODYSSEY_LOG DROP CONSTRAINT odyssey_log_pkey;

-- 제약 이름이 다르면 아래 쿼리로 먼저 확인합니다.
SELECT conname FROM pg_constraint
 WHERE conrelid = 'odyssey_log'::regclass AND contype = 'p';
```
{% endtab %}

{% tab title="SQL Server" %}
```sql
-- 기본 키 제약 이름이 자동 생성되므로, 이름을 조회한 뒤 삭제합니다.
DECLARE @pk sysname, @sql nvarchar(400);
SELECT @pk = name FROM sys.key_constraints
 WHERE parent_object_id = OBJECT_ID('ODYSSEY_LOG') AND type = 'PK';
IF @pk IS NOT NULL
BEGIN
    SET @sql = N'ALTER TABLE ODYSSEY_LOG DROP CONSTRAINT ' + QUOTENAME(@pk);
    EXEC sp_executesql @sql;
END
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
**실행 전 확인**

* 데이터가 많은 테이블은 실행에 시간이 걸리거나 테이블이 잠길 수 있습니다. **Odyssey 를 정지한 뒤 발송이 적은 시간에 실행**하고, 실행 후 다시 기동하세요.
* MySQL 8 에서 `sql_require_primary_key=ON` 이면 기본 키가 없는 테이블을 허용하지 않아 기본 키 삭제와 새 로그 테이블 생성이 실패합니다. 해당 옵션을 사용하는 환경은 고객센터로 문의해 주세요.
* 기본 키를 삭제해도 `(MSG_ID, STATUS)` 인덱스는 남아 있어 **`MSG_ID`** 조회 성능은 유지됩니다.
* 기본 키를 삭제한 뒤에는 로그 테이블에 같은 **`MSG_ID`** 행이 2건 이상 있을 수 있습니다.
{% endhint %}
