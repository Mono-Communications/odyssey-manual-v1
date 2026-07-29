# 권장 설정 (HA 모드별)

| HA 모드               | HA\_AUTO\_SWITCH | LOAD\_BALANCE\_PERCENT | DB\_LEASE\_FAIL\_CLOSED |
| ------------------- | ---------------- | ---------------------- | ----------------------- |
| AA (일반 운영)          | —                | 양 노드 합 100 (기본 50:50)  | Y                       |
| AS (단순 운영)          | N (수동)           | — (사용 안함)              | Y                       |
| STANDALONE (개발/테스트) | —                | —                      | N (선택)                  |

{% hint style="warning" %}
**자주 하는 실수**

1. **양 노드에 같은 `NODE_NUM` 입력** — 1번 노드는 `NODE_NUM=1`, 2번 노드는 `NODE_NUM=2`로 정확히 다르게 설정하세요.
2. **`LOAD_BALANCE_PERCENT` 합이 100이 아님** — 합이 100을 초과하면 중복 발송, 미만이면 일부 메시지가 영원히 처리되지 않습니다.
3. **`DB_LEASE_NAME`을 노드별로 다르게 설정** — 동일 클러스터는 같은 `DB_LEASE_NAME`을 사용하세요.
4. **`DB_LEASE_TTL_MS` / `_RENEW_INTERVAL_MS` 임의 조정** — 기본값 유지 권장.
5. **운영 중 `HA_MODE` 변경** — HA 모드 변경 시 양 노드를 정지 후 동시 재기동하세요.
{% endhint %}
