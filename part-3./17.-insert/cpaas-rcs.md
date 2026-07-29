# CPAAS RCS 템플릿 (치환 문자 사용)

CPaaS RCS 템플릿 발송 시 치환 변수만 `R_BODY` 에 JSON 으로 입력합니다.

```sql
-- 템플릿 본문 (사전 등록)
-- 안녕하세요. {{이름}}님, 회원가입이 정상적으로 완료되었습니다.

INSERT INTO ODYSSEY (
subject, msg_type, schedule_time, submit_time,
callback_num, rcpt_data, r_body, r_messagebaseid
) VALUES (
'RCS 테스트',
12,
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'발신번호',
'수신번호',
'{"이름":"홍길동"}',
'템플릿코드'
);
```

{% hint style="info" %}
치환 문자가 없는 경우 `R_BODY` 컬럼에 NULL 또는 빈 문자열을 입력합니다. 텍스트/이미지 템플릿 사용 방식은 동일합니다.
{% endhint %}
