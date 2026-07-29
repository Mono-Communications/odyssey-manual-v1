---
description: Odyssey 자체에서 발생하는 내부 에러 코드입니다.
---

# Odyssey 내부 에러 코드

| CODE | CONTENT                 | 설명                          |
| ---- | ----------------------- | --------------------------- |
| 16   | Time out                | 발송 시간이 지난 메시지 (limit 옵션 참고) |
| 34   | Blank MsgType           | 메시지 타입 오류                   |
| 35   | Blank Number            | 수/발신 번호 비어있음                |
| 36   | cdr\_id Invalid Token   | 과금 정보 매칭 실패                 |
| 90   | SPAM Message            | 발송 금지 시간에 인입되어 자동 실패 처리됨    |
| 91   | Invalid File Extension  | 파일 형식 오류 (jpg/JPG 외)        |
| 92   | Different Content Count | 파일 개수 또는 파일 이름 오류           |
| 93   | Attached File Error     | 업로드 대상 첨부파일이 없거나 에러 상태      |
| 94   | File Upload Time out    | 파일 업로드 60초 이상 결과 없음         |
| 96   | IOException             | 입출력 작업 중 예외 발생              |
| 97   | NullPointerException    | Null 호출 예외 발생               |
| 98   | SQLException            | DB 예외 발생                    |
| 99   | Exception               | 기타 예외 발생                    |
| 403  | BlockedNumber           | 차단된 번호                      |
| 9998 | AgentStop               | Odyssey 종료                  |
| -92  | ImageDownload Failed    | 파일 다운로드 실패                  |
