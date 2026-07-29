# 카카오 알림톡 발송 (msg\_type=6)

```sql
INSERT INTO ODYSSEY (
msg_type, submit_time, schedule_time, subject,
callback_num, rcpt_data, k_tmplcode, k_message, k_option
) VALUES (
6,
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'카카오 알림톡 테스트',
'발신번호',
'수신번호',
'템플릿코드',
'알림톡 메시지 내용',
'버튼(JSON) 내용'
);
```
