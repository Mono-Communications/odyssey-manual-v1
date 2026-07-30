# 15-1. 노드 정보 / HA 모드

`HA_MODE`는 이중화 운영 방식을 결정합니다.

<table><thead><tr><th width="179.39996337890625">모드</th><th width="266.1998291015625">동작</th><th width="104">처리량</th><th>권장 사용처</th></tr></thead><tbody><tr><td>AA (Active-Active)</td><td>두 노드가 동시에 발송 (로드밸런싱)</td><td>2배</td><td>일반 운영 환경 (권장)</td></tr><tr><td>AS (Active-Standby)</td><td>Master만 발송, Slave는 대기</td><td>1배</td><td>단순 동작이 필요한 환경</td></tr><tr><td>STANDALONE</td><td>단일 노드, 이중화 미사용</td><td>1배</td><td>개발 / 테스트</td></tr></tbody></table>

`HA_AUTO_SWITCH`는 AS 모드에서 SLAVE가 활성된 동안 MASTER가 복구되면 자동으로 역할을 되돌릴지 여부입니다.

— **`N` (수동 전환) 유지를 권장**합니다. 자동 전환 시 역할이 왔다갔다하는 플리커링(Flickering)이 발생할 수 있습니다.
