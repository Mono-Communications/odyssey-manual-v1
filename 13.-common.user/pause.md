# 발송 금지 시간 (pause)

발송 금지 시간은 `application-HA.yaml`에 직접 설정하지 않습니다. Web UI의 "발송 금지 시간" 화면에서만 편집 가능하며, 설정값은 `PAUSE_INFO` 테이블에 저장됩니다.

{% hint style="warning" %}
**반드시 설정하세요.** 광고성 메시지는 **정보통신망법에 따라 야간(21:00 \~ 익일 08:00) 발송이 금지**되어 있습니다. 해당 시간대를 차단하지 않으면 과태료 대상이 될 수 있으므로, 광고성 메시지를 발송하는 환경이라면 반드시 야간 차단을 설정해야 합니다.
{% endhint %}

### 기타 옵션

| 옵션             | 설명                                   |
| -------------- | ------------------------------------ |
| kisa-orig-code | KISA 코드. 재판매 사업자만 발급받은 코드를 설정합니다.    |
| agencykey      | agencyId(대행사 ID)에 매핑되는 대행사 KEY 값.    |
| brandid        | chatbotId(챗봇 ID) 소유 brandId(브랜드 ID). |
| brandkey       | brandId에 매핑되는 브랜드 KEY 값.             |
| rcs-stat-info  | RCS 고객반응 통계 기능 사용 여부. (true/false)   |
