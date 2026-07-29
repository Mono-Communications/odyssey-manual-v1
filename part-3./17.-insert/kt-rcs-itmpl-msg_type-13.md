# KT RCS ITMPL 발송 (msg\_type=13)

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
