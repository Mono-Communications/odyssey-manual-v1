# 14. 계정 설정 (sessions)

각 게이트웨이 별 세션 정보는 <mark style="color:red;">`kt`</mark> / <mark style="color:red;">`rcs`</mark> / <mark style="color:red;">`cpaas`</mark>/ <mark style="color:red;">`kakao`</mark> 영역의 <mark style="color:green;">`sessions`</mark> 리스트에 입력합니다. 실제 사용하는 세션만 등록하고, 사용하지 않는 영역은 주석 처리하거나 통째로 삭제합니다.

### 세션 매핑

<mark style="color:green;">`common.transmission`</mark> 설정에 따라 사용하는 세션 영역이 결정됩니다.

<table><thead><tr><th width="223.39996337890625">common.transmission 값</th><th width="194.7999267578125">사용 세션 영역</th><th>게이트웨이</th></tr></thead><tbody><tr><td><strong><code>msg: KT</code></strong></td><td><mark style="color:red;"><code>kt.sessions</code></mark></td><td>KT Xroshot (문자 직접 연동)</td></tr><tr><td><strong><code>msg: CPAAS</code></strong></td><td><mark style="color:red;"><code>cpaas.sessions</code></mark></td><td>KT CPaaS (문자 API)</td></tr><tr><td><strong><code>rcs: KT</code></strong></td><td><mark style="color:red;"><code>rcs.sessions</code></mark></td><td>KT RCS Hermes API</td></tr><tr><td><strong><code>rcs: CPAAS</code></strong></td><td><mark style="color:red;"><code>cpaas.sessions</code></mark></td><td>KT CPaaS (RCS API)</td></tr><tr><td><strong><code>kakao: MN</code></strong></td><td><mark style="color:red;"><code>kakao.sessions</code></mark></td><td>엠앤와이즈 직접 연동</td></tr><tr><td><strong><code>kakao: CPAAS</code></strong></td><td><mark style="color:red;"><code>cpaas.sessions</code></mark></td><td>KT CPaaS (카카오 API)</td></tr></tbody></table>
