# 로그 관리

Odyssey 로그 파일을 브라우저에서 조회하고 다운로드할 수 있습니다.

* **날짜 필터**: 시작일\~종료일 범위로 로그 파일을 필터링합니다.
* **파일 브라우저**: `log/` 폴더와 `log_backup/` 폴더를 아코디언 형태로 탐색합니다.
* **다운로드**: 개별 파일 다운로드, 전체 ZIP 다운로드, 선택 파일 ZIP 다운로드를 지원합니다.

!\[로그 관리]\(./images/06. 로그 저장.png)

그림 20. 로그 관리 — 날짜 필터, log/log\_backup 디렉토리 탐색, 파일 선택 다운로드

### 이중화 설정

HA 운영 모드 선택, 부하 분산, `ha.properties` 직접 편집을 한 화면에서 처리합니다.

| 운영 모드              | 설명                                        | 부하 분산 / HA.PROPERTIES              |
| ------------------ | ----------------------------------------- | ---------------------------------- |
| **Standalone**     | 단일 노드 운영. 이중화 미사용.                        | 부하 분산 비활성, HA.PROPERTIES 비활성       |
| **Active/Active**  | 두 노드가 동시에 메시지를 나눠 발송. 처리량 ↑, 부하 분산.       | 부하 분산 활성, Load Balance Ratio 조정 가능 |
| **Active/Standby** | Master 한 대만 발송, Slave는 대기. 장애 시 자동/수동 전환. | HA\_AUTO\_SWITCH 활성, 부하 분산 비활성     |

!\[이중화 설정 - Standalone 모드]\(./images/07. 이중화설정 - SA.png)

그림 21. 이중화 설정 — Standalone 모드 (부하 분산 · HA.PROPERTIES 비활성)

!\[이중화 설정 - Active/Active 모드]\(./images/07-1. 이중화설정 - AA.png)

그림 22. 이중화 설정 — Active/Active 모드 (부하 분산 활성, Load Balance Ratio 조절 가능)

!\[이중화 설정 - Active/Standby 모드]\(./images/07-2. 이중화설정 - AS.png)

그림 23. 이중화 설정 — Active/Standby 모드 (HA\_AUTO\_SWITCH 활성)

{% hint style="info" %}
HA 프로파일로 기동한 경우에만 본 메뉴가 활성화됩니다. AS/SA 프로파일에서는 메뉴가 표시되지 않거나 일부 옵션이 비활성화될 수 있습니다.
{% endhint %}
