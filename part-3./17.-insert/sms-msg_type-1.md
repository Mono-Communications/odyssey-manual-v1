# 17-1. Legacy

> **`SCHEDULE_TIME`**, **`SUBMIT_TIME`**&#xC758; 포맷은 고객사 DB에 맞게 변경하세요.
>
> 수신번호(**`RCPT_DATA`**), 발신번호(**`CALLBACK_NUM`**)는 고객사 운영 환경에 맞게 변경하세요.

## <mark style="color:blue;">1. SMS 발송 (msg\_type=1)</mark>

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

## <mark style="color:blue;">2. LMS 발송 (msg\_type=2)</mark>

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

## <mark style="color:blue;">3. MMS 발송 (msg\_type=3)</mark>

MMS는 **최대 3개의 파일**을 첨부할 수 있습니다.

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

{% hint style="info" %}
<mark style="color:$primary;">**첨부 파일 저장 경로 :**</mark> <mark style="color:red;">**`application.yml`**</mark> 의 <mark style="color:green;">`file-dir`</mark> 에 설정된 로컬 주소. DB에 insert한 **`FILE_NAMEn`** 과 실제 파일명이 같아야 합니다.
{% endhint %}

## <mark style="color:blue;">4. VMS 발송 (msg\_type=4)</mark>

* VMS는 음성 파일을 직접 첨부하는 방식과 TTS convert로 보내는 방식으로 나뉩니다.
* VMS는 **KT 크로샷**으로만 발송 가능하며, **2차/3차 발송은 없습니다**.
  * msg\_type\_second, msg\_type\_third : 0
  * fail\_send : 'N'

### 발송 우선순위

1. <mark style="color:$primary;background-color:$info;">**첨부 파일**</mark><mark style="background-color:$info;">이 있을 때</mark> — 음성 파일 첨부 방식
2. **첨부 파일이 없고** & <mark style="color:$primary;background-color:$info;">**message(content)**</mark><mark style="background-color:$info;">가 있을 때</mark> — TTS convert 방식
3. 첨부 파일이 없고, message도 없을 때 — 오류 발생

### 4-1. 음성 파일 첨부 방식

VMS는 **최대 1개의 파일**을 첨부할 수 있습니다. (2개 이상 첨부 시, 1개만 전송)

{% hint style="danger" %}
파일을 2개 이상 첨부할 경우 더 먼저 insert 된(**`FILE_NAMEn`** index가 더 낮은)파일 1개만 발송 처리되지만, 메모리 누수가 발생할 수 있으므로 **`FILE_NAMEn` 에는 반드시 1개의 파일만 insert 하는 것을 권장**합니다.
{% endhint %}

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
    'file.wav',                     -- 첨부파일명 (file-dir 폴더에 사전 저장)
    'N'                                -- fail_send(2,3차 발송) 없음
);
```

{% hint style="info" %}
<mark style="color:$primary;">**첨부 파일 저장 경로 :**</mark> <mark style="color:red;">**`application.yml`**</mark> 의 <mark style="color:green;">`file-dir`</mark> 에 설정된 로컬 주소. DB에 insert한 **`FILE_NAMEn`** 과 실제 파일명이 같아야 합니다.
{% endhint %}

{% hint style="warning" %}
음성 파일 전송 방식으로 VMS를 발송 시도 할 때 반드시 **`FILE_NAMEn`**&#xC774; 존재해야 합니다. **`FILE_NAMEn` 이 모두 null 혹은 공백**이면 자동으로 TTS convert 방식으로 발송을 시도하며 **VMS 발송에 실패**할 수 있습니다.
{% endhint %}

### 4-2. TTS convert 방식

TTS로 변환할 음성 메시지 내용을 **`message`** 컬럼에 입력해주세요. **`message`** 컬럼의 값이 비어있을 경우 VMS 발송에 실패합니다.

```sql
INSERT INTO ODYSSEY (
    msg_type, submit_time, schedule_time, subject, message,
    callback_num, rcpt_data, file_count, file_name1, fail_send
) VALUES (
    4,
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    'VMS 발송',
    'VMS TTS convert 방식 테스트입니다.', -- message 내용 있어야 함
    '발신번호',
    '수신번호',
    0,
    '',                                 -- 첨부파일 없어야 함
    'N'                                -- fail_send(2,3차 발송) 없음
);
```

{% hint style="warning" %}
TTS convert 방식으로 VMS를 발송할 때 **`FILE_NAMEn`** 이 모두 null 혹은 공백이어야 합니다. **`FILE_NAMEn` 에 값이 있을 경우** 자동으로 음성 파일 발송을 시도하며 **VMS 발송에 실패**할 수 있습니다.
{% endhint %}

## <mark style="color:blue;">5. GSMS 발송 (msg\_type=22)</mark>

* GSMS는 **커뮤니즈**로만 발송 가능하며, **2차/3차 발송은 없습니다**.
  * msg\_type\_second, msg\_type\_third : 0
  * fail\_send : 'N'
* GSMS는 발송 완료 여부만 확인 가능하며, **수신자의 수신 여부를 확인할 수 없습니다**.

```sql
insert into odyssey (
    msg_type, message, schedule_time, submit_time,
    reserved01, callback_num, reserved02, rcpt_data,
    fail_send, gsms_type)
values (
    22,
    '[MonoComm] This is an international character test. GSMS Test.',
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    '82',                -- RESERVED01 : 발송번호 국가코드
    '15777223',          -- 발송번호
    '84',                -- RESERVED02 : 수신번호 국가코드
    '84982609007',       -- 수신번호 : RESERVED02 값과 무관하게 국가코드 + 발송번호 형식
    'N',
    0                    -- GSMS_TYPE : GSMS 문자열 타입 (0: unicode / 1: text)
);
```

{% hint style="danger" %}
<mark style="color:green;">**`RCPT_DATA`**</mark> 의 형식

* 수신번호는 <mark style="color:green;">`RESERVED02`</mark> (수신번호 국가코드) 컬럼 값과 무관하게 국가코드 + 발송번호 형식으로 입력해야 합니다.
  * **\[예시]** 한국(국가코드) 번호 '010-1234-5678' 로 전송할 경우
    * 국가코드 : +82 / 전화번호 : 010-1234-5678 **(국가 불문 첫 '0'은 생략)**
    * <mark style="color:green;">**`RCPT_DATA`**</mark> : **821012345678** (82 + 1012345678)
{% endhint %}

{% hint style="info" %}
GSMS 는 실발송번호가 아닌, <mark style="color:green;">`RESERVED01`</mark> 을 기준으로 대체되는 **sender-id** 값으로 전송됩니다. sender-id 값은 발송하는 고객사 등에 따라 상이하며 sender-id 값은 <mark style="color:red;">**`senderId.yml`**</mark> 에 세팅하여 사용합니다. (참고 [8-1. senderId.yml](../../part-2./8./8-1.-senderid.yml.md))
{% endhint %}
