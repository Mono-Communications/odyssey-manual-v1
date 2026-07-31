# 2.패키지 구성

Odyssey는 **자립형 배포 패키지**로 구성됩니다. 시스템 자바, DB 드라이버, 매퍼 쿼리 등 운영 시 자주 바뀌는 영역을 외부 폴더로 분리해, jar 재빌드 없이 운영 환경에서 직접 변경할 수 있습니다.

## <mark style="color:$primary;">**Linux / Windows 패키지 구분**</mark> <a href="#linux-windows" id="linux-windows"></a>

고객사 OS 에 따라 두 가지 zip 패키지 중 하나를 받습니다.

<table><thead><tr><th width="130">패키지</th><th width="250">산출물</th><th>OS 전용 추가 파일</th></tr></thead><tbody><tr><td><strong>Linux</strong></td><td><mark style="color:red;"><code>odyssey-linux-1.0.0.zip</code></mark></td><td><code>start.sh</code> / <code>stop.sh</code></td></tr><tr><td><strong>Windows</strong></td><td><mark style="color:red;"><code>odyssey-windows-1.0.0.zip</code></mark></td><td><code>start.bat</code> / <code>stop.bat</code> / <code>installService.bat</code> / <code>unInstallService.bat</code></td></tr></tbody></table>

## <mark style="color:$primary;">**패키지 폴더 구조**</mark> <a href="#undefined" id="undefined"></a>

공통 영역(**`config/`**, **`lib/`**, **`auth/`**, **`upload/`** 등) 은 두 패키지가 동일하고, **`jre/` 만 OS별 다른 빌드** (Linux x64 ELF / Windows x64 PE) 가 동봉됩니다.

{% tabs %}
{% tab title="Linux 패키지 구성" %}
<figure><img src="../../.gitbook/assets/1_Linux_패키지.png" alt="그림 1. Linux 패키지 구성"><figcaption><p>그림 1. Linux 패키지 구성</p></figcaption></figure>
{% endtab %}

{% tab title="Windows 패키지 구성" %}
<figure><img src="../../.gitbook/assets/2_Windows_패키지.png" alt="그림 2. Windows 패키지 구성"><figcaption><p>그림 2. Windows 패키지 구성</p></figcaption></figure>
{% endtab %}
{% endtabs %}

### **공통 항목**

<table><thead><tr><th width="259">항목</th><th>설명</th></tr></thead><tbody><tr><td><strong><code>odyssey-1.0.0.jar</code></strong></td><td>자사 코드 (thin jar — 외부 <mark style="color:red;"><code>lib/</code></mark> 와 함께 동작)</td></tr><tr><td><strong><code>lib/</code></strong></td><td>외부 라이브러리 폴더 — Spring Boot, JDBC 드라이버, Netty 등 (<a href="2-4.-lib.md">2-4. lib폴더 — 외부라이브러리</a> 참고)</td></tr><tr><td><strong><code>libs/</code></strong></td><td>운영 모니터링 네이티브 라이브러리 폴더 — <mark style="color:red;"><code>cypher.dll</code></mark>(Windows) / <mark style="color:red;"><code>libcypher.so</code></mark>(Linux) (<a href="2-7.-libs.md">2-7. libs 폴더 — 네이티브 모니터링 라이브러리</a> 참고)</td></tr><tr><td><strong><code>jre/</code></strong></td><td>번들 Java 21 JRE — 시스템 자바와 무관하게 동작 (<a href="2-5.-jre-jre.md">2-5. jre 폴더 — 번들 JRE</a> 참고)</td></tr><tr><td><strong><code>config/</code></strong></td><td>환경설정 폴더 — <mark style="color:red;"><code>application.yaml</code>, <code>ha.properties</code></mark>, <mark style="color:red;"><code>mapper/</code></mark> 등(<a href="2-1.-config.md">2-1. config 폴더</a>, <a href="2-2.-config-mapper.md">2-2. config/mapper 폴더 — 매퍼 외부화</a> 참고)</td></tr><tr><td><strong><code>auth/</code></strong></td><td>KT 크로샷 세션 인증파일(<mark style="color:red;"><code>.cert</code></mark>) 폴더 (<a href="2-3.-auth.md">2-3. auth 폴더</a> 참고)</td></tr><tr><td><strong><code>upload/</code></strong></td><td>RCS, MMS, VMS 첨부 파일 폴더 (자동 업로드 사용 시)</td></tr><tr><td><strong><code>logs/</code></strong> (자동 생성)</td><td><p>실행 로그 폴더</p><ul><li><strong><code>live/</code></strong> — <mark style="color:red;"><code>system.log</code></mark>(전체 로그), <mark style="color:red;"><code>error.log</code></mark>, <mark style="color:red;"><code>router.log</code></mark> 등 모듈별 파일</li><li><strong><code>odyssey-pipeline.out</code></strong> — </li></ul></td></tr><tr><td><strong><code>pids/</code></strong> (자동 생성)</td><td>실행 중 프로세스 PID 파일 폴더</td></tr><tr><td><strong><code>log_backup/</code></strong> (자동 생성)</td><td>일별 압축 로그 백업</td></tr><tr><td><strong><code>backup/</code></strong> (자동 생성)</td><td>Web UI 설정 변경 백업</td></tr></tbody></table>

### **Linux 전용**

<table><thead><tr><th width="197">항목</th><th>설명</th></tr></thead><tbody><tr><td><strong><code>start.sh</code></strong> / <strong><code>stop.sh</code></strong></td><td>시작 / 종료 스크립트 (<a href="../4.-start-stop.md">4. 실행 / 정지</a> 참고)</td></tr></tbody></table>

### **Windows 전용**

<table><thead><tr><th width="229">항목</th><th>설명</th></tr></thead><tbody><tr><td><strong><code>start.bat</code></strong> / <strong><code>stop.bat</code></strong></td><td>수동 실행 / 종료 스크립트 — 더블클릭 또는 cmd 에서 실행 ( <a href="2-6.-windows.md">2-6. Windows 전용 파일</a> 참고)</td></tr><tr><td><strong><code>installService.bat</code></strong> / <strong><code>unInstallService.bat</code></strong></td><td>Windows 서비스 등록 / 해제 — 24/7 운영 시 사용</td></tr></tbody></table>

{% hint style="info" %}
자사 코드 jar 는 본체만 포함된 작은 파일(수백 KB)이며, 실제 의존 라이브러리는 외부 **`lib/`** 폴더에서 로딩됩니다. 드라이버 등 라이브러리 교체 시 jar 재빌드 없이 **`lib/`** 안의 jar 만 교체하면 됩니다.
{% endhint %}
