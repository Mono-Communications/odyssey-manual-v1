# RCS SMS 발송 (msg\_type=9)

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
