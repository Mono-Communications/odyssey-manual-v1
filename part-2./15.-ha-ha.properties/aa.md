# 15-6. 로드밸런싱 (AA 모드 전용)

<mark style="color:red;">`LOAD_BALANCE_PERCENT`</mark>는 본 노드가 처리할 메시지 비율(%)이며, **양 노드의 합이 정확히 100**이 되어야 합니다. 합이 어긋나면 중복 발송 또는 누락이 발생할 수 있습니다.

<table><thead><tr><th width="285.79998779296875">노드 사양</th><th width="232.1998291015625">1번 노드</th><th>2번 노드</th></tr></thead><tbody><tr><td>동등 사양</td><td><mark style="color:red;"><code>50</code></mark></td><td><mark style="color:red;"><code>50</code></mark></td></tr><tr><td>1번이 더 좋음 (CPU/메모리/네트워크)</td><td><mark style="color:red;"><code>60 ~ 70</code></mark></td><td><mark style="color:red;"><code>40 ~ 30</code></mark></td></tr><tr><td>2번이 더 좋음</td><td><mark style="color:red;"><code>30 ~ 40</code></mark></td><td><mark style="color:red;"><code>70 ~ 60</code></mark></td></tr></tbody></table>

<mark style="color:red;">`ENFORCE_LOAD_BALANCE_RATIO=Y`</mark> (엄격) 설정 시 비율을 어기는 메시지 fetch를 차단합니다. `N`은 권고치로만 사용합니다.

