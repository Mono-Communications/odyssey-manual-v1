# RCS LMS 발송 (msg\_type=10)

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
