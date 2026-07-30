# 17-1. KT Xroshot

> **SCHEDULE\_TIME**, **SUBMIT\_TIME**의 포맷은 고객사 DB에 맞게 변경하세요.
>
> **수신번호(RCPT\_DATA)**, **발신번호(CALLBACK\_NUM)**&#xB294; 고객사 운영 환경에 맞게 변경하세요.

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

* VMS는 음성 파일을 직접 첨부하는 방식과 TTS convert로 보내는 방식으로 나뉩니다.
* VMS는 **KT 크로샷**으로만 발송 가능하며, 따라서 **2차/3차 발송은 없습니다**.
  * msg\_type\_second, msg\_type\_third : 0
  * fail\_send : 'N'

### 발송우선순위

1. **첨부 파일이 있을 때** — 음성 파일 첨부 방식
2. 첨부 파일이 없고, **message(content)가 있을 때** — TTS convert 방식
3. 첨부 파일이 없고, message도 없을 때 — 오류 발생

### 4-1. 음성 파일 첨부 방식

```sql
INSERT INTO ODYSSEY (
msg_type, submit_time, schedule_time, subject, message,
callback_num, rcpt_data, file_count, file_name1, fail_send
) VALUES (
    4,
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    'VMS 발송',
    '',                                -- message : 내용 유무 상관 없음
    '발신번호',
    '수신번호',
    1,                                -- 첨부파일 있어야 함
    'voice.mp3',                     -- 첨부파일명 (file-dir 폴더에 사전 저장)
    'N'                                -- fail_send(2,3차 발송) 없음
);
```

### 4-2. TTS convert 방식

```sql
INSERT INTO ODYSSEY (
msg_type, submit_time, schedule_time, subject, message,
callback_num, rcpt_data, file_count, file_name1, fail_send
) VALUES (
    4,
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    'VMS 발송',
    'VMS TTS convert 방식 테스트입니다.' -- message 내용 있어야 함
    '발신번호',
    '수신번호',
    0,                                -- 첨부파일 없어야 함
    '',                             
    'N'                                -- fail_send(2,3차 발송) 없음
);
```
