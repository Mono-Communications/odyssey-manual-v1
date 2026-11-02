# 17-3. 카카오

> **`SCHEDULE_TIME`**, **`SUBMIT_TIME`**&#xC758; 포맷은 고객사 DB에 맞게 변경하세요.
>
> 수신번호(**`RCPT_DATA`**), 발신번호(**`CALLBACK_NUM`**)는 고객사 운영 환경에 맞게 변경하세요.

## <mark style="color:blue;">DBMS 별 DATE\_FORMAT</mark>

예시 쿼리는 MySQL 기준으로 작성되었습니다. 고객사 DBMS 별 <mark style="color:green;">**`schedule_time`**</mark>, <mark style="color:green;">**`submit_time`**</mark> 등의 컬럼에 대하여 insert 쿼리가 달라질 수 있습니다. 해당 포맷 설명을 참고하세요.

<table><thead><tr><th width="301">DBMS 종류</th><th>DATE_FORMAT</th></tr></thead><tbody><tr><td>MySQL, MariaDB</td><td><code>DATE_FORMAT(NOW(), '%Y%m%d%H%i%s')</code></td></tr><tr><td>Oracle, PostgreSQL</td><td><code>TO_CHAR(SYSDATE, 'YYYYMMDDHH24MISS')</code></td></tr><tr><td>SQL Server</td><td><code>FORMAT(GETDATE(), 'yyyyMMddHHmmss')</code></td></tr></tbody></table>

## alimtalk-param : true

* 파라미터 치환 값만 입력
  * 템플릿 사용 시 button 등 옵션 값의 치환 값도 모두 **`k_message`** 에 입력

### <mark style="color:blue;">카카오 알림톡 발송 (msg\_type=6)</mark>

```sql
INSERT INTO ODYSSEY (
    msg_type, submit_time, schedule_time, subject,
    callback_num, rcpt_data, k_tmplcode, k_message
) VALUES (
    6,
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    '카카오 알림톡 테스트',
    '발신번호',
    '수신번호',
    '템플릿코드',
    '{"개별1":"홍길동","버튼링크":"mono.co.kr"}'    -- 파라미터값 key:value 형식으로 입력
);
```

### <mark style="color:blue;">카카오 알림톡 이미지 발송 (msg\_type=8)</mark>

* image url 별도로 입력하지 않음

```sql
INSERT INTO ODYSSEY (
    msg_type, submit_time, schedule_time, subject,
    callback_num, rcpt_data, k_tmplcode, k_message, k_option
) VALUES (
    8,
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    '카카오 알림톡 테스트',
    '발신번호',
    '수신번호',
    '템플릿코드',
    '{"개별1":"홍길동","버튼링크":"mono.co.kr"}'    -- 파라미터값 key:value 형식으로 입력
);
```

## alimtalk-param : false

* 템플릿 사용 시 내용 전부 입력
  * 템플릿 내용과 입력 내용이 모두 동일해야 하며, 치환값을 내용에 포함하여 입력하면 자동 치환됨
* 버튼 등 옵션 값의 치환 값은 **`k_option`**&#xC5D0; 별도 입력

### <mark style="color:blue;">카카오 알림톡 발송 (msg\_type=6)</mark>

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
    '안녕하세요 홍길동님, 모노커뮤니케이션즈에 가입해주셔서 감사합니다.',
    '{
  "button": [
    {
      "name": "모노커뮤니케이션즈 홈페이지",
      "type": "WL",
      "url_mobile": "http://mono.co.kr",
      "url_pc": "http://mono.co.kr"
    }
  ]
}'
);
```

### <mark style="color:blue;">카카오 알림톡 이미지 발송 (msg\_type=8)</mark>

* image url 별도로 입력하지 않음

```sql
INSERT INTO ODYSSEY (
    msg_type, submit_time, schedule_time, subject,
    callback_num, rcpt_data, k_tmplcode, k_message, k_option
) VALUES (
    8,
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

{% hint style="info" %}
치환 값 입력이 템플릿과 일치하지 않는 경우 해당 치환 문자열은 치환되지 않은 채 key값으로 발송됩니다.

ex. '안녕하세요 #{개별1}님, 모노커뮤니케이션즈에 가입해주셔서 감사합니다.'
{% endhint %}

{% hint style="warning" %}
단, 버튼 등 옵션 값의 치환 값이 일치하지 않는 경우 에러가 발생합니다. (errorCode=1030)
{% endhint %}



### <mark style="color:$primary;">강조표기 / 아이템 하이라이트 작성</mark>

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
