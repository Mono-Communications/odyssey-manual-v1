# SMS 발송 (msg\_type=1)

```sql
INSERT INTO ODYSSEY (
msg_type, submit_time, schedule_time, message, callback_num, rcpt_data
) VALUES (
1,
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'SMS 테스트 발송입니다.',
'발신번호',
'수신번호'
);
```
