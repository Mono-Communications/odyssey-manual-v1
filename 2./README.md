# 2. 패키지 구성

Odyssey는 **자립형 배포 패키지**로 구성됩니다. 시스템 자바, DB 드라이버, 매퍼 쿼리 등 운영 시 자주 바뀌는 영역을 외부 폴더로 분리해, jar 재빌드 없이 운영 환경에서 직접 변경할 수 있습니다.

<table><thead><tr><th width="189">배포 형태</th><th width="248">실행 jar</th><th>용도</th></tr></thead><tbody><tr><td><strong><code>multi</code></strong> (UI 포함)</td><td><code>odyssey-app-1.0.0.jar</code></td><td>Web UI를 통한 설정·모니터링·로그 관리가 필요한 일반 고객사</td></tr><tr><td><strong><code>pipeline</code></strong> (엔진 단독)</td><td><code>odyssey-pipeline-1.0.0.jar</code></td><td>YAML로만 운영하며 Web UI가 필요하지 않은 고객사</td></tr></tbody></table>

### <mark style="color:$primary;">Linux / Windows 패키지 구분</mark> <a href="#linux-windows" id="linux-windows"></a>

고객사 OS 에 따라 두 가지 zip 패키지 중 하나를 받습니다.

<table><thead><tr><th width="113">패키지</th><th width="258">산출물</th><th>OS 전용 추가 파일</th></tr></thead><tbody><tr><td><strong>Linux</strong></td><td><code>odyssey-linux-1.0.0.zip</code></td><td><code>start.sh</code> / <code>stop.sh</code></td></tr><tr><td><strong>Windows</strong></td><td><code>odyssey-windows-1.0.0.zip</code></td><td><code>start.bat</code> / <code>stop.bat</code> / <code>installService.bat</code> / <code>unInstallService.bat</code> / <code>Odyssey.exe</code> / <code>Odyssey-multi.xml</code> / <code>Odyssey-pipeline.xml</code></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>

공통 영역(`config/`, `lib/`, `auth/`, `upload/`, jar 2종) 은 두 패키지가 동일하고, **`jre/` 만 OS별 다른 빌드** (Linux x64 ELF / Windows x64 PE) 가 동봉됩니다.

### <mark style="color:$primary;">패키지 폴더 구조</mark> <a href="#undefined" id="undefined"></a>

{% tabs %}
{% tab title="Linux 패키지 구성" %}
<figure><img src="../.gitbook/assets/image.png" alt="그림 1. Linux 패키지 구성"><figcaption><p>그림 1. Linux 패키지 구성</p></figcaption></figure>
{% endtab %}

{% tab title="Windows 패키지 구성" %}
<figure><img src="../.gitbook/assets/image (1).png" alt="그림 2. Windows 패키지 구성"><figcaption><p>그림 2. Windows 패키지 구성</p></figcaption></figure>
{% endtab %}
{% endtabs %}

#### **공통 항목**

<table><thead><tr><th width="283">항목</th><th>설명</th></tr></thead><tbody><tr><td><code>odyssey-app-1.0.0.jar</code> / <code>odyssey-pipeline-1.0.0.jar</code></td><td>자사 코드 (thin jar — 외부 lib/ 와 함께 동작)</td></tr><tr><td><code>lib/</code></td><td>외부 라이브러리 폴더 — Spring Boot, JDBC 드라이버, Netty 등 (자세히는 <a href="https://mono-communications.github.io/odyssey-manual/#2-4-lib-%ED%8F%B4%EB%8D%94-%E2%80%94-%EC%99%B8%EB%B6%80-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC">2-4 lib 폴더</a>)</td></tr><tr><td><code>libs/</code></td><td>운영 모니터링 네이티브 라이브러리 폴더 — <code>cypher.dll</code>(Windows) / <code>libcypher.so</code>(Linux) (자세히는 <a href="https://mono-communications.github.io/odyssey-manual/#2-7-libs-%ED%8F%B4%EB%8D%94-%E2%80%94-%EB%84%A4%EC%9D%B4%ED%8B%B0%EB%B8%8C-%EB%AA%A8%EB%8B%88%ED%84%B0%EB%A7%81-%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC">2-7 libs 폴더</a>)</td></tr><tr><td><code>jre/</code></td><td>번들 Java 21 JRE — 시스템 자바와 무관하게 동작 (자세히는 <a href="https://mono-communications.github.io/odyssey-manual/#2-5-jre-%ED%8F%B4%EB%8D%94-%E2%80%94-%EB%B2%88%EB%93%A4-jre">2-5 jre 폴더</a>)</td></tr><tr><td><code>config/</code></td><td>환경설정 폴더 — <code>application-HA.yaml</code>, <code>ha.properties</code>, <code>mapper/</code> (자세히는 <a href="https://mono-communications.github.io/odyssey-manual/#2-1-config-%ED%8F%B4%EB%8D%94">2-1 config 폴더</a>, <a href="https://mono-communications.github.io/odyssey-manual/#2-2-configmapper-%ED%8F%B4%EB%8D%94-%E2%80%94-%EB%A7%A4%ED%8D%BC-%EC%99%B8%EB%B6%80%ED%99%94">2-2 매퍼 외부화</a>)</td></tr><tr><td><code>auth/</code></td><td>KT 크로샷 세션 인증파일(<code>.cert</code>) 폴더</td></tr><tr><td><code>upload/</code></td><td>RCS MMS 첨부 이미지 파일 폴더 (자동 업로드 사용 시)</td></tr><tr><td><code>log/</code> (자동 생성)</td><td>실행 로그 폴더 — <code>agent.log</code>(전체 로그), <code>error.log</code>, <code>router.log</code> 등 모듈별 파일</td></tr><tr><td><code>pids/</code> (자동 생성)</td><td>실행 중 프로세스 PID 파일 폴더</td></tr><tr><td><code>log_backup/</code> (자동 생성)</td><td>일별 압축 로그 백업</td></tr><tr><td><code>backup/</code> (자동 생성)</td><td>Web UI 설정 변경 백업</td></tr></tbody></table>

**Linux 전용**

<table><thead><tr><th width="265">항목</th><th>설명</th></tr></thead><tbody><tr><td><code>start.sh</code> / <code>stop.sh</code></td><td>시작 / 종료 스크립트 (자세히는 <a href="https://mono-communications.github.io/odyssey-manual/#4-%EC%8B%A4%ED%96%89--%EC%A0%95%EC%A7%80">4장 실행 / 정지</a>)</td></tr></tbody></table>

**Windows 전용**

<table><thead><tr><th width="217">항목</th><th>설명</th></tr></thead><tbody><tr><td><code>start.bat</code> / <code>stop.bat</code></td><td>수동 실행 / 종료 스크립트 — 더블클릭 또는 cmd 에서 실행 (자세히는 <a href="https://mono-communications.github.io/odyssey-manual/#2-6-windows-%EC%A0%84%EC%9A%A9-%ED%8C%8C%EC%9D%BC">2-6 Windows 전용 파일</a>)</td></tr><tr><td><code>installService.bat</code> / <code>unInstallService.bat</code></td><td>Windows 서비스 등록 / 해제 — 24/7 운영 시 사용</td></tr><tr><td><code>Odyssey.exe</code></td><td>WinSW (Windows Service Wrapper) — 서비스 등록의 wrapper 역할</td></tr><tr><td><code>Odyssey-multi.xml</code> / <code>Odyssey-pipeline.xml</code></td><td>서비스 모드별 설정 template — <code>installService.bat</code> 이 메뉴 선택에 따라 활성화</td></tr></tbody></table>

{% hint style="info" %}
자사 코드 jar 는 본체만 포함된 작은 파일(수백 KB)이며, 실제 의존 라이브러리는 외부 `lib/` 폴더에서 로딩됩니다. 드라이버 등 라이브러리 교체 시 jar 재빌드 없이 lib/ 안의 jar 만 교체하면 됩니다.
{% endhint %}
