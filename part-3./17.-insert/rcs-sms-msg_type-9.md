# 17-2. RCS

> 예시 쿼리는 DBMS 별 탭으로 제공합니다. 사용하는 DBMS 의 탭을 선택하세요.
>
> 수신번호(**`RCPT_DATA`**), 발신번호(**`CALLBACK_NUM`**)는 고객사 운영 환경에 맞게 변경하세요.

## <mark style="color:blue;">**1. RCS SMS 발송 (msg\_type=9)**</mark>

{% tabs %}
{% tab title="MySQL" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    9,
    'RCS SMS 발송',
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    '발신번호',
    '수신번호',
    'SS000000',
    '"body":{"description":"RCS 단문 테스트"}',
    '버튼 JSON 내용',
    'N',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="MariaDB" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    9,
    'RCS SMS 발송',
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    '발신번호',
    '수신번호',
    'SS000000',
    '"body":{"description":"RCS 단문 테스트"}',
    '버튼 JSON 내용',
    'N',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="PostgreSQL" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    9,
    'RCS SMS 발송',
    TO_CHAR(NOW(), 'YYYYMMDDHH24MISS'),
    TO_CHAR(NOW(), 'YYYYMMDDHH24MISS'),
    '발신번호',
    '수신번호',
    'SS000000',
    '"body":{"description":"RCS 단문 테스트"}',
    '버튼 JSON 내용',
    'N',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="Oracle" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    9,
    'RCS SMS 발송',
    TO_CHAR(SYSDATE, 'YYYYMMDDHH24MISS'),
    TO_CHAR(SYSDATE, 'YYYYMMDDHH24MISS'),
    '발신번호',
    '수신번호',
    'SS000000',
    '"body":{"description":"RCS 단문 테스트"}',
    '버튼 JSON 내용',
    'N',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="SQL Server" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    9,
    N'RCS SMS 발송',
    FORMAT(GETDATE(), 'yyyyMMddHHmmss'),
    FORMAT(GETDATE(), 'yyyyMMddHHmmss'),
    N'발신번호',
    N'수신번호',
    N'SS000000',
    N'"body":{"description":"RCS 단문 테스트"}',
    N'버튼 JSON 내용',
    N'N',
    N'AGENCYID'
);
```
{% endtab %}
{% endtabs %}

## <mark style="color:blue;">**2. RCS LMS 발송 (msg\_type=10)**</mark>

{% tabs %}
{% tab title="MySQL" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    10,
    'RCS LMS 발송',
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    '발신번호',
    '수신번호',
    'SL000000',
    '"body":{"description":"RCS 장문 테스트"}',
    '버튼 JSON 내용',
    'N',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="MariaDB" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    10,
    'RCS LMS 발송',
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    '발신번호',
    '수신번호',
    'SL000000',
    '"body":{"description":"RCS 장문 테스트"}',
    '버튼 JSON 내용',
    'N',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="PostgreSQL" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    10,
    'RCS LMS 발송',
    TO_CHAR(NOW(), 'YYYYMMDDHH24MISS'),
    TO_CHAR(NOW(), 'YYYYMMDDHH24MISS'),
    '발신번호',
    '수신번호',
    'SL000000',
    '"body":{"description":"RCS 장문 테스트"}',
    '버튼 JSON 내용',
    'N',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="Oracle" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    10,
    'RCS LMS 발송',
    TO_CHAR(SYSDATE, 'YYYYMMDDHH24MISS'),
    TO_CHAR(SYSDATE, 'YYYYMMDDHH24MISS'),
    '발신번호',
    '수신번호',
    'SL000000',
    '"body":{"description":"RCS 장문 테스트"}',
    '버튼 JSON 내용',
    'N',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="SQL Server" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    10,
    N'RCS LMS 발송',
    FORMAT(GETDATE(), 'yyyyMMddHHmmss'),
    FORMAT(GETDATE(), 'yyyyMMddHHmmss'),
    N'발신번호',
    N'수신번호',
    N'SL000000',
    N'"body":{"description":"RCS 장문 테스트"}',
    N'버튼 JSON 내용',
    N'N',
    N'AGENCYID'
);
```
{% endtab %}
{% endtabs %}

## <mark style="color:blue;">**3. RCS MMS 발송 (msg\_type=11) - File ID 자동 치환**</mark>

**`upload` 폴더에 이미지를 저장하고&#x20;**<mark style="color:red;">**`FILE_NAMEn`**</mark>**&#x20;컬럼에 파일명을 지정하면 Odyssey가 자동으로 업로드 후 `R_BODY` 의&#x20;**<mark style="color:red;">**`REPLACE_FILE_NAMEn`**</mark>**&#x20;문자열을 실제 File ID로 치환합니다.**

{% tabs %}
{% tab title="MySQL" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, file_count, file_name1, r_agencyid
) VALUES (
    11,
    'RCS MMS 발송',
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    '발신번호',
    '수신번호',
    'SMwThM00',
    '"body":{"title":"RCS MMS 테스트","description":"RCS MMS
    테스트","media":"maapfile://REPLACE_FILE_NAME1"}',
    '버튼 JSON 내용',
    'N',
    1,
    'test.jpg',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="MariaDB" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, file_count, file_name1, r_agencyid
) VALUES (
    11,
    'RCS MMS 발송',
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    '발신번호',
    '수신번호',
    'SMwThM00',
    '"body":{"title":"RCS MMS 테스트","description":"RCS MMS
    테스트","media":"maapfile://REPLACE_FILE_NAME1"}',
    '버튼 JSON 내용',
    'N',
    1,
    'test.jpg',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="PostgreSQL" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, file_count, file_name1, r_agencyid
) VALUES (
    11,
    'RCS MMS 발송',
    TO_CHAR(NOW(), 'YYYYMMDDHH24MISS'),
    TO_CHAR(NOW(), 'YYYYMMDDHH24MISS'),
    '발신번호',
    '수신번호',
    'SMwThM00',
    '"body":{"title":"RCS MMS 테스트","description":"RCS MMS
    테스트","media":"maapfile://REPLACE_FILE_NAME1"}',
    '버튼 JSON 내용',
    'N',
    1,
    'test.jpg',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="Oracle" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, file_count, file_name1, r_agencyid
) VALUES (
    11,
    'RCS MMS 발송',
    TO_CHAR(SYSDATE, 'YYYYMMDDHH24MISS'),
    TO_CHAR(SYSDATE, 'YYYYMMDDHH24MISS'),
    '발신번호',
    '수신번호',
    'SMwThM00',
    '"body":{"title":"RCS MMS 테스트","description":"RCS MMS
    테스트","media":"maapfile://REPLACE_FILE_NAME1"}',
    '버튼 JSON 내용',
    'N',
    1,
    'test.jpg',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="SQL Server" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, file_count, file_name1, r_agencyid
) VALUES (
    11,
    N'RCS MMS 발송',
    FORMAT(GETDATE(), 'yyyyMMddHHmmss'),
    FORMAT(GETDATE(), 'yyyyMMddHHmmss'),
    N'발신번호',
    N'수신번호',
    N'SMwThM00',
    N'"body":{"title":"RCS MMS 테스트","description":"RCS MMS
    테스트","media":"maapfile://REPLACE_FILE_NAME1"}',
    N'버튼 JSON 내용',
    N'N',
    1,
    N'test.jpg',
    N'AGENCYID'
);
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**파일이 2개, 3개인 경우 `REPLACE_FILE_NAME1` / `REPLACE_FILE_NAME2` / `REPLACE_FILE_NAME3` 을 각각 사용하며, `FILE_NAME1~3` 컬럼에 대응되는 파일명을 저장합니다. 이미지는 발송 실패 시 MMS 대체 발송을 고려하여 최대 3개까지 지원합니다.**
{% endhint %}

## <mark style="color:blue;">**4. RCS TMPL 발송 (msg\_type=12)**</mark>

{% tabs %}
{% tab title="MySQL" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    12,
    'RCS TMPL 발송',
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    '발신번호',
    '수신번호',
    '템플릿ID',
    '"body":{"title":"RCS TMPL 테스트","description":"템플릿 변수에 해당하는 값을
    포함하여 구성"}',
    '버튼 JSON 내용',
    'N',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="MariaDB" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    12,
    'RCS TMPL 발송',
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    '발신번호',
    '수신번호',
    '템플릿ID',
    '"body":{"title":"RCS TMPL 테스트","description":"템플릿 변수에 해당하는 값을
    포함하여 구성"}',
    '버튼 JSON 내용',
    'N',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="PostgreSQL" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    12,
    'RCS TMPL 발송',
    TO_CHAR(NOW(), 'YYYYMMDDHH24MISS'),
    TO_CHAR(NOW(), 'YYYYMMDDHH24MISS'),
    '발신번호',
    '수신번호',
    '템플릿ID',
    '"body":{"title":"RCS TMPL 테스트","description":"템플릿 변수에 해당하는 값을
    포함하여 구성"}',
    '버튼 JSON 내용',
    'N',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="Oracle" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    12,
    'RCS TMPL 발송',
    TO_CHAR(SYSDATE, 'YYYYMMDDHH24MISS'),
    TO_CHAR(SYSDATE, 'YYYYMMDDHH24MISS'),
    '발신번호',
    '수신번호',
    '템플릿ID',
    '"body":{"title":"RCS TMPL 테스트","description":"템플릿 변수에 해당하는 값을
    포함하여 구성"}',
    '버튼 JSON 내용',
    'N',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="SQL Server" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    12,
    N'RCS TMPL 발송',
    FORMAT(GETDATE(), 'yyyyMMddHHmmss'),
    FORMAT(GETDATE(), 'yyyyMMddHHmmss'),
    N'발신번호',
    N'수신번호',
    N'템플릿ID',
    N'"body":{"title":"RCS TMPL 테스트","description":"템플릿 변수에 해당하는 값을
    포함하여 구성"}',
    N'버튼 JSON 내용',
    N'N',
    N'AGENCYID'
);
```
{% endtab %}
{% endtabs %}

### <mark style="color:$primary;">**4-1. CPaaS RCS TMPL (치환 문자 사용)**</mark>

**CPaaS RCS 템플릿 발송 시 치환 변수만&#x20;**<mark style="color:red;">**`R_BODY`**</mark>**&#x20;에 JSON 으로 입력합니다.**

{% tabs %}
{% tab title="MySQL" %}
```sql
-- 템플릿 본문 (사전 등록)
-- 안녕하세요. {{이름}}님, 회원가입이 정상적으로 완료되었습니다.

INSERT INTO ODYSSEY (
    subject, msg_type, schedule_time, submit_time,
    callback_num, rcpt_data, r_body, r_messagebaseid
) VALUES (
    'RCS 테스트',
    12,
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    '발신번호',
    '수신번호',
    '{"이름":"홍길동"}',
    '템플릿코드'
);
```
{% endtab %}

{% tab title="MariaDB" %}
```sql
-- 템플릿 본문 (사전 등록)
-- 안녕하세요. {{이름}}님, 회원가입이 정상적으로 완료되었습니다.

INSERT INTO ODYSSEY (
    subject, msg_type, schedule_time, submit_time,
    callback_num, rcpt_data, r_body, r_messagebaseid
) VALUES (
    'RCS 테스트',
    12,
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    '발신번호',
    '수신번호',
    '{"이름":"홍길동"}',
    '템플릿코드'
);
```
{% endtab %}

{% tab title="PostgreSQL" %}
```sql
-- 템플릿 본문 (사전 등록)
-- 안녕하세요. {{이름}}님, 회원가입이 정상적으로 완료되었습니다.

INSERT INTO ODYSSEY (
    subject, msg_type, schedule_time, submit_time,
    callback_num, rcpt_data, r_body, r_messagebaseid
) VALUES (
    'RCS 테스트',
    12,
    TO_CHAR(NOW(), 'YYYYMMDDHH24MISS'),
    TO_CHAR(NOW(), 'YYYYMMDDHH24MISS'),
    '발신번호',
    '수신번호',
    '{"이름":"홍길동"}',
    '템플릿코드'
);
```
{% endtab %}

{% tab title="Oracle" %}
```sql
-- 템플릿 본문 (사전 등록)
-- 안녕하세요. {{이름}}님, 회원가입이 정상적으로 완료되었습니다.

INSERT INTO ODYSSEY (
    subject, msg_type, schedule_time, submit_time,
    callback_num, rcpt_data, r_body, r_messagebaseid
) VALUES (
    'RCS 테스트',
    12,
    TO_CHAR(SYSDATE, 'YYYYMMDDHH24MISS'),
    TO_CHAR(SYSDATE, 'YYYYMMDDHH24MISS'),
    '발신번호',
    '수신번호',
    '{"이름":"홍길동"}',
    '템플릿코드'
);
```
{% endtab %}

{% tab title="SQL Server" %}
```sql
-- 템플릿 본문 (사전 등록)
-- 안녕하세요. {{이름}}님, 회원가입이 정상적으로 완료되었습니다.

INSERT INTO ODYSSEY (
    subject, msg_type, schedule_time, submit_time,
    callback_num, rcpt_data, r_body, r_messagebaseid
) VALUES (
    N'RCS 테스트',
    12,
    FORMAT(GETDATE(), 'yyyyMMddHHmmss'),
    FORMAT(GETDATE(), 'yyyyMMddHHmmss'),
    N'발신번호',
    N'수신번호',
    N'{"이름":"홍길동"}',
    N'템플릿코드'
);
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**치환 문자가 없는 경우 `R_BODY` 컬럼에 NULL 또는 빈 문자열을 입력합니다. 텍스트/이미지 템플릿 사용 방식은 동일합니다.**
{% endhint %}

## <mark style="color:blue;">**5. RCS ITMPL 발송 (msg\_type=13)**</mark>

{% tabs %}
{% tab title="MySQL" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    13,
    'RCS ITMPL 발송',
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    '발신번호',
    '수신번호',
    '템플릿ID',
    '"body":{"title":"RCS ITMPL 테스트","description":"템플릿 변수에 해당하는
    값을 포함하여 구성"}',
    '버튼 JSON 내용',
    'Y',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="MariaDB" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    13,
    'RCS ITMPL 발송',
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    '발신번호',
    '수신번호',
    '템플릿ID',
    '"body":{"title":"RCS ITMPL 테스트","description":"템플릿 변수에 해당하는
    값을 포함하여 구성"}',
    '버튼 JSON 내용',
    'Y',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="PostgreSQL" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    13,
    'RCS ITMPL 발송',
    TO_CHAR(NOW(), 'YYYYMMDDHH24MISS'),
    TO_CHAR(NOW(), 'YYYYMMDDHH24MISS'),
    '발신번호',
    '수신번호',
    '템플릿ID',
    '"body":{"title":"RCS ITMPL 테스트","description":"템플릿 변수에 해당하는
    값을 포함하여 구성"}',
    '버튼 JSON 내용',
    'Y',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="Oracle" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    13,
    'RCS ITMPL 발송',
    TO_CHAR(SYSDATE, 'YYYYMMDDHH24MISS'),
    TO_CHAR(SYSDATE, 'YYYYMMDDHH24MISS'),
    '발신번호',
    '수신번호',
    '템플릿ID',
    '"body":{"title":"RCS ITMPL 테스트","description":"템플릿 변수에 해당하는
    값을 포함하여 구성"}',
    '버튼 JSON 내용',
    'Y',
    'AGENCYID'
);
```
{% endtab %}

{% tab title="SQL Server" %}
```sql
INSERT INTO ODYSSEY (
    msg_type, subject, submit_time, schedule_time,
    callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
    r_copyallowed, r_agencyid
) VALUES (
    13,
    N'RCS ITMPL 발송',
    FORMAT(GETDATE(), 'yyyyMMddHHmmss'),
    FORMAT(GETDATE(), 'yyyyMMddHHmmss'),
    N'발신번호',
    N'수신번호',
    N'템플릿ID',
    N'"body":{"title":"RCS ITMPL 테스트","description":"템플릿 변수에 해당하는
    값을 포함하여 구성"}',
    N'버튼 JSON 내용',
    N'Y',
    N'AGENCYID'
);
```
{% endtab %}
{% endtabs %}
