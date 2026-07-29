# 17-1. KT Xroshot

> **SCHEDULE\_TIME**, **SUBMIT\_TIME**의 포맷은 고객사 DB에 맞게 변경하세요.
>
> **수신번호(RCPT\_DATA)**, 발**신번호(CALLBACK\_NUM)**&#xB294; 고객사 운영 환경에 맞게 변경하세요.

## 1. SMS 발송 (msg\_type=1)

```sql
INSERT INTO ODYSSEY (
    MSG_TYPE, SCHEDULE_TIME, SUBMIT_TIME, MESSAGE, CALLBACK_NUM, RCPT_DATA
) VALUES (
    1,                              -- 1 = SMS
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    '[테스트] Odyssey 첫 발송 성공!',
    '0212345678',                   -- 발신번호 (특수문자 제외)
    '01012345678'                   -- 수신번호 (특수문자 제외)
);
```



## 2. LMS 발송 (msg\_type=2)

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



## 3. MMS 발송 (msg\_type=3)

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



## 4. VMS 발송 (msg\_type=4)

### 4-1. TTS convert 방식

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

### 4-2. 음성 파일 첨부 방식
