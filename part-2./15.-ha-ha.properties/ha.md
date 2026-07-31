# 15-1. 노드 정보 / HA 모드

<mark style="color:red;">`HA_MODE`</mark>는 이중화 운영 방식을 결정합니다.

<table><thead><tr><th width="179.39996337890625">모드</th><th width="266.1998291015625">동작</th><th width="104">처리량</th><th>권장 사용처</th></tr></thead><tbody><tr><td><strong><code>AA</code></strong> (Active-Active)</td><td>두 노드가 동시에 발송 (로드밸런싱)</td><td>2배</td><td>일반 운영 환경 (권장)</td></tr><tr><td><strong><code>AS</code></strong> (Active-Standby)</td><td>Master만 발송, Slave는 대기</td><td>1배</td><td>단순 동작이 필요한 환경</td></tr><tr><td><strong><code>STANDALONE</code></strong></td><td>단일 노드, 이중화 미사용</td><td>1배</td><td>개발 / 테스트</td></tr></tbody></table>

<mark style="color:red;">`HA_AUTO_SWITCH`</mark>는 AS 모드에서 SLAVE가 활성화 된 동안 MASTER가 복구되면 자동으로 역할을 되돌릴지 여부입니다.

<mark style="color:red;">**`N`**</mark>**&#x20;(수동 전환) 유지를 권장**합니다. 자동 전환 시 역할이 왔다갔다하는 플리커링(Flickering)이 발생할 수 있습니다.

