# 15. HA 이중화 설정 (ha.properties)

HA 프로파일에서 사용하는 이중화 노드 정보, 게이트웨이 감시, DB 기반 분산 락(Lease), 로드밸런싱 비율을 정의합니다. 파일 위치는 Odyssey 설치 폴더의 `config/ha.properties` 입니다.

```properties
NODE_CNT=2
NODE_NUM=1
HA_MODE=AA # AA | AS | STANDALONE
HA_MASTER_SLAVE=MASTER # MASTER | SLAVE
HA_AUTO_SWITCH=N # Y | N (AS mode only)

# NETWORK
HA_PORT=12001
INT_PEER_NODE_CHECK=N
INT_PEER_NODE_IP=127.0.0.1
INT_PEER_NODE_HA_PORT=9999
EXT_PEER_NODE_CHECK=Y
EXT_PEER_NODE_IP={{ip}}
EXT_PEER_NODE_HA_PORT=12000

# GATEWAY CHECK
PING_CMD=ping 127.0.0.1 -n 1
PING_SUCCESS_KEY=TTL=
PING_INTERVAL=1000
PING_TIMEOUT=5000

# HA TIMING (ms)
NODE_CHECK_INTERVAL=1000
NODE_CHECK_TIMEOUT=3000
NODE_ACTIVATING_INTERVAL=3000

# SAFETY / STABILITY
FAILBACK_STABILIZATION_MS=30000
SPLIT_BRAIN_PROTECTION=N
PEER_FRESHNESS_MS=3000

# DB LEASE
DB_LEASE_ENABLED=Y
DB_LEASE_FAIL_CLOSED=Y
DB_URL=jdbc:mysql://{{ip}}:{{port}}/{{database}}?useUnicode=true&characterEncoding=UTF-8&useSSL=false&allowPublicKeyRetrieval=true
DB_USER={{id}}
DB_PASSWORD={{pw}}
DB_LEASE_NAME=ha_lease_master
DB_LEASE_TTL_MS=5000
DB_LEASE_RENEW_INTERVAL_MS=1000

# LOAD BALANCE RATIO
LOAD_BALANCE_PERCENT=60
ENFORCE_LOAD_BALANCE_RATIO=Y
```



## 항목 별 설명

<table><thead><tr><th width="106.99993896484375">그룹</th><th width="221.39996337890625">옵션</th><th width="223.4000244140625">설명</th><th>권장값</th></tr></thead><tbody><tr><td>노드 정보</td><td>NODE_CNT</td><td>이중화 참여 노드 수</td><td>2</td></tr><tr><td>노드 정보</td><td>NODE_NUM</td><td>본 노드 번호</td><td>1 또는 2 (양 노드 다른 값)</td></tr><tr><td>노드 정보</td><td>HA_MODE</td><td>이중화 모드</td><td>AA (권장) / AS / STANDALONE</td></tr><tr><td>노드 정보</td><td>HA_MASTER_SLAVE</td><td>본 노드 역할</td><td>MASTER 또는 SLAVE</td></tr><tr><td>노드 정보</td><td>HA_AUTO_SWITCH</td><td>AS 모드 자동 역할 전환</td><td>N (수동, 권장)</td></tr><tr><td>네트워크</td><td>HA_PORT</td><td>본 노드 HA 통신 포트</td><td>12001</td></tr><tr><td>네트워크</td><td>INT_PEER_NODE_CHECK / _IP / _HA_PORT</td><td>내부 네트워크 Peer 감시</td><td>보통 N</td></tr><tr><td>네트워크</td><td>EXT_PEER_NODE_CHECK / _IP / _HA_PORT</td><td>외부 네트워크 Peer 감시</td><td>Y + 상대 노드 IP/포트</td></tr><tr><td>PING</td><td>PING_CMD</td><td>게이트웨이 생존 확인 명령</td><td>OS에 맞게 (한 번만 수정)</td></tr><tr><td>PING</td><td>PING_SUCCESS_KEY</td><td>PING 성공 인식 문자열</td><td>TTL=</td></tr><tr><td>PING</td><td>PING_INTERVAL / PING_TIMEOUT</td><td>PING 주기 / 응답 대기 (ms)</td><td>1000 / 5000</td></tr><tr><td>타이밍</td><td>NODE_CHECK_INTERVAL / _TIMEOUT</td><td>Peer 상태 체크 주기 / 응답 대기 (ms)</td><td>1000 / 3000</td></tr><tr><td>타이밍</td><td>NODE_ACTIVATING_INTERVAL</td><td>Activating → Active 대기 (ms)</td><td>3000</td></tr><tr><td>안정성</td><td>FAILBACK_STABILIZATION_MS</td><td>Failback 안정 대기 (ms)</td><td>30000</td></tr><tr><td>안정성</td><td>SPLIT_BRAIN_PROTECTION</td><td>Split-Brain 보호 모드</td><td>N (필요 시 Y)</td></tr><tr><td>안정성</td><td>PEER_FRESHNESS_MS</td><td>Peer 상태 유효 기간 (ms)</td><td>3000</td></tr><tr><td>DB Lease</td><td>DB_LEASE_ENABLED</td><td>DB Lease 사용</td><td>HA 운영 시 Y</td></tr><tr><td>DB Lease</td><td>DB_LEASE_FAIL_CLOSED</td><td>DB 실패 시 본 노드 정지 여부</td><td>Y (권장)</td></tr><tr><td>DB Lease</td><td>DB_URL / DB_USER / DB_PASSWORD</td><td>Lease DB 접속 정보</td><td>메인 DB와 동일</td></tr><tr><td>DB Lease</td><td>DB_LEASE_NAME</td><td>Lease 식별자</td><td>ha_lease_master (양 노드 동일)</td></tr><tr><td>DB Lease</td><td>DB_LEASE_TTL_MS / _RENEW_INTERVAL_MS</td><td>Lease 만료 / 갱신 주기 (ms)</td><td>5000 / 1000</td></tr><tr><td>로드밸런싱</td><td>LOAD_BALANCE_PERCENT</td><td>본 노드 처리 비율 (%)</td><td>양 노드 합이 정확히 100</td></tr><tr><td>로드밸런싱</td><td>ENFORCE_LOAD_BALANCE_RATIO</td><td>로드밸런싱 비율 강제 여부</td><td>Y (엄격)</td></tr></tbody></table>
