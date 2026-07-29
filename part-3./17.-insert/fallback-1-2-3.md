# FALLBACK 발송 (1차 실패 시 2차/3차 순차 발송)

1차 발송이 실패한 경우 2차, 3차 발송을 자동으로 시도합니다. `msg_type` / `msg_type_second` / `msg_type_third` 가 발송 순서이며, 각 메시지에 필요한 모든 컬럼을 함께 입력하고 `FAIL_SEND` 를 `'Y'`로 설정해야 합니다.

```sql
-- 예) 1차 카카오 알림톡 -> 실패 시 2차 LMS
INSERT INTO ODYSSEY (
msg_type, msg_type_second, subject,
submit_time, schedule_time, message,
callback_num, rcpt_data, fail_send,
k_tmplcode, k_message, k_option
) VALUES (
6,
2,
'제목',
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'LMS 메시지 내용',
'발신번호',
'수신번호',
'Y',
'템플릿코드',
'알림톡 메시지 내용',
'버튼(JSON) 내용'
);
```
