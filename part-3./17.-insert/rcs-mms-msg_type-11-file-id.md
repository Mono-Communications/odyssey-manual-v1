# RCS MMS 발송 (msg\_type=11) - File ID 자동 치환

`upload` 폴더에 이미지를 저장하고 `FILE_NAMEn` 컬럼에 파일명을 지정하면 Odyssey가 자동으로 업로드 후 `R_BODY` 의 `REPLACE_FILE_NAMEn` 문자열을 실제 File ID로 치환합니다.

```sql
INSERT INTO ODYSSEY (
msg_type, subject, submit_time, schedule_time,
callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
r_copyallowed, file_count, file_name1, r_agencyid
) VALUES (
11,
'RCS MMS 발송',
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'발신번호',
'수신번호',
'SMwThM00',
'"body":{"title":"RCS MMS 테스트","description":"RCS MMS
테스트","media":"maapfile://REPLACE_FILE_NAME1"}',
'버튼 JSON 내용',
'N',
1,
'test.jpg',
'AGENCYID'
);
```

{% hint style="info" %}
파일이 2개, 3개인 경우 `REPLACE_FILE_NAME1` / `REPLACE_FILE_NAME2` / `REPLACE_FILE_NAME3` 을 각각 사용하며, `FILE_NAME1~3` 컬럼에 대응되는 파일명을 저장합니다. 이미지는 발송 실패 시 MMS 대체발송을 고려하여 최대 3개까지 지원합니다.
{% endhint %}
