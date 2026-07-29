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

* 웹 UI는 **헤더**, **사이드바**, **콘텐츠 영역** 3개 부분으로 구성됩니다.
  * **헤더**: 상단 고정. 애플리케이션 타이틀("Odyssey 설정")과 버전 정보를 표시합니다.
  * **사이드바**: 좌측 메뉴. 각 설정 화면으로 이동하며, 하단에 "설정 적용" 버튼이 있습니다.
  * **콘텐츠 영역**: 선택한 메뉴에 해당하는 설정 화면이 표시됩니다.
* 사이드바 메뉴 항목은 다음과 같습니다.

<table><thead><tr><th width="140.2000732421875">메뉴</th><th width="236.800048828125">설정 화면</th><th>대응 YAML 설정 참고</th></tr></thead><tbody><tr><td>모니터링</td><td>실시간 발송 현황 + 발송 통계 (일/주/월)</td><td>— (조회 전용)</td></tr><tr><td>데이터베이스</td><td>DB 연결 정보 및 옵션</td><td><a href="../../part-2./10.-db.md">10. DB 설정</a></td></tr><tr><td>상세 설정</td><td>서비스 토글, 발송 파라미터</td><td><a href="../../part-2./11..md">11. 사용 서비스</a> ~ <a href="../../part-2./13.-common.user.md">13. 기본 설정 (common.user)</a></td></tr><tr><td>세션 설정</td><td>통신사별 계정 관리</td><td><a href="../../part-2./14.-sessions/">14. 계정 설정 (sessions)</a></td></tr><tr><td>발송 금지 시간</td><td>시간대별 발송 차단</td><td><a href="../../part-2./13.-common.user.md">13. 기본 설정 (common.user)</a></td></tr><tr><td>로그 저장</td><td>로그 파일 조회 및 다운로드</td><td><a href="../22..md">22. 로그 / 에러 분석</a></td></tr><tr><td>이중화 설정</td><td>HA 운영 모드 선택 + <code>ha.properties</code> 편집</td><td><a href="../../part-2./15.-ha-ha.properties/">15. HA 이중화 설정 (ha.properties)</a></td></tr></tbody></table>
