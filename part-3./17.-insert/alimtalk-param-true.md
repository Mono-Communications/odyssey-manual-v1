# 카카오 알림톡 - alimtalk-param=true 모드

CPaaS 세션에서 `alimtalk-param=true` 로 설정한 경우, `K_MESSAGE` 컬럼에 치환 변수만 JSON으로 입력합니다.

```sql
-- 템플릿 본문 (사전 등록)
-- #{이름}님, 저희 제품을 구매해주셔서 감사합니다.
-- 문의: #{개별1}

INSERT INTO ODYSSEY (
subject, msg_type, schedule_time, submit_time,
callback_num, rcpt_data, k_message, k_tmplcode, k_adflag
) VALUES (
'카카오 테스트',
6,
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'발신번호',
'수신번호',
'{"이름":"홍길동","개별1":"연구소"}',
'템플릿코드',
'N'
);
```

{% hint style="info" %}
템플릿 본문에 치환 문자가 없으면 `K_MESSAGE` 에 NULL 또는 빈 문자열을 입력합니다.
{% endhint %}
