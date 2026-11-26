# 15-1. ha.properties 항목별 요약

<mark style="color:red;">**`config/ha.properties`**</mark> 의 항목을 그룹별로 설명합니다. 전체 항목과 권장값은 [15. HA 이중화 설정 (ha.properties)](README.md) 의 표를 참고하세요.

## <mark style="color:blue;">노드 정보 / HA 모드</mark>

<mark style="color:red;">`HA_MODE`</mark>는 이중화 운영 방식을 결정합니다.

<table><thead><tr><th width="179.39996337890625">모드</th><th width="266.1998291015625">동작</th><th width="104">처리량</th><th>권장 사용처</th></tr></thead><tbody><tr><td><strong><code>AA</code></strong> (Active-Active)</td><td>두 노드가 동시에 발송 (로드밸런싱)</td><td>2배</td><td>일반 운영 환경 (권장)</td></tr><tr><td><strong><code>AS</code></strong> (Active-Standby)</td><td>Master만 발송, Slave는 대기</td><td>1배</td><td>단순 동작이 필요한 환경</td></tr><tr><td><strong><code>STANDALONE</code></strong></td><td>단일 노드, 이중화 미사용</td><td>1배</td><td>개발 / 테스트</td></tr></tbody></table>

<mark style="color:red;">`HA_AUTO_SWITCH`</mark>는 AS 모드에서 SLAVE가 활성화 된 동안 MASTER가 복구되면 자동으로 역할을 되돌릴지 여부입니다.

<mark style="color:red;">**`N`**</mark>**&#x20;(수동 전환) 유지를 권장**합니다. 자동 전환 시 역할이 왔다갔다하는 플리커링(Flickering)이 발생할 수 있습니다.

## <mark style="color:blue;">네트워크 / Peer 감시</mark>

양 노드의 IP와 HA 포트를 교차 등록합니다. 동일 호스트에서 다중 인스턴스 테스트가 필요할 때만 <mark style="color:red;">`INT_PEER_NODE_CHECK=Y`</mark>를 사용합니다.

## <mark style="color:blue;">Gateway PING 체크</mark>

게이트웨이 생존을 주기적으로 확인하여 네트워크 단절 시 자동으로 Failover를 트리거합니다.

<table><thead><tr><th width="298.00006103515625">OS</th><th>PING_CMD</th></tr></thead><tbody><tr><td><strong><code>Linux</code></strong></td><td><mark style="color:red;"><code>ping -c 1 -W 1 [target]</code></mark></td></tr><tr><td><strong><code>Windows</code></strong></td><td><mark style="color:red;"><code>ping [target] -n 1</code></mark></td></tr></tbody></table>

{% hint style="info" %}
`[target]`은 게이트웨이 IP 또는 기본 게이트웨이(라우터) IP를 입력합니다. 설치 시 OS 유형에 맞춰 **한 번만** 수정하면 운영 중 바꿀 일이 없습니다.
{% endhint %}

## <mark style="color:blue;">HA 타이밍 / 안정성 / Split-Brain 방지</mark>

Peer 노드 감시 주기, Failback 안정화 대기, Split-Brain 보호 동작 등을 제어합니다. **기본값 유지를 강력히 권장**합니다. — 임의 변경 시 장애 감지 속도와 스플릿-브레인 방지 안정성 사이의 균형이 깨집니다.

## <mark style="color:blue;">DB Lease (DB 기반 분산 락)</mark>

Odyssey HA는 두 노드의 활성/정지를 DB 테이블(<mark style="color:red;">**`ha_lease`**</mark>)에 기록되는 임차권(Lease) 기반으로 관리합니다. <mark style="color:red;">**`ha_lease`**</mark> 테이블은 최초 기동 시 자동 생성됩니다.

* **`DB_LEASE_NAME`**: 동일 클러스터의 두 노드는 **같은 값**을 사용해야 같은 Lease를 두고 경쟁합니다.
* **`DB_LEASE_TTL_MS`** / **`RENEW_INTERVAL_MS`**: 갱신 주기는 TTL의 1/3 \~ 1/5 사이를 권장합니다 (기본 <mark style="color:red;">`5000`</mark> / <mark style="color:red;">`1000`</mark>).
* **`DB_LEASE_FAIL_CLOSED=Y`** (권장): DB 연결이 끊기면 본 노드가 즉시 정지해 split-brain 위험을 차단합니다.

## <mark style="color:blue;">로드밸런싱 (AA 모드 전용)</mark>

<mark style="color:red;">**`LOAD_BALANCE_PERCENT`**</mark>는 본 노드가 처리할 메시지 비율(%)이며, **양 노드의 합이 정확히 100**이 되어야 합니다. 합이 어긋나면 중복 발송 또는 누락이 발생할 수 있습니다.

<table><thead><tr><th width="285.79998779296875">노드 사양</th><th width="232.1998291015625">1번 노드</th><th>2번 노드</th></tr></thead><tbody><tr><td>동등 사양</td><td><mark style="color:red;"><code>50</code></mark></td><td><mark style="color:red;"><code>50</code></mark></td></tr><tr><td>1번이 더 좋음 (CPU/메모리/네트워크)</td><td><mark style="color:red;"><code>60 ~ 70</code></mark></td><td><mark style="color:red;"><code>40 ~ 30</code></mark></td></tr><tr><td>2번이 더 좋음</td><td><mark style="color:red;"><code>30 ~ 40</code></mark></td><td><mark style="color:red;"><code>70 ~ 60</code></mark></td></tr></tbody></table>

<mark style="color:red;">**`ENFORCE_LOAD_BALANCE_RATIO=Y`**</mark> (엄격) 설정 시 비율을 어기는 메시지 fetch를 차단합니다. `N`은 권고치로만 사용합니다.
