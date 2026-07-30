# 15-7. 권장 설정 (HA 모드별)

<table><thead><tr><th width="179.39996337890625">HA 모드</th><th width="183.800048828125">HA_AUTO_SWITCH</th><th width="249.7999267578125">LOAD_BALANCE_PERCENT</th><th>DB_LEASE_FAIL_CLOSED</th></tr></thead><tbody><tr><td>AA (일반 운영)</td><td>—</td><td>양 노드 합 100 (기본 50:50)</td><td>Y</td></tr><tr><td>AS (단순 운영)</td><td>N (수동)</td><td>— (사용 안함)</td><td>Y</td></tr><tr><td>STANDALONE (개발/테스트)</td><td>—</td><td>—</td><td>N (선택)</td></tr></tbody></table>

{% hint style="warning" %}
<mark style="color:$warning;">**자주 하는 실수**</mark>

1. **양 노드에 같은 `NODE_NUM` 입력** — 1번 노드는 `NODE_NUM=1`, 2번 노드는 `NODE_NUM=2`로 정확히 다르게 설정하세요.
2. **`LOAD_BALANCE_PERCENT` 합이 100이 아님** — 합이 100을 초과하면 중복 발송, 미만이면 일부 메시지가 영원히 처리되지 않습니다.
3. **`DB_LEASE_NAME`을 노드별로 다르게 설정** — 동일 클러스터는 같은 `DB_LEASE_NAME`을 사용하세요.
4. **`DB_LEASE_TTL_MS` / `_RENEW_INTERVAL_MS` 임의 조정** — 기본값을 유지하기를 권장합니다.
5. **운영 중 `HA_MODE` 변경** — HA 모드 변경 시 양 노드를 정지 후 동시 재기동하세요.
{% endhint %}
