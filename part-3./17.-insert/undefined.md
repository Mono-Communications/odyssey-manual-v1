# 카카오 알림톡 강조표기 / 아이템 하이라이트 작성

`K_OPTION` 컬럼에 JSON 형식으로 입력합니다.

```json
// 강조 표기
{"attachment":{"title":"강조 표기"}}

// 강조 표기 + 버튼
{"attachment":{"button":[{"name":"버튼
이름","type":"AC"}],"title":"강조 표기"}}

// 아이템 하이라이트
{"attachment":{"button":[{"name":"채널
추가","type":"AC"}],
"itemHighlight":{"title":"메시지 전송","description":"아이템리스트형
테스트"},
"item":{"list":[{"title":"등록일시","description":"20240801"},
{"title":"전송결과","description":"#{변수1}"}]}}}
```
