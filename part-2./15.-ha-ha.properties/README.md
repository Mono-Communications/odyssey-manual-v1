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

<table><thead><tr><th width="106.99993896484375">그룹</th><th width="221.39996337890625">옵션</th><th width="223.4000244140625">설명</th><th>권장값</th></tr></thead><tbody><tr><td>노드 정보</td><td><strong><code>NODE_CNT</code></strong></td><td>이중화 참여 노드 수</td><td><mark style="color:red;"><code>2</code></mark></td></tr><tr><td>노드 정보</td><td><strong><code>NODE_NUM</code></strong></td><td>본 노드 번호</td><td><mark style="color:red;"><code>1</code></mark> 또는 <mark style="color:red;"><code>2</code></mark> (양 노드 다른 값)</td></tr><tr><td>노드 정보</td><td><strong><code>HA_MODE</code></strong></td><td>이중화 모드</td><td><mark style="color:red;"><code>AA</code></mark> (권장) / <mark style="color:red;"><code>AS</code></mark> / <mark style="color:red;"><code>STANDALONE</code></mark></td></tr><tr><td>노드 정보</td><td><strong><code>HA_MASTER_SLAVE</code></strong></td><td>본 노드 역할</td><td><mark style="color:red;"><code>MASTER</code></mark> 또는 <mark style="color:red;"><code>SLAVE</code></mark></td></tr><tr><td>노드 정보</td><td><strong><code>HA_AUTO_SWITCH</code></strong></td><td>AS 모드 자동 역할 전환</td><td><mark style="color:red;"><code>N</code></mark> (수동, 권장)</td></tr><tr><td>네트워크</td><td><strong><code>HA_PORT</code></strong></td><td>본 노드 HA 통신 포트</td><td><mark style="color:red;"><code>12001</code></mark></td></tr><tr><td>네트워크</td><td><strong><code>INT_PEER_NODE_CHECK / _IP / _HA_PORT</code></strong></td><td>내부 네트워크 Peer 감시</td><td>보통 <mark style="color:red;"><code>N</code></mark></td></tr><tr><td>네트워크</td><td><strong><code>EXT_PEER_NODE_CHECK / _IP / _HA_PORT</code></strong></td><td>외부 네트워크 Peer 감시</td><td><mark style="color:red;"><code>Y</code></mark> + 상대 노드 IP/포트</td></tr><tr><td>PING</td><td><strong><code>PING_CMD</code></strong></td><td>게이트웨이 생존 확인 명령</td><td>OS에 맞게 (한 번만 수정)</td></tr><tr><td>PING</td><td><strong><code>PING_SUCCESS_KEY</code></strong></td><td>PING 성공 인식 문자열</td><td><mark style="color:red;"><code>TTL=</code></mark></td></tr><tr><td>PING</td><td><strong><code>PING_INTERVAL / PING_TIMEOUT</code></strong></td><td>PING 주기 / 응답 대기 (ms)</td><td><mark style="color:red;"><code>1000</code></mark> / <mark style="color:red;"><code>5000</code></mark></td></tr><tr><td>타이밍</td><td><strong><code>NODE_CHECK_INTERVAL / _TIMEOUT</code></strong></td><td>Peer 상태 체크 주기 / 응답 대기 (ms)</td><td><mark style="color:red;"><code>1000</code></mark> / <mark style="color:red;"><code>3000</code></mark></td></tr><tr><td>타이밍</td><td><strong><code>NODE_ACTIVATING_INTERVAL</code></strong></td><td>Activating → Active 대기 (ms)</td><td><mark style="color:red;"><code>3000</code></mark></td></tr><tr><td>안정성</td><td><strong><code>FAILBACK_STABILIZATION_MS</code></strong></td><td>Failback 안정 대기 (ms)</td><td><mark style="color:red;"><code>30000</code></mark></td></tr><tr><td>안정성</td><td><strong><code>SPLIT_BRAIN_PROTECTION</code></strong></td><td>Split-Brain 보호 모드</td><td><mark style="color:red;"><code>N</code></mark> (필요 시 <mark style="color:red;"><code>Y</code></mark>)</td></tr><tr><td>안정성</td><td><strong><code>PEER_FRESHNESS_MS</code></strong></td><td>Peer 상태 유효 기간 (ms)</td><td><mark style="color:red;"><code>3000</code></mark></td></tr><tr><td>DB Lease</td><td><strong><code>DB_LEASE_ENABLED</code></strong></td><td>DB Lease 사용</td><td>HA 운영 시 <mark style="color:red;"><code>Y</code></mark></td></tr><tr><td>DB Lease</td><td><strong><code>DB_LEASE_FAIL_CLOSED</code></strong></td><td>DB 실패 시 본 노드 정지 여부</td><td><mark style="color:red;"><code>Y</code></mark> (권장)</td></tr><tr><td>DB Lease</td><td><strong><code>DB_URL / DB_USER / DB_PASSWORD</code></strong></td><td>Lease DB 접속 정보</td><td>메인 DB와 동일</td></tr><tr><td>DB Lease</td><td><strong><code>DB_LEASE_NAME</code></strong></td><td>Lease 식별자</td><td><mark style="color:red;"><code>ha_lease_master</code></mark> (양 노드 동일)</td></tr><tr><td>DB Lease</td><td><strong><code>DB_LEASE_TTL_MS / _RENEW_INTERVAL_MS</code></strong></td><td>Lease 만료 / 갱신 주기 (ms)</td><td><mark style="color:red;"><code>5000</code></mark> / <mark style="color:red;"><code>1000</code></mark></td></tr><tr><td>로드밸런싱</td><td><strong><code>LOAD_BALANCE_PERCENT</code></strong></td><td>본 노드 처리 비율 (%)</td><td>양 노드 합이 정확히 <mark style="color:red;"><code>100</code></mark></td></tr><tr><td>로드밸런싱</td><td><strong><code>ENFORCE_LOAD_BALANCE_RATIO</code></strong></td><td>로드밸런싱 비율 강제 여부</td><td><mark style="color:red;"><code>Y</code></mark> (엄격)</td></tr></tbody></table>
