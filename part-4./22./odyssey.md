# Odyssey 로그 파일 구성

Odyssey의 로그는 `log/` 폴더에 출력되며, 일별로 압축되어 `log_backup/` 폴더에 보관됩니다. 주요 로그 파일은 다음과 같습니다.

| 로그 파일                                  | 내용                                                        |
| -------------------------------------- | --------------------------------------------------------- |
| agent.log                              | **전체 로그(catch-all)** — 모든 서비스 모듈 + HA 모듈 + Spring/DB 등 전반 |
| error.log                              | 에러 전용 로그 (장애 발생 시 우선 확인)                                  |
| router.log                             | Router 모듈 — 메시지 라우팅, 채널 분기                                |
| collect.log                            | Collector 모듈 — KT/RCS/카카오 수집 결과                           |
| send\_kt.log                           | KT 크로샷 발송 (SMS/LMS/MMS, legacy socket)                    |
| send\_rcs.log                          | KT RCS Hermes 발송                                          |
| send\_kko.log                          | 카카오 알림톡/친구톡 발송                                            |
| report.log                             | 리포트 처리 (수신 결과 콜백)                                         |
| cpaas.log                              | CPaaS API 발송/리포트 (legacy/kakao/rcs)                       |
| odyssey-app.out / odyssey-pipeline.out | JVM 콘솔 안전망 — Spring 부트 init, JVM 크래시 등 logback이 못 잡는 출력   |

{% hint style="info" %}
`agent.log`는 모든 모듈 로그를 통합해서 받는 전체 로그입니다. 특정 채널/모듈만 추적하고 싶을 땐 모듈별 파일을 참고하세요. 로그 파일 명은 logback 설정에 따라 환경별로 다를 수 있습니다. 정확한 파일명은 운영 환경의 `log/` 폴더를 확인하시기 바랍니다.
{% endhint %}
