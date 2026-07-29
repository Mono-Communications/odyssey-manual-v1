---
layout:
  width: default
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# 항목별 설명

| 그룹       | 옵션                                         | 설명                          | 권장값                         |
| -------- | ------------------------------------------ | --------------------------- | --------------------------- |
| 노드 정보    | NODE\_CNT                                  | 이중화 참여 노드 수                 | 2                           |
| 노드 정보    | NODE\_NUM                                  | 본 노드 번호                     | 1 또는 2 (양 노드 다른 값)          |
| 노드 정보    | HA\_MODE                                   | 이중화 모드                      | AA (권장) / AS / STANDALONE   |
| 노드 정보    | HA\_MASTER\_SLAVE                          | 본 노드 역할                     | MASTER 또는 SLAVE             |
| 노드 정보    | HA\_AUTO\_SWITCH                           | AS 모드 자동 역할 전환              | N (수동, 권장)                  |
| 네트워크     | HA\_PORT                                   | 본 노드 HA 통신 포트               | 12001                       |
| 네트워크     | INT\_PEER\_NODE\_CHECK / \_IP / \_HA\_PORT | 내부 네트워크 Peer 감시             | 보통 N                        |
| 네트워크     | EXT\_PEER\_NODE\_CHECK / \_IP / \_HA\_PORT | 외부 네트워크 Peer 감시             | Y + 상대 노드 IP/포트             |
| PING     | PING\_CMD                                  | 게이트웨이 생존 확인 명령              | OS에 맞게 (한 번만 수정)            |
| PING     | PING\_SUCCESS\_KEY                         | PING 성공 인식 문자열              | TTL=                        |
| PING     | PING\_INTERVAL / PING\_TIMEOUT             | PING 주기 / 응답 대기 (ms)        | 1000 / 5000                 |
| 타이밍      | NODE\_CHECK\_INTERVAL / \_TIMEOUT          | Peer 상태 체크 주기 / 응답 대기 (ms)  | 1000 / 3000                 |
| 타이밍      | NODE\_ACTIVATING\_INTERVAL                 | Activating → Active 대기 (ms) | 3000                        |
| 안정성      | FAILBACK\_STABILIZATION\_MS                | Failback 안정 대기 (ms)         | 30000                       |
| 안정성      | SPLIT\_BRAIN\_PROTECTION                   | Split-Brain 보호 모드           | N (필요 시 Y)                  |
| 안정성      | PEER\_FRESHNESS\_MS                        | Peer 상태 유효 기간 (ms)          | 3000                        |
| DB Lease | DB\_LEASE\_ENABLED                         | DB Lease 사용                 | HA 운영 시 Y                   |
| DB Lease | DB\_LEASE\_FAIL\_CLOSED                    | DB 실패 시 본 노드 정지 여부          | Y (권장)                      |
| DB Lease | DB\_URL / DB\_USER / DB\_PASSWORD          | Lease DB 접속 정보              | 메인 DB와 동일                   |
| DB Lease | DB\_LEASE\_NAME                            | Lease 식별자                   | ha\_lease\_master (양 노드 동일) |
| DB Lease | DB\_LEASE\_TTL\_MS / \_RENEW\_INTERVAL\_MS | Lease 만료 / 갱신 주기 (ms)       | 5000 / 1000                 |
| 로드밸런싱    | LOAD\_BALANCE\_PERCENT                     | 본 노드 처리 비율 (%)              | 양 노드 합이 정확히 100             |
| 로드밸런싱    | ENFORCE\_LOAD\_BALANCE\_RATIO              | 로드밸런싱 비율 강제 여부              | Y (엄격)                      |
