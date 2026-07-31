# 15-5. DB Lease (DB 기반 분산 락)

Odyssey HA는 두 노드의 활성/정지를 DB 테이블(<mark style="color:red;">**`ha_lease`**</mark>)에 기록되는 임차권(Lease) 기반으로 관리합니다. <mark style="color:red;">**`ha_lease`**</mark> 테이블은 최초 기동 시 자동 생성됩니다.

* **`DB_LEASE_NAME`**: 동일 클러스터의 두 노드는 **같은 값**을 사용해야 같은 Lease를 두고 경쟁합니다.
* **`DB_LEASE_TTL_MS`** / **`RENEW_INTERVAL_MS`**: 갱신 주기는 TTL의 1/3 \~ 1/5 사이를 권장합니다 (기본 <mark style="color:red;">`5000`</mark> / <mark style="color:red;">`1000`</mark>).
* **`DB_LEASE_FAIL_CLOSED=Y`** (권장): DB 연결이 끊기면 본 노드가 즉시 정지해 split-brain 위험을 차단합니다.

