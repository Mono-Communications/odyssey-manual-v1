# MMS 발송 (msg\_type=3)

```sql
INSERT INTO ODYSSEY (
msg_type, submit_time, schedule_time, subject, message,
callback_num, rcpt_data, file_count, file_name1
) VALUES (
3,
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'MMS 발송',
'MMS 테스트 발송입니다.',
'발신번호',
'수신번호',
1,
'test.jpg' -- 첨부파일명 (file-dir 폴더에 사전 저장)
);
```
