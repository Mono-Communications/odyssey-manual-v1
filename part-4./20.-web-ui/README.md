# 20. Web UI 상세

**Odyssey**는 브라우저 기반의 웹 설정 UI를 제공합니다. 실시간 모니터링 및 로그 관리를 수행할 수 있습니다.

### <mark style="color:blue;">접속 방법</mark> <a href="#undefined" id="undefined"></a>

**Odyssey**가 구동된 상태에서 브라우저로 다음 주소에 접속합니다.

```
http://[서버IP]:[포트]
```

{% hint style="info" %}
권장 브라우저: Chrome, Edge (최신 버전). IE는 지원하지 않습니다.
{% endhint %}

### <mark style="color:blue;">화면 구조</mark> <a href="#undefined" id="undefined"></a>

* 웹 UI는 **헤더**, **사이드바**, **콘텐츠 영역** 3개 부분으로 구성됩니다.
  * **헤더**: 상단 고정. 애플리케이션 타이틀("**Odyssey** 설정")과 버전 정보를 표시합니다.
  * **사이드바**: 좌측 메뉴. 각 설정 화면으로 이동하며, 하단에 "설정 적용" 버튼이 있습니다.
  * **콘텐츠 영역**: 선택한 메뉴에 해당하는 설정 화면이 표시됩니다.
* 사이드바 메뉴 항목은 다음과 같습니다.

<table><thead><tr><th width="198.2000732421875">메뉴</th><th width="482.800048828125">설정 화면</th></tr></thead><tbody><tr><td><strong>파이프라인 모니터링</strong></td><td>실시간 발송 현황 + System Health 체크</td></tr><tr><td><strong>스레드 모니터링</strong></td><td>스레드 현황 및 기능 별 스레드 상세 목록</td></tr><tr><td><strong>DB 모니터링</strong></td><td>DB 연결 정보 및 처리 현황</td></tr><tr><td><strong>로그 모니터링</strong></td><td>로그 파일 조회 및 다운로드</td></tr><tr><td><strong>네트워크 모니터링</strong></td><td>통신사 별 + 계정 별 연결 상태 모니터링</td></tr><tr><td><strong>메시징 통계</strong></td><td>기간 별 발송 현황 및 메시지 타입 별 통계 분석</td></tr><tr><td><strong>발송 금지 시간</strong></td><td>시간대 별 발송 차단 설정</td></tr></tbody></table>
