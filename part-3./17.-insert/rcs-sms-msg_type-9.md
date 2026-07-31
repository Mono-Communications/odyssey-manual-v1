# 17-2. RCS

> **`SCHEDULE_TIME`**, **`SUBMIT_TIME`**&#xC758; 포맷은 고객사 DB에 맞게 변경하세요.
>
> 수신번호(**`RCPT_DATA`**), 발신번호(**`CALLBACK_NUM`**)는 고객사 운영 환경에 맞게 변경하세요.

## <mark style="color:blue;">**1. RCS SMS 발송 (msg\_type=9)**</mark>

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

## <mark style="color:blue;">**2. RCS LMS 발송 (msg\_type=10)**</mark>

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

## <mark style="color:blue;">**3. RCS MMS 발송 (msg\_type=11) - File ID 자동 치환**</mark>

**`upload` 폴더에 이미지를 저장하고&#x20;**<mark style="color:red;">**`FILE_NAMEn`**</mark>**&#x20;컬럼에 파일명을 지정하면 Odyssey가 자동으로 업로드 후 `R_BODY` 의&#x20;**<mark style="color:red;">**`REPLACE_FILE_NAMEn`**</mark>**&#x20;문자열을 실제 File ID로 치환합니다.**

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

{% hint style="info" %}
**파일이 2개, 3개인 경우 `REPLACE_FILE_NAME1` / `REPLACE_FILE_NAME2` / `REPLACE_FILE_NAME3` 을 각각 사용하며, `FILE_NAME1~3` 컬럼에 대응되는 파일명을 저장합니다. 이미지는 발송 실패 시 MMS 대체 발송을 고려하여 최대 3개까지 지원합니다.**
{% endhint %}

## <mark style="color:blue;">**4. RCS TMPL 발송 (msg\_type=12)**</mark>

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

### <mark style="color:purple;">**4-1. CPaaS RCS TMPL (치환 문자 사용)**</mark>

**CPaaS RCS 템플릿 발송 시 치환 변수만&#x20;**<mark style="color:red;">**`R_BODY`**</mark>**&#x20;에 JSON 으로 입력합니다.**

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

{% hint style="info" %}
**치환 문자가 없는 경우 `R_BODY` 컬럼에 NULL 또는 빈 문자열을 입력합니다. 텍스트/이미지 템플릿 사용 방식은 동일합니다.**
{% endhint %}

## <mark style="color:blue;">**5. RCS ITMPL 발송 (msg\_type=13)**</mark>

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
