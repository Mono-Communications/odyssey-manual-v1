# 14. 계정 설정 (sessions)

각 게이트웨이별 세션 정보는 `kt` / `rcs` / `cpaas` / `kakao` 영역의 `sessions` 리스트에 입력합니다. 실제 사용하는 세션만 등록하고, 사용하지 않는 영역은 주석 처리하거나 통째로 삭제합니다.

### 세션 매핑

`common.transmission` 설정에 따라 사용하는 세션 영역이 결정됩니다.

<table><thead><tr><th width="223.39996337890625">common.transmission 값</th><th width="194.7999267578125">사용 세션 영역</th><th>게이트웨이</th></tr></thead><tbody><tr><td>msg: KT</td><td>kt.sessions</td><td>KT Xroshot (문자 직접 연동)</td></tr><tr><td>msg: CPAAS</td><td>cpaas.sessions</td><td>KT CPaaS (문자 API)</td></tr><tr><td>rcs: KT</td><td>rcs.sessions</td><td>KT RCS Hermes API</td></tr><tr><td>rcs: CPAAS</td><td>cpaas.sessions</td><td>KT CPaaS (RCS API)</td></tr><tr><td>kakao: MN</td><td>kakao.sessions</td><td>엠앤와이즈 직접 연동</td></tr><tr><td>kakao: CPAAS</td><td>cpaas.sessions</td><td>KT CPaaS (카카오 API)</td></tr></tbody></table>
