# 15. HA 이중화 설정 (ha.properties)

HA 프로파일에서 사용하는 이중화 노드 정보, 게이트웨이 감시, DB 기반 분산 락(Lease), 로드밸런싱 비율을 정의합니다. 파일 위치는 Odyssey 설치 폴더의 **`config/ha.properties`** 입니다.

## <mark style="color:blue;">설정 방법</mark> <a href="#ha-setup" id="ha-setup"></a>

이중화는 **Odyssey 2대(1번 노드, 2번 노드)가 같은 DB 를 바라보는 구성**입니다. 아래 순서로 설정합니다.

### 1. 준비

* 두 서버에 **같은 버전**의 Odyssey 를 설치합니다.
* 두 노드의 <mark style="color:red;">**`config/application.yml`**</mark> 은 **같은 DB**(`spring.datasource.hikari`)와 **같은 테이블명**(`common.tables.table-name`)을 사용해야 합니다.
* 두 서버가 서로의 HA 통신 포트(**`HA_PORT`**)로 접속할 수 있어야 합니다. 서버 사이에 방화벽이 있으면 양방향으로 허용합니다.
* 로그 이관은 켜 둡니다. (`common.execute.fetch: true`)

### 2. application.yml — 이중화 모드 지정 (두 노드 모두)

<mark style="color:red;">**`config/application.yml`**</mark> 의 **`ha-mode.mode`** 에 이중화 모드를 입력합니다. 기본값은 `STANDALONE`(이중화 미사용)입니다.

```yaml
ha-mode:
  mode: AA        # AA | AS | STANDALONE
```

{% hint style="warning" %}
**`ha-mode.mode`** 가 `AA` · `AS` 가 아니면 `STANDALONE` 으로 기동합니다. <mark style="color:red;">**`ha.properties`**</mark> 만 수정하고 이 값을 바꾸지 않으면 이중화가 동작하지 않습니다. <mark style="color:red;">**`ha.properties`**</mark> 의 **`HA_MODE`** 와 같은 값으로 맞추세요.
{% endhint %}

### 3. ha.properties — 노드별 값 입력

<mark style="color:red;">**`config/ha.properties`**</mark> 를 노드마다 작성합니다. **노드마다 달라야 하는 값**과 **두 노드가 같아야 하는 값**을 구분해서 입력합니다.

<table><thead><tr><th width="250">항목</th><th width="230">1번 노드</th><th>2번 노드</th></tr></thead><tbody><tr><td><strong><code>NODE_NUM</code></strong></td><td><code>1</code></td><td><code>2</code></td></tr><tr><td><strong><code>HA_MASTER_SLAVE</code></strong></td><td><code>MASTER</code></td><td><code>SLAVE</code></td></tr><tr><td><strong><code>HA_PORT</code></strong></td><td>1번 노드의 HA 포트 (예: <code>12001</code>)</td><td>2번 노드의 HA 포트 (예: <code>12001</code>)</td></tr><tr><td><strong><code>EXT_PEER_NODE_CHECK</code></strong></td><td><code>Y</code></td><td><code>Y</code></td></tr><tr><td><strong><code>EXT_PEER_NODE_IP</code></strong></td><td><strong>2번</strong> 노드의 IP</td><td><strong>1번</strong> 노드의 IP</td></tr><tr><td><strong><code>EXT_PEER_NODE_HA_PORT</code></strong></td><td><strong>2번</strong> 노드의 <code>HA_PORT</code></td><td><strong>1번</strong> 노드의 <code>HA_PORT</code></td></tr><tr><td><strong><code>PING_CMD</code></strong></td><td colspan="2">각 서버의 OS 에 맞는 명령 (<a href="ha.md">15-1. ha.properties 항목별 요약</a> 참고)</td></tr><tr><td><strong><code>LOAD_BALANCE_PERCENT</code></strong> (AA)</td><td>예: <code>50</code></td><td>예: <code>50</code> (두 노드의 합이 <code>100</code>)</td></tr></tbody></table>

<table><thead><tr><th width="250">두 노드가 같아야 하는 항목</th><th>입력</th></tr></thead><tbody><tr><td><strong><code>NODE_CNT</code></strong></td><td><code>2</code></td></tr><tr><td><strong><code>HA_MODE</code></strong></td><td><code>AA</code> 또는 <code>AS</code> (<strong><code>ha-mode.mode</code></strong> 와 같은 값)</td></tr><tr><td><strong><code>DB_LEASE_ENABLED</code></strong></td><td><code>Y</code></td></tr><tr><td><strong><code>DB_URL</code></strong> / <strong><code>DB_USER</code></strong> / <strong><code>DB_PASSWORD</code></strong></td><td><mark style="color:red;"><strong><code>application.yml</code></strong></mark> 과 같은 DB 의 접속 정보. <strong><code>DB_URL</code></strong> 형식은 <a href="../../part-1./3.-settings.md#id-3-1-db-springdatasourcehikari">3-1. DB 연결</a> 의 DBMS 별 <strong><code>jdbc-url</code></strong> 예시와 같습니다.</td></tr><tr><td><strong><code>DB_LEASE_NAME</code></strong></td><td><code>ha_lease_master</code> (두 노드가 같은 값)</td></tr><tr><td>타이밍 · 안정성 항목</td><td>기본값 유지</td></tr></tbody></table>

{% hint style="info" %}
**`ha_lease`** 테이블은 Odyssey 가 최초 기동 때 자동으로 만듭니다. DB 계정에 테이블 생성 권한이 없으면 <mark style="color:red;">**`config/mapper/{{DBMS}}/table.xml`**</mark> 의 `createHATable` 생성문으로 미리 만들어 두세요.
{% endhint %}

### 4. 기동과 확인

1. 1번 노드를 기동하고 <mark style="color:red;">**`logs/live/system.log`**</mark> 에서 아래 로그를 확인합니다.
2. 2번 노드를 기동하고 같은 로그를 확인합니다. **`nodeNum`** 이 노드마다 다르게 찍혀야 합니다.

```
[HaModule] HA module start - mode=AA, nodeNum=1, lb=50%
```

<table><thead><tr><th width="420">로그</th><th>의미</th></tr></thead><tbody><tr><td><code>[HaModule] HA module start - mode=..., nodeNum=..., lb=...%</code></td><td>이중화 모듈이 정상 기동했습니다.</td></tr><tr><td><code>[HA MODULE] - HA module start skip (STANDALONE)</code></td><td><strong><code>ha-mode.mode</code></strong> 가 <code>STANDALONE</code> 입니다. 이중화가 동작하지 않습니다.</td></tr><tr><td><code>[HA MODULE] - HA module start fail</code></td><td>이중화 모듈 기동에 실패했습니다. Odyssey 를 정지하고 <mark style="color:red;"><strong><code>ha.properties</code></strong></mark> 의 값(상대 노드 IP · 포트, DB 접속 정보)을 확인한 뒤 다시 기동하세요.</td></tr></tbody></table>

3. 테스트 메시지를 발송한 뒤 발송 테이블 · 로그 테이블의 **`LB_ID`** 컬럼에 메시지를 수집한 노드 번호가 기록되는지 확인합니다. ([6. 테스트 발송](../../part-1./6.-test-sms.md) 참고)

{% hint style="warning" %}
이중화 모드나 <mark style="color:red;">**`ha.properties`**</mark> 값을 바꿀 때는 **두 노드를 모두 정지한 뒤** 수정하고 다시 기동하세요.
{% endhint %}

## <mark style="color:blue;">ha.properties 예시</mark>

```properties
NODE_CNT=2
NODE_NUM=1
HA_MODE=AA                     # AA | AS | STANDALONE
HA_MASTER_SLAVE=MASTER         # MASTER | SLAVE
HA_AUTO_SWITCH=N               # Y | N (AS mode only)

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

## 장애 전환 시 동작 <a href="#failover" id="failover"></a>

* 메시지를 수집한 노드의 번호가 발송 테이블의 **`LB_ID`** 컬럼에 기록됩니다.
* 상대 노드가 내려가면 남은 노드가 상대 노드가 수집한 메시지의 **발송 결과 조회, 로그 테이블 이관, 만료 처리**를 이어받습니다.
* 대기 중인 노드(담당 구간이 없는 노드)는 수집 · 발송 결과 조회 · 이관 · 만료 처리를 하지 않습니다.
* 정상 정지한 노드의 큐에 남아 있던 미발송 메시지는 수집 전 상태로 되돌려져 남은 노드가 다시 수집해 발송합니다. 강제 종료나 서버 장애 때는 되돌리지 못합니다. ([4. 실행 / 정지](../../part-1./4.-start-stop.md#stop-behavior) 참고)

{% hint style="info" %}
이중화 동작을 확인한 DBMS : MySQL 8.0, PostgreSQL, Oracle 11.2, SQL Server 2022
{% endhint %}
