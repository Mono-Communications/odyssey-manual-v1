---
description: 1차 실패 시 2차, 3차 순차 발송
---

# 17-4. FALLBACK 발송

> **SCHEDULE\_TIME**, **SUBMIT\_TIME**의 포맷은 고객사 DB에 맞게 변경하세요.
>
> **수신번호(RCPT\_DATA)**, **발신번호(CALLBACK\_NUM)**&#xB294; 고객사 운영 환경에 맞게 변경하세요.

1차 발송이 실패한 경우 2차, 3차 발송을 자동으로 시도합니다. `msg_type` / `msg_type_second` / `msg_type_third` 순서로 발송하며, 각 메시지에 필요한 모든 컬럼을 함께 입력하고 `FAIL_SEND` 를 `'Y'`로 설정해야 합니다.

```sql
-- 예) 1차 카카오 알림톡 -> 실패 시 2차 LMS
INSERT INTO ODYSSEY (
msg_type, msg_type_second, subject,
submit_time, schedule_time, message,
callback_num, rcpt_data, fail_send,
k_tmplcode, k_message, k_option
) VALUES (
    6,                                    -- msg_type (1차 발송) : 6 = A_KAKAO
    2,                                    -- msg_type_second (2차 발송) : 2 = LMS
    '제목',                                -- subject (제목)
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),    -- submit_time
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),    -- schedule_time
    'LMS 메시지 내용',                        -- message (본문)
    '발신번호',                            -- callback_num
    '수신번호',                            -- rcpt_data
    'Y',                                    -- fail_send (2차, 3차 발송 사용여부)
    '템플릿코드',                            -- k_tmplcode
    '알림톡 메시지 내용',                    -- k_message
    '버튼(JSON) 내용'                        -- k_option
);
```
