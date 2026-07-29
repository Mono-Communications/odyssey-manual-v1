# LMS 발송 (msg\_type=2)

```sql
INSERT INTO ODYSSEY (
msg_type, submit_time, schedule_time, subject, message, callback_num, rcpt_data
) VALUES (
2,
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'LMS 발송',
'LMS 테스트 발송입니다.',
'발신번호',
'수신번호'
);
```
