# 20. Web UI 상세

Odyssey는 브라우저 기반의 웹 설정 UI를 제공합니다. YAML 파일을 직접 편집하지 않고도 주요 설정을 변경하고, 실시간 모니터링 및 로그 관리를 수행할 수 있습니다.



### 접속 방법 <a href="#undefined" id="undefined"></a>

Odyssey가 구동된 상태에서 브라우저로 다음 주소에 접속합니다.

```
http://[서버IP]:[포트]
```

{% hint style="info" %}
권장 브라우저: Chrome, Edge (최신 버전). IE는 지원하지 않습니다.
{% endhint %}

### 화면 구조 <a href="#undefined" id="undefined"></a>

웹 UI는 **헤더**, **사이드바**, **콘텐츠 영역** 3개 부분으로 구성됩니다.

* **헤더**: 상단 고정. 애플리케이션 타이틀("Odyssey 설정")과 버전 정보를 표시합니다.
* **사이드바**: 좌측 메뉴. 각 설정 화면으로 이동하며, 하단에 "설정 적용" 버튼이 있습니다.
* **콘텐츠 영역**: 선택한 메뉴에 해당하는 설정 화면이 표시됩니다.

사이드바 메뉴 항목은 다음과 같습니다.

<table><thead><tr><th width="210.60003662109375">메뉴</th><th>설정 화면</th><th>대응 YAML 설정</th></tr></thead><tbody><tr><td>모니터링</td><td>실시간 발송 현황 + 발송 통계 (일/주/월)</td><td>— (조회 전용)</td></tr><tr><td>데이터베이스</td><td>DB 연결 정보 및 옵션</td><td><a href="https://mono-communications.github.io/odyssey-manual/#10-db-%EC%84%A4%EC%A0%95">10장</a></td></tr><tr><td>상세 설정</td><td>서비스 토글, 발송 파라미터</td><td><a href="https://mono-communications.github.io/odyssey-manual/#11-%EC%82%AC%EC%9A%A9-%EC%84%9C%EB%B9%84%EC%8A%A4">11장</a> ~ <a href="https://mono-communications.github.io/odyssey-manual/#13-%EA%B8%B0%EB%B3%B8-%EC%84%A4%EC%A0%95-commonuser">13장</a></td></tr><tr><td>세션 설정</td><td>통신사별 계정 관리</td><td><a href="https://mono-communications.github.io/odyssey-manual/#14-%EA%B3%84%EC%A0%95-%EC%84%A4%EC%A0%95-sessions">14장</a></td></tr><tr><td>발송 금지 시간</td><td>시간대별 발송 차단</td><td><a href="https://mono-communications.github.io/odyssey-manual/#13-%EA%B8%B0%EB%B3%B8-%EC%84%A4%EC%A0%95-commonuser">13장</a></td></tr><tr><td>로그 저장</td><td>로그 파일 조회 및 다운로드</td><td><a href="https://mono-communications.github.io/odyssey-manual/#22-%EB%A1%9C%EA%B7%B8--%EC%97%90%EB%9F%AC-%EB%B6%84%EC%84%9D">22장</a></td></tr><tr><td>이중화 설정</td><td>HA 운영 모드 선택 + <code>ha.properties</code> 편집</td><td><a href="https://mono-communications.github.io/odyssey-manual/#15-ha-%EC%9D%B4%EC%A4%91%ED%99%94-%EC%84%A4%EC%A0%95-haproperties">15장</a></td></tr></tbody></table>
