# 19. 테이블 레이아웃 (MySQL 기준)

{% hint style="info" %}
해당 내용은 MySQL 기준으로 작성되었습니다. **고객사 별 DBMS에 따라 데이터 타입이 변경**될 수 있으며, 정확한 확인이 필요하면 <mark style="color:red;">**`config/mapper/{{DBMS}}/table.xml`**</mark> 파일을 참고해주세요.
{% endhint %}

Odyssey 최초 기동 시 <mark style="color:green;">**`common.tables.table-name`**</mark> 에 지정된 이름으로 테이블이 자동 생성됩니다. 아래는 발송 테이블(<mark style="color:red;">**`rv-submit`**</mark> — 기본 `ODYSSEY`)의 컬럼 레이아웃입니다.

<table><thead><tr><th width="169.79998779296875">컬럼명</th><th width="171">데이터 타입</th><th width="72.4000244140625">NN</th><th width="90">기본값</th><th>설명</th></tr></thead><tbody><tr><td><strong><code>MSG_ID</code></strong></td><td>BIGINT(20) AUTO_INCREMENT</td><td>Y</td><td></td><td>메시지당 유니크한 번호 (PK)</td></tr><tr><td><strong><code>LB_ID</code></strong></td><td>BIGINT(20)</td><td>Y</td><td>0</td><td>로드밸런싱 ID (HA 분산 처리용)</td></tr><tr><td><strong><code>SUBJECT</code></strong></td><td>VARCHAR(40)</td><td></td><td></td><td>메시지 제목</td></tr><tr><td><strong><code>MSG_TYPE</code></strong></td><td>TINYINT(2)</td><td>Y</td><td></td><td>1차 메시지 구분<br>(<a href="../18.-msg_type-status.md">18. MSG_TYPE / STATUS 코드</a> 참고)</td></tr><tr><td><strong><code>MSG_TYPE_SECOND</code></strong></td><td>TINYINT(2)</td><td>Y</td><td>0</td><td>2차 메시지 구분 (FALLBACK)</td></tr><tr><td><strong><code>MSG_TYPE_THIRD</code></strong></td><td>TINYINT(2)</td><td>Y</td><td>0</td><td>3차 메시지 구분 (FALLBACK)</td></tr><tr><td><strong><code>STATUS</code></strong></td><td>SMALLINT</td><td>0</td><td></td><td>메시지 상태 (<a href="../18.-msg_type-status.md">18. MSG_TYPE / STATUS 코드</a> 참고)</td></tr><tr><td><strong><code>SCHEDULE_TIME</code></strong></td><td>VARCHAR(16)</td><td>Y</td><td></td><td>발송 시작 시각 (YYYYMMDDHH24MISS)</td></tr><tr><td><strong><code>SUBMIT_TIME</code></strong></td><td>VARCHAR(16)</td><td>Y</td><td></td><td>메시지 등록 시각 (YYYYMMDDHH24MISS)</td></tr><tr><td><strong><code>MESSAGE</code></strong></td><td>TEXT</td><td></td><td></td><td>메시지 내용</td></tr><tr><td><strong><code>CALLBACK_NUM</code></strong></td><td>VARCHAR(20)</td><td>Y</td><td></td><td>회신번호 (특수문자 제외)</td></tr><tr><td><strong><code>RCPT_DATA</code></strong></td><td>VARCHAR(20)</td><td>Y</td><td></td><td>수신번호 (특수문자 제외)</td></tr><tr><td><strong><code>FILE_COUNT</code></strong></td><td>TINYINT(1)</td><td></td><td>0</td><td>MMS 첨부 파일 개수</td></tr><tr><td><strong><code>FILE_NAME1</code></strong></td><td>VARCHAR(128)</td><td></td><td></td><td>첨부 파일 1</td></tr><tr><td><strong><code>FILE_NAME2</code></strong></td><td>VARCHAR(128)</td><td></td><td></td><td>첨부 파일 2</td></tr><tr><td><strong><code>FILE_NAME3</code></strong></td><td>VARCHAR(128)</td><td></td><td></td><td>첨부 파일 3</td></tr><tr><td><strong><code>HEADER</code></strong></td><td>TINYINT(1)</td><td></td><td></td><td>CPAAS HEADER (광고 표기)</td></tr><tr><td><strong><code>FOOTER</code></strong></td><td>VARCHAR(20)</td><td></td><td></td><td>CPAAS FOOTER (수신거부 번호)</td></tr><tr><td><strong><code>CDR_ID</code></strong></td><td>VARCHAR(20)</td><td></td><td></td><td>과금 ID</td></tr><tr><td><strong><code>RESULT</code></strong></td><td>MEDIUMINT(6)</td><td></td><td>성공 : 0</td><td>전송 결과 코드 (SMS/LMS/MMS/VMS)</td></tr><tr><td><strong><code>RCS_RESULT</code></strong></td><td>MEDIUMINT(6)</td><td></td><td></td><td>전송 결과 코드 (RCS)</td></tr><tr><td><strong><code>KKO_RESULT</code></strong></td><td>MEDIUMINT(6)</td><td></td><td></td><td>전송 결과 코드 (KAKAO)</td></tr><tr><td><strong><code>RESULT_DESC</code></strong></td><td>VARCHAR(200)</td><td></td><td></td><td>결과코드 상세 내용</td></tr><tr><td><strong><code>DELIVER_TIME</code></strong></td><td>VARCHAR(16)</td><td></td><td></td><td>전송 시각 (마지막 발송)</td></tr><tr><td><strong><code>REPORT_RECV_TIME</code></strong></td><td>VARCHAR(16)</td><td></td><td></td><td>리포트 수신 시각</td></tr><tr><td><strong><code>TELCOINFO</code></strong></td><td>VARCHAR(4)</td><td></td><td></td><td>수신자 이통사 정보</td></tr><tr><td><strong><code>FAIL_SEND</code></strong></td><td>VARCHAR(1)</td><td></td><td>'N'</td><td>실패 재발송(FALLBACK) 여부 (Y/N)</td></tr><tr><td><strong><code>K_TMPLCODE</code></strong></td><td>VARCHAR(30)</td><td></td><td></td><td>알림톡 템플릿 코드</td></tr><tr><td><strong><code>K_MESSAGE</code></strong></td><td>TEXT</td><td></td><td></td><td>알림톡 메시지 내용</td></tr><tr><td><strong><code>K_OPTION</code></strong></td><td>TEXT</td><td></td><td></td><td>알림톡 button 등 옵션(JSON)<br>- alimtalk-param : false 일 때</td></tr><tr><td><strong><code>K_SERIAL_NM</code></strong></td><td>VARCHAR(40)</td><td></td><td></td><td>알림톡 시리얼명</td></tr><tr><td><strong><code>K_ADFLAG</code></strong></td><td>VARCHAR(1)</td><td></td><td>'N'</td><td>알림톡 광고 문구 여부 (Y/N)</td></tr><tr><td><strong><code>K_SENDERKEY</code></strong></td><td>VARCHAR(40)</td><td></td><td></td><td>알림톡 발신 프로필 키</td></tr><tr><td><strong><code>R_MESSAGEBASEID</code></strong></td><td>VARCHAR(40)</td><td></td><td></td><td>RCS messageBaseId</td></tr><tr><td><strong><code>R_BODY</code></strong></td><td>TEXT</td><td></td><td></td><td>RCS body (JSON)</td></tr><tr><td><strong><code>R_BUTTON</code></strong></td><td>TEXT</td><td></td><td></td><td>RCS button (JSON)</td></tr><tr><td><strong><code>R_HEADER</code></strong></td><td>TINYINT(1)</td><td></td><td></td><td>RCS 광고 문구 여부 (0/1)</td></tr><tr><td><strong><code>R_FOOTER</code></strong></td><td>VARCHAR(20)</td><td></td><td></td><td>RCS 수신거부 번호 (R_HEADER=1 시 필수)</td></tr><tr><td><strong><code>R_COPYALLOWED</code></strong></td><td>VARCHAR(1)</td><td></td><td>'N'</td><td>RCS 메시지 복사 허용 여부 (Y/N)</td></tr><tr><td><strong><code>R_QUERYID</code></strong></td><td>VARCHAR(60)</td><td></td><td></td><td>RCS 리포트 요청 queryId</td></tr><tr><td><strong><code>RESERVED01</code></strong></td><td>VARCHAR(60)</td><td></td><td></td><td>예약 필드 1</td></tr><tr><td><strong><code>RESERVED02</code></strong></td><td>VARCHAR(60)</td><td></td><td></td><td>예약 필드 2</td></tr><tr><td><strong><code>RESERVED03</code></strong></td><td>VARCHAR(60)</td><td></td><td></td><td>예약 필드 3</td></tr><tr><td><strong><code>KISA_ORIG_CODE</code></strong></td><td>VARCHAR(9)</td><td></td><td></td><td>KISA 코드</td></tr><tr><td><strong><code>R_AGENCYID</code></strong></td><td>VARCHAR(60)</td><td></td><td></td><td>RCS agencyId</td></tr><tr><td><strong><code>R_AGENCYKEY</code></strong></td><td>VARCHAR(256)</td><td></td><td></td><td>RCS agencyKey</td></tr><tr><td><strong><code>R_BRANDKEY</code></strong></td><td>VARCHAR(256)</td><td></td><td></td><td>RCS brandKey</td></tr><tr><td><strong><code>R_CDR_ID</code></strong></td><td>VARCHAR(20)</td><td></td><td></td><td>RCS 과금 ID</td></tr><tr><td><strong><code>TRACKING_ID</code></strong></td><td>VARCHAR(40)</td><td></td><td></td><td>리포트 요청 TRACKING ID</td></tr><tr><td><strong><code>TOKEN</code></strong></td><td>VARCHAR(100)</td><td></td><td></td><td>리포트 요청 TOKEN</td></tr><tr><td><strong><code>C_STATUS</code></strong></td><td>VARCHAR(1)</td><td></td><td></td><td>CPaaS 전송 결과 STATUS</td></tr><tr><td><strong><code>SUB_KEY</code></strong></td><td>VARCHAR(100)</td><td></td><td></td><td>CPAAS 부서/과금 분리 코드</td></tr><tr><td><strong><code>GSMS_TYPE</code></strong></td><td>TINYINT(1)</td><td></td><td>0</td><td>GSMS 문자열 타입<br>0 : unicode / 1 : text</td></tr></tbody></table>

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
* **`backup`** 설정이 `YEAR` / `MONTHLY` / `DAILY` 이면 로그 테이블(예: `ODYSSEY_LOG_202611`)마다 실행합니다. ([10. DB 설정](../../part-2./10.-db.md) 참고)

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
