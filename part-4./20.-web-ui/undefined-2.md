# 20-1. 모니터링

**Odyssey**의 실시간 발송 상태와 발송 통계를 시각적으로 확인하는 대시보드입니다.

### <mark style="color:blue;">실시간 발송 현황</mark>

* **파이프라인 시각화**: DB 조회 → 전송 대기 → 발송 처리 흐름을 단계별로 표시합니다.
* **큐 사이즈**: 전송 유형(**legacy/RCS/카카오**)별 대기 건수를 표시합니다.
* **TPS**: 초당 처리 건수(Transactions Per Second)를 실시간으로 표시합니다.
* **CPU / 메모리 사용률**: 원형 게이지로 서버 리소스 사용 현황을 표시합니다.

<figure><img src="../../.gitbook/assets/10.png" alt="그림 10. 모니터링 화면 — 실시간 발송 현황 (파이프라인, 큐 사이즈, TPS, 리소스 게이지)"><figcaption><p>그림 10-1. 모니터링 화면 — 실시간 발송 현황 (파이프라인, 큐 사이즈, TPS, 리소스 게이지)</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/10_2.png" alt="그림 10-1. 모니터링 화면 — 스레드"><figcaption><p>그림 10-2. 모니터링 화면 — 스레드</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/10_3.png" alt="그림 10-3. 모니터링 화면 — DB 현황"><figcaption><p>그림 10-3. 모니터링 화면 — DB 현황</p></figcaption></figure>



### <mark style="color:blue;">발송 통계</mark>

일/주/월 단위로 집계된 발송 통계를 차트로 확인하고, 결과를 **CSV·Excel**로 내려받을 수 있습니다.

* **메시지 타입 별 통계**: **legacy / RCS / Kakao** 등 메시지 종류 별 발송 건수
* **시간대 별 발송 추이**: 00시 \~ 23시 시간대 별 발송 추이 차트 (일/주/월 단위 선택)
* **템플릿 별 발송 추이**: **RCS·카카오 알림톡 템플릿** 코드 별 발송 건수 (템플릿 코드 검색 지원)

<figure><img src="../../.gitbook/assets/11.png" alt="그림 11. 모니터링 화면 — 발송 통계 (메시지 타입 별 / 시간대 별 / 템플릿 별, CSV·Excel 내보내기)"><figcaption><p>그림 11. 모니터링 화면 — 발송 통계 (메시지 타입 별 / 시간대 별 / 전송 단계별, CSV 내보내기)</p></figcaption></figure>

{% hint style="info" %}
실시간 발송 현황은 WebSocket을 통해 실시간 갱신되며, 발송 통계는 약 14초 주기로 자동 갱신됩니다. 모니터링 화면 자체에서 설정을 변경하는 기능은 없습니다.
{% endhint %}
