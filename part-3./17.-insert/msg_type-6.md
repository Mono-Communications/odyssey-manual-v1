# 17-3. 카카오

> **`SCHEDULE_TIME`**, **`SUBMIT_TIME`**&#xC758; 포맷은 고객사 DB에 맞게 변경하세요.
>
> 수신번호(**`RCPT_DATA`**), 발신번호(**`CALLBACK_NUM`**)는 고객사 운영 환경에 맞게 변경하세요.

## <mark style="color:blue;">카카오 알림톡 발송 (msg\_type=6)</mark>

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



### <mark style="color:purple;">강조표기 / 아이템 하이라이트 작성</mark>

<mark style="color:red;">**`K_OPTION`**</mark> 컬럼에 JSON 형식으로 입력합니다.

```json
// 강조 표기
{
"attachment":
    {"title":"강조 표기"}
}

// 강조 표기 + 버튼
{
"attachment":
    {
    "button":[{
                "name":"버튼 이름",
                "type":"AC"
              }],
              "title":"강조 표기"
    }
}

// 아이템 하이라이트
{
"attachment":
    {
    "button":[{
                "name":"채널추가",
                "type":"AC"
              }],
    "itemHighlight":{
                     "title":"메시지 전송",
                     "description":"아이템리스트형 테스트"
                    },
    "item":{
            "list":[{
                     "title":"등록일시",
                     "description":"20240801"
                    },
                    {
                     "title":"전송결과",
                     "description":"#{변수1}"
                    }]
           }
     }
}
```



### <mark style="color:purple;">alimtalk-param=true 모드</mark>

CPaaS 세션에서 **`alimtalk-param=`**<mark style="color:green;">**`true`**</mark> 로 설정한 경우, <mark style="color:red;">**`K_MESSAGE`**</mark> 컬럼에 치환 변수만 JSON으로 입력합니다.

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
템플릿 본문에 치환 문자가 없으면 <mark style="color:red;">**`K_MESSAGE`**</mark> 에 NULL 또는 빈 문자열을 입력합니다.
{% endhint %}
