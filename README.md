# Odyssey 통합 매뉴얼

> **버전**: v1\
> **작성일**: 2026.04.27\
> **고객센터**: 02-333-7223

## 들어가기 전에

이 프로그램은 본질적으로 외부의 위험한 상황에서 사용하도록 개발된 것이 아닙니다. 따라서 그런 목적으로 사용된 경우, 사용자는 응용 프로그램의 안전한 사용을 보장하기 위한 모든 적절한 안전 조치, 백업, 대비 및 기타 조치를 반드시 취해야 합니다. 프로그램이 이러한 목적으로 사용되었을 경우 ㈜모노커뮤니케이션즈는 이러한 프로그램 사용으로 인한 피해를 책임지지 않습니다.

이 프로그램(소프트웨어와 설명서 포함)은 저작권법, 특허 및 기타 지적재산권 관련 법규에 의해 보호됩니다. 이 프로그램을 리버스 엔지니어링하거나 분해하거나 또는 역 컴파일하는 것은 금지되어 있습니다.

사용자는 시스템 해킹을 방지하기 위하여 백신 프로그램을 이용한 주기적인 PC 관리를 하여야 하며, 아이디/비밀번호를 외부로 노출할 수 없고, 지정된 장소에서만 프로그램을 사용하여야 합니다.

이 문서의 내용은 사전 공지 없이 변경될 수 있습니다.

## Part 1. 시작 가이드 (Getting Started)

> 본 파트는 Odyssey 패키지를 받은 시점부터 첫 SMS 실발송 성공까지의 단계별 가이드입니다. Odyssey를 처음 설치하는 운영자라면 본 파트만 따라가도 첫 발송에 도달할 수 있습니다.

## 1. Odyssey 실행 환경

| 항목       | 요구 사항                                                                                                                                          |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| **자바**   | **Java 21 이상**. 기본 패키지에 Java 21 JRE 가 동봉되어 있어 별도 설치 없이 그대로 동작합니다. 고객사가 Java 21 을 자체 설치한 환경이라면 패키지에서 jre/ 폴더를 제거하면 시스템 Java 로 자동 fallback 합니다.  |
| **DB**   | MySQL 5.7 / 8.0 이상 (UTF-8 환경).                                                                                                                 |
| **OS**   | **Linux x64 (glibc)** 또는 **Windows x64**. OS별 별도 zip 패키지 제공 — Linux 는 RHEL / Ubuntu / CentOS 등 일반 엔터프라이즈 배포판, Windows 는 Win10 / Server 2016 이상 |
| **메모리**  | 최소 1GB, 권장 2GB 이상                                                                                                                              |
| **네트워크** | DB 서버 접근, 게이트웨이 IP/PORT outbound 허용                                                                                                            |

## 2. 패키지 구성

Odyssey는 **자립형 배포 패키지**로 구성됩니다. 시스템 자바, DB 드라이버, 매퍼 쿼리 등 운영 시 자주 바뀌는 영역을 외부 폴더로 분리해, jar 재빌드 없이 운영 환경에서 직접 변경할 수 있습니다.

| 배포 형태                | 실행 jar                     | 용도                                   |
| -------------------- | -------------------------- | ------------------------------------ |
| **multi** (UI 포함)    | odyssey-app-1.0.0.jar      | Web UI를 통한 설정·모니터링·로그 관리가 필요한 일반 고객사 |
| **pipeline** (엔진 단독) | odyssey-pipeline-1.0.0.jar | YAML로만 운영하며 Web UI가 필요하지 않은 고객사      |

### Linux / Windows 패키지 구분

고객사 OS 에 따라 두 가지 zip 패키지 중 하나를 받습니다.

| 패키지         | 산출물                       | OS 전용 추가 파일                                                                                                               |
| ----------- | ------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **Linux**   | odyssey-linux-1.0.0.zip   | start.sh / stop.sh                                                                                                        |
| **Windows** | odyssey-windows-1.0.0.zip | start.bat / stop.bat / installService.bat / unInstallService.bat / Odyssey.exe / Odyssey-multi.xml / Odyssey-pipeline.xml |

공통 영역(`config/`, `lib/`, `auth/`, `upload/`, jar 2종) 은 두 패키지가 동일하고, **`jre/` 만 OS별 다른 빌드** (Linux x64 ELF / Windows x64 PE) 가 동봉됩니다.

### 패키지 폴더 구조

!\[Linux 패키지 구성]\(./images/Odyssey 구버전 패키징 구성\_linux.png)

그림 1. Linux 패키지 구성

!\[Windows 패키지 구성]\(./images/Odyssey 구버전 패키징 구성\_window.png)

그림 2. Windows 패키지 구성

#### 공통 항목

| 항목                                                 | 설명                                                                |
| -------------------------------------------------- | ----------------------------------------------------------------- |
| odyssey-app-1.0.0.jar / odyssey-pipeline-1.0.0.jar | 자사 코드 (thin jar — 외부 lib/ 와 함께 동작)                                |
| lib/                                               | 외부 라이브러리 폴더 — Spring Boot, JDBC 드라이버, Netty 등                     |
| libs/                                              | 운영 모니터링 네이티브 라이브러리 폴더 — cypher.dll(Windows) / libcypher.so(Linux) |
| jre/                                               | 번들 Java 21 JRE — 시스템 자바와 무관하게 동작                                  |
| config/                                            | 환경설정 폴더 — application-HA.yaml, ha.properties, mapper/             |
| auth/                                              | KT 크로샷 세션 인증파일(.cert) 폴더                                          |
| upload/                                            | RCS MMS 첨부 이미지 파일 폴더 (자동 업로드 사용 시)                                |
| log/ (자동 생성)                                       | 실행 로그 폴더 — agent.log(전체 로그), error.log, router.log 등 모듈별 파일       |
| pids/ (자동 생성)                                      | 실행 중 프로세스 PID 파일 폴더                                               |
| log\_backup/ (자동 생성)                               | 일별 압축 로그 백업                                                       |
| backup/ (자동 생성)                                    | Web UI 설정 변경 백업                                                   |

#### Linux 전용

| 항목                 | 설명           |
| ------------------ | ------------ |
| start.sh / stop.sh | 시작 / 종료 스크립트 |

#### Windows 전용

| 항목                                        | 설명                                                       |
| ----------------------------------------- | -------------------------------------------------------- |
| start.bat / stop.bat                      | 수동 실행 / 종료 스크립트 — 더블클릭 또는 cmd 에서 실행                      |
| installService.bat / unInstallService.bat | Windows 서비스 등록 / 해제 — 24/7 운영 시 사용                       |
| Odyssey.exe                               | WinSW (Windows Service Wrapper) — 서비스 등록의 wrapper 역할     |
| Odyssey-multi.xml / Odyssey-pipeline.xml  | 서비스 모드별 설정 template — installService.bat 이 메뉴 선택에 따라 활성화 |

{% hint style="info" %}
자사 코드 jar 는 본체만 포함된 작은 파일(수백 KB)이며, 실제 의존 라이브러리는 외부 `lib/` 폴더에서 로딩됩니다. 드라이버 등 라이브러리 교체 시 jar 재빌드 없이 lib/ 안의 jar 만 교체하면 됩니다.
{% endhint %}

### 2-1. config 폴더

!\[config 폴더 내부]\(./images/Odyssey 패키징 - config 폴더 내부.png)

그림 3. config 폴더 내부 (application-HA.yaml + ha.properties + mapper/)

| 항목                  | 역할                                         |
| ------------------- | ------------------------------------------ |
| application-HA.yaml | DB, 사용 서비스, 세션, Poseidon 등 모든 운영 설정        |
| ha.properties       | HA 이중화 노드 정보, DB Lease, 로드밸런싱 (HA 운영 시 필수) |
| mapper/             | MyBatis 매퍼 XML — DBMS별 폴더 구성               |

### 2-2. config/mapper 폴더 — 매퍼 외부화

운영 중 SQL 쿼리(메시지 조회, 통계, INSERT 등)를 변경해야 할 때 jar 재빌드 없이 외부 폴더의 XML 만 수정하면 됩니다. 변경 후 재시작이 필요합니다.

!\[config/mapper/{dbms}/ 구성]\(./images/Odyssey 패키징 - config 폴더 내부 - dbms.png)

그림 4. config/mapper/{dbms}/ 구성 (현재 mysql 지원)

DBMS별 폴더 안에 5종의 매퍼 파일이 있습니다.

!\[DBMS 폴더 내부 매퍼 파일]\(./images/Odyssey 패키징 - config 폴더 내부 - dbms - 쿼리.png)

그림 5. DBMS 폴더 내부 매퍼 파일 5종

| 파일              | 역할                |
| --------------- | ----------------- |
| selectQuery.xml | 메시지 조회 (FETCH) 쿼리 |
| insertQuery.xml | INSERT 쿼리         |
| updateQuery.xml | 상태 갱신 쿼리          |
| deleteQuery.xml | DELETE / 이관 쿼리    |
| table.xml       | 테이블 자동 생성 DDL     |

#### 동작 원리 — 외부 우선 + classpath fallback

Odyssey는 시작 시 매퍼를 다음 순서로 로드합니다.

{% stepper %}
{% step %}
## 외부 우선

`./config/mapper/{dbms}/*.xml` 에 파일이 1개 이상 있으면 외부 폴더 사용
{% endstep %}

{% step %}
## classpath fallback

외부 폴더가 비어있거나 누락되면 jar 안에 동봉된 기본 매퍼 사용 (안전망)
{% endstep %}
{% endstepper %}

시작 로그에서 어느 경로가 사용 중인지 확인할 수 있습니다.

```
# 외부 폴더 사용 시 (정상)
INFO MyBatis mappers: external [file:./config/mapper/mysql/*.xml] -> 5 files

# 또는 fallback 시
INFO MyBatis mappers: classpath fallback [classpath:/mapper/mysql/*.xml] -> 5 files
```

#### 운영 워크플로우

{% stepper %}
{% step %}
## 매퍼 수정

```bash
vi config/mapper/mysql/selectQuery.xml
```
{% endstep %}

{% step %}
## 재시작

```bash
./stop.sh
./start.sh multi
```
{% endstep %}
{% endstepper %}

{% hint style="info" %}
핫 리로드는 지원하지 않습니다. 변경 후 반드시 재시작하세요.
{% endhint %}

{% hint style="warning" %}
XML 문법 오류가 있으면 기동에 실패합니다. 변경 후 반드시 시작 로그에서 매퍼 로드 결과를 확인하세요.
{% endhint %}

### 2-3. auth 폴더

!\[auth 폴더 내부]\(./images/Odyssey 패키징 - auth 폴더 내부.png)

그림 6. auth 폴더 내부 (.cert 인증파일)

KT 크로샷 세션 인증파일(`.cert`)을 보관합니다. 세션마다 다른 파일이 들어가며, 파일명은 `application-HA.yaml`의 `kt.sessions[].auth-file` 값과 정확히 일치해야 합니다.

{% hint style="info" %}
`.cert` 파일은 대소문자를 구분합니다. Linux 환경에서 특히 주의하세요.
{% endhint %}

### 2-4. lib 폴더 — 외부 라이브러리

!\[lib 폴더 내부]\(./images/Odyssey 패키징 - 외부 lib.png)

그림 7. lib 폴더 내부 (외부 라이브러리 약 130개)

Spring Boot, JDBC 드라이버, Netty 등 모든 외부 라이브러리가 들어있습니다 (약 130개 `.jar`). `start.sh` 가 `-cp "lib/*"` 와일드카드로 자동 인식합니다.

#### DB 드라이버 교체 시나리오

고객사 DB가 MySQL 5.x인 경우, 기본 동봉된 드라이버를 5.x용으로 교체할 수 있습니다.

{% stepper %}
{% step %}
## 기본 드라이버 제거

```bash
cd /path/to/odyssey/lib
rm mysql-connector-j-*.jar
```
{% endstep %}

{% step %}
## 호환 드라이버 추가

```bash
cp /tmp/mysql-connector-java-5.1.49.jar lib/
```
{% endstep %}

{% step %}
## 재시작

```bash
./stop.sh
./start.sh multi
```
{% endstep %}
{% endstepper %}

{% hint style="info" %}
**드라이버 교체 시 yaml도 함께 확인**해야 합니다. `driver-class-name` 과 `jdbc-url` 옵션이 버전마다 다릅니다.
{% endhint %}

| 항목                | MySQL 8.x                                  | MySQL 5.x                                 |
| ----------------- | ------------------------------------------ | ----------------------------------------- |
| driver-class-name | com.mysql.cj.jdbc.Driver                   | com.mysql.jdbc.Driver                     |
| URL 옵션 차이         | useSSL=false\&allowPublicKeyRetrieval=true | useSSL=false\&serverTimezone=Asia/Seoul 등 |

다른 DBMS 드라이버(`postgresql-*.jar`, `mssql-jdbc-*.jar`, `mariadb-java-client-*.jar`, `ojdbc11-*.jar`)도 동일한 방식으로 교체할 수 있습니다.

{% hint style="info" %}
`lib/` 안에는 **외부 라이브러리만** 들어있습니다. `odyssey-app-*.jar`, `odyssey-pipeline-*.jar` 같은 자사 코드는 패키지 루트에 위치하며, 임의로 변경하지 마세요.
{% endhint %}

### 2-5. jre 폴더 — 번들 JRE

!\[jre 폴더 내부]\(./images/Odyssey 패키징 - jre.png)

그림 8. jre 폴더 내부 (Java 21 LTS 번들)

자체 동봉된 **Java 21 LTS** JRE 입니다. 기본적으로 Odyssey는 시스템에 설치된 자바와 **무관하게** 이 폴더의 JRE만으로 동작하며, 고객사가 Java 21 을 자체 운영하는 환경이라면 jre 폴더를 제거하여 시스템 Java 로 전환할 수도 있습니다.

#### Java 결정 우선순위

`start.sh` 는 기동 시 다음 순서로 사용할 Java 를 결정합니다.

| 순위 | 조건                                  | 사용 Java                     |
| -- | ----------------------------------- | --------------------------- |
| 1  | ./jre/ 폴더 존재 + ./jre/bin/java 실행 가능 | **번들 JRE** (./jre/bin/java) |
| 2  | ./jre/ 폴더 없음 + 시스템 PATH 에 java 존재   | **시스템 Java** (java)         |
| 실패 | 둘 다 없음 또는 Java 21 미만                | 기동 거부 + 에러 안내               |

시작 시 다음과 같은 INFO 로그로 어느 Java 가 선택됐는지 확인할 수 있습니다.

```
# 번들 JRE 사용 시
INFO Java: ./jre/bin/java (bundled JRE (./jre))

# 시스템 Java 사용 시
INFO Java: java (system Java (PATH))
```

#### 시스템 Java 사용 운영 패턴

```bash
# 패키지에서 jre 폴더만 제거 (다른 폴더 그대로)
rm -rf jre/

# 시스템 Java 21 확인
java -version
# → openjdk version "21.0.x" ... 또는 동등 버전

# 그대로 기동 — start.sh 가 시스템 Java 자동 사용
./start.sh multi
```

{% hint style="info" %}
시스템 Java 사용 시에도 **Java 21 이상이 필수**입니다 (Spring Boot 3.5.x 최소 요구사항). 미만 버전이면 `start.sh` 가 명확한 에러 메시지로 기동을 거부합니다.
{% endhint %}

#### 검증 명령

```bash
# 번들 JRE 버전 확인 (jre/ 동봉 환경)
./jre/bin/java -version
# → openjdk version "21.0.x" ...  (Linux x64)

# 실행 중인 프로세스가 어느 Java 로 떠 있는지 확인
ps -ef | grep odyssey
# → 번들 사용 시: 명령줄에 ./jre/bin/java 절대경로
# → 시스템 사용 시: 명령줄에 java (PATH 에서 해석됨)
```

#### 첫 실행 전 — Linux 측 실행 비트 복원

패키지 전송 방식(scp, zip 압축 등)에 따라 실행 비트가 손실될 수 있습니다. 첫 실행 전 한 번 복원합니다.

```bash
chmod -R +x jre/bin start.sh stop.sh
```

{% hint style="info" %}
번들 JRE는 OS별 다른 빌드입니다 — Linux 패키지에는 Linux x64 (glibc), Windows 패키지에는 Windows x64 (PE32+) 가 동봉됩니다. 폴더명(`jre/`)은 동일하지만 내부 바이너리는 OS 전용이라 서로 호환되지 않습니다.
{% endhint %}

### 2-6. Windows 전용 파일

Windows 패키지에는 운영자가 직접 사용하는 4개 .bat 와, Windows 서비스 등록 시 자동으로 사용되는 wrapper 파일들이 들어있습니다.

| 파일                                        | 역할                                                                       | 직접 실행/편집 |
| ----------------------------------------- | ------------------------------------------------------------------------ | -------- |
| start.bat / stop.bat                      | 수동 실행 / 정지 (Linux start.sh / stop.sh 와 1:1 대응)                           | ✅ 사용     |
| installService.bat / unInstallService.bat | Windows 서비스 등록 / 해제 (UAC 자동 요청, 메뉴로 multi/pipeline 선택)                   | ✅ 사용     |
| Odyssey.exe                               | WinSW (Windows Service Wrapper) — 서비스에 등록되는 실행 파일                        | ❌        |
| Odyssey-multi.xml / Odyssey-pipeline.xml  | 모드별 서비스 설정 template                                                      | ❌        |
| Odyssey.xml (자동 생성)                       | active 서비스 설정 — installService.bat 시 동적 생성, unInstallService.bat 시 자동 삭제 | ❌        |

{% hint style="warning" %}
`Odyssey.exe`, `Odyssey*.xml` 은 `installService.bat` 가 자동으로 처리하는 내부 파일입니다. **운영자/고객지원팀이 직접 실행하거나 편집할 필요가 없습니다.**
{% endhint %}

### 2-7. libs 폴더 — 네이티브 모니터링 라이브러리

운영 모니터링용 네이티브 라이브러리가 들어있는 폴더입니다. OS별로 다른 바이너리가 동봉됩니다.

| 파일           | OS          |
| ------------ | ----------- |
| cypher.dll   | Windows x64 |
| libcypher.so | Linux x64   |

start 스크립트(및 Windows 서비스)가 이 폴더를 통해 라이브러리를 로딩합니다. **폴더와 파일을 삭제하거나 다른 위치로 옮기지 마세요.** 없어도 메시지 발송 기능 자체는 정상 동작하지만, 운영 모니터링 신호가 수집되지 않습니다.

{% hint style="info" %}
`jre/` 와 마찬가지로 OS 전용 바이너리입니다. Linux 패키지에는 `libcypher.so`, Windows 패키지에는 `cypher.dll` 만 동봉됩니다.
{% endhint %}

## 3. 첫 실행에 꼭 필요한 설정

`config/application-HA.yaml`을 열어 아래 항목들을 운영 환경에 맞게 입력합니다.

### 3-1. DB 연결 (`spring.datasource.hikari`)

```yaml
spring:
  datasource:
    hikari:
      driver-class-name: com.mysql.cj.jdbc.Driver
      jdbc-url: jdbc:mysql://{{ip}}:{{port}}/{{database}}?useUnicode=true&characterEncoding=UTF-8&useSSL=false&allowPublicKeyRetrieval=true
      username: {{id}}
      password: {{pw}}        # OTP 기반 암호문 입력 권장
```

| 항목       | 입력                      |
| -------- | ----------------------- |
| jdbc-url | 고객사 DB 서버 IP / 포트 / DB명 |
| username | DB 접속 계정                |
| password | DB 접속 패스워드              |

### 3-2. 사용 메시지 종류 (`common.execute`)

발송할 메시지 종류만 `true`로 설정합니다. 사용하지 않는 종류는 `false`로 두면 불필요한 DB 폴링이 줄어 부하가 낮아집니다.

```yaml
common:
  execute:
    sms: true
    lms: true
    mms: true
    rcs: false       # RCS 사용 시 true
    kakao: false     # 카카오 알림톡/친구톡 사용 시 true
    fetch: true      # 로그 이관 (HA 운영 시 true 권장)
```

### 3-3. 발송 경로 (`common.transmission`)

각 메시지 그룹별로 어떤 게이트웨이를 통해 발송할지 지정합니다. **반드시 계약된 게이트웨이와 일치**해야 합니다.

```yaml
common:
  transmission:
    msg: KT          # 문자: KT (KT 크로샷) | CPAAS
    rcs: KT          # RCS: KT (KT RCS Hermes API) | CPAAS
    kakao: CPAAS     # 카카오: MN (엠앤와이즈) | CPAAS
```

### 3-4. 테이블명 (`common.tables.table-name`)

Odyssey가 자동 생성할 테이블 이름을 지정합니다. 일반적으로 기본값을 사용하며, 고객사 DB에 같은 이름의 기존 테이블이 있는 경우에만 충돌 방지를 위해 변경합니다.

```yaml
common:
  tables:
    table-name:
      rv-submit: ODYSSEY
      rv-submit-log: ODYSSEY_LOG
      rv-stat: ODYSSEY_STAT
      rv-file: ODYSSEY_RCSFILE
      rv-tmpl-stat: ODYSSEY_TEMPLATE_STAT
```

{% hint style="info" %}
위 5개 테이블 + `ha_lease`, `PAUSE_INFO` 테이블은 Odyssey 최초 기동 시 자동 생성됩니다. 운영 환경에서는 미리 DB CREATE/INSERT/SELECT 권한을 부여해 두시기 바랍니다.
{% endhint %}

### 3-5. 발송 처리 건수 (`common.tables.fetch-count`)

각 서비스가 1초당 DB에서 가져와 발송할 최대 메시지 건수입니다.

```yaml
common:
  tables:
    fetch-count:
      sms: 200
      lms: 200
      mms: 50
      rcs: 60
      kakao: 400
      fetch: 1000
```

{% hint style="info" %}
각 세션의 `max-cnt` 합과 같거나 약간 큰 값으로 설정하는 것이 원칙입니다. 세션 한도 이상으로 늘려도 게이트웨이에서 차단되어 의미가 없습니다.
{% endhint %}

### 3-6. 게이트웨이 세션 (사용하는 것만)

`common.transmission`에서 지정한 게이트웨이의 세션 정보를 입력합니다. 사용하지 않는 게이트웨이 영역은 통째로 주석 처리하거나 삭제합니다.

각 세션의 `max-cnt`는 **계약한 초당 발송 한도와 정확히 일치**시켜야 합니다.

#### KT 크로샷 (`transmission.msg = KT`)

```yaml
kt:
  sessions:
    - seq: 1
      rcs-ip: rcs.xroshot.com
      sp-id: {{xroshot_id}}
      sp-pwd: {{xroshot_pw}}      
      end-user: {{user}}
      auth-file: {{cert_file}}    # auth/ 폴더의 .cert 파일명과 일치
      max-cnt: 200                # 권장
      sms: true
      lms: true
      mms: true
```

#### KT RCS (`transmission.rcs = KT`)

```yaml
rcs:
  sessions:
    - seq: 1
      send-url: https://agency.hermes.kt.com/corp/v1
      report-url: https://query.hermes.kt.com/corp/v1
      rcs-id: {{rcs_id}}
      rcs-secret: {{rcs_pw}}       
      agencyid: ktbizrcs
      max-cnt: 30                  # 권장
```

#### CPaaS (`transmission.msg = CPAAS` / `rcs = CPAAS` / `kakao = CPAAS`)

```yaml
cpaas:
  sessions:
    - seq: 1
      send-url: https://api.communis.kt.com/cpaas/v2.0
      report-url: https://api.communis.kt.com/cpaas/v2.0
      api-id: {{communis_id}}
      api-pw: {{communis_pw}}      
      sender-key: {{kakao_senderkey}}
      max-cnt: 20                  # 권장
```

#### 엠앤와이즈 카카오 (`transmission.kakao = MN`)

```yaml
kakao:
  sessions:
    - seq: 1
      send-url: https://wt-api.carrym.com:8443/v3
      report-url: https://wt-api.carrym.com:8443/v3
      api-id: {{api_id}}
      api-key: {{api_key}}
      sender-key: {{sender_key}}
      max-cnt: 0
```

### 3-7. RCS 발송 시 추가 설정 (`common.user`)

CPaaS RCS로 발송하는 경우 다음 KEY를 입력합니다. RCS 청약 시 발급받습니다.

```yaml
common:
  user:
    agencykey: {{agency_key}}    # 대행사 KEY
    brandid: {{brand_id}}        # 브랜드 ID
    brandkey: {{brand_key}}      # 브랜드 KEY
```

{% hint style="info" %}
RCS를 사용하지 않는 환경은 빈 문자열(`''`) 또는 키 자체를 생략해도 됩니다.
{% endhint %}

### 그 외 옵션

`common.user`의 ping/restart 타이밍, RCS MMS 자동 업로드, OTP 등 세부 옵션은 모두 기본값이 안전합니다.

## 4. 실행 / 정지

배포 패키지에는 사전 빌드된 thin jar(`odyssey-app-1.0.0.jar`, `odyssey-pipeline-1.0.0.jar`)와 번들 JRE(`jre/`), 외부 라이브러리(`lib/`)가 포함되어 있어, 별도 빌드 없이 바로 기동할 수 있습니다.

### Linux

Odyssey 설치 폴더에서 다음 명령을 실행합니다. `start.sh` 는 자동으로 적절한 Java 를 선택하고(`jre/` 동봉 시 번들 JRE, 미동봉 시 시스템 Java 21) 외부 `lib/` 를 classpath 와일드카드로 인식합니다.

```bash
# 시작 — multi 모드 (엔진 + Web UI)
./start.sh multi

# 시작 — pipeline 모드 (엔진 단독)
./start.sh pipeline

# 정지 (graceful, 최대 30초 대기)
./stop.sh

# 강제 정지
./stop.sh all force
```

{% hint style="info" %}
첫 실행 전 한 번만 실행 비트 복원: `chmod +x start.sh stop.sh` (번들 JRE 동봉 시 `chmod -R +x jre/bin` 도 함께 실행)
{% endhint %}

### Windows

Windows 패키지는 두 가지 운영 모드를 제공합니다 — **수동 실행** (테스트/임시) 과 **Windows 서비스 등록** (24/7 운영, 권장).

#### 수동 실행

cmd 또는 탐색기 더블클릭으로 실행. 사용자 로그인 세션에 묶여 있어 로그아웃 시 종료됩니다.

```cmd
start.bat                    :: 메뉴로 multi/pipeline 선택
start.bat multi              :: 또는 인자로 직접
stop.bat                     :: 모두 정지
```

#### Windows 서비스 등록 (24/7 운영)

`installService.bat` 더블클릭(또는 cmd 실행) → UAC 권한 자동 요청 → 메뉴에서 모드 선택 → **서비스 등록 + 시작이 한 번에 처리됩니다.** 부팅 시 자동 시작 + 죽으면 자동 재시작 + 사용자 로그아웃 무관 동작.

!\[installService.bat 실행 화면]\(./images/Odyssey 패키징 - window installer.png)

그림 24. installService.bat 실행 — 모드 선택 후 서비스 자동 등록 + 시작

```cmd
installService.bat           :: 메뉴로 multi/pipeline 선택
installService.bat multi     :: 또는 인자로 직접
unInstallService.bat         :: 서비스 정지 + 등록 해제
```

등록 후 운영:

```cmd
sc query Odyssey             :: 상태 확인
net stop Odyssey             :: 정지
net start Odyssey            :: 시작
```

또는 `services.msc` 에서 "Odyssey" 항목 우클릭으로 GUI 조작 가능.

{% hint style="warning" %}
수동 모드와 서비스 모드를 동시에 실행하지 마세요 (포트/DB 락 충돌). 한 모드만 골라 운영. 설치 경로는 한글/공백 없는 영문(예: `C:\Odyssey\`) 권장.
{% endhint %}

### 정상 기동 확인

`log/agent.log`(또는 모드별 `log/odyssey-app.out` / `log/odyssey-pipeline.out`)에 다음과 유사한 메시지가 출력됩니다.

```
Java: ./jre/bin/java (bundled JRE (./jre))
MyBatis mappers: external [file:./config/mapper/mysql/*.xml] -> 5 files
Database Driver Load Success.
DBMS=[MySQL], URL=jdbc:mysql://**.**.**.**/****
Mono Messaging Service agent=[Odyssey-1.0.0] starts.
Exist Table Name=[ODYSSEY]
Exist Table Name=[ODYSSEY_RCSFILE]
SendKT Thread Start
```

{% hint style="info" %}
시작 로그의 핵심 줄 — `Java: ...` (어느 Java 사용 중), `MyBatis mappers: external ...` (외부 매퍼 정상 로드), `Poseidon integration disabled` (Poseidon 미연동 환경에서만, 정상).
{% endhint %}

## 5. Web UI 살펴보기 (multi 모드 한정)

`multi` 모드로 기동한 경우, 브라우저로 다음 주소에 접속하면 Web UI가 표시됩니다.

```
http://[서버IP]:[포트]
```

기본 포트는 `application-HA.yaml`의 `server.port` 값(`8090`)입니다.

!\[모니터링 대시보드 — 실시간 발송 현황]\(./images/01. 모니터링 화면.png)

그림 9. 모니터링 대시보드 — 실시간 발송 현황 (파이프라인, 큐 사이즈, TPS, 리소스 게이지)

첫 화면은 **모니터링 대시보드**로, 파이프라인·큐 사이즈·TPS·CPU/메모리 게이지를 실시간으로 보여줍니다. 좌측 사이드바에서 데이터베이스·상세 설정·세션 설정·발송 금지 시간·로그·이중화 등 다른 화면으로 이동할 수 있습니다.

{% hint style="info" %}
pipeline 모드(엔진 단독)에서는 Web UI가 제공되지 않습니다. 결과는 로그(`log/agent.log`)와 DB(`ODYSSEY` 테이블의 `RESULT` 컬럼)로 확인합니다.
{% endhint %}

## 6. 테스트 발송 — SMS 1건

Odyssey 정상 기동 후, 다음 SQL을 실행하면 SMS 1건이 발송됩니다. 수신번호와 회신번호는 운영 환경에 맞게 변경하세요.

```sql
INSERT INTO ODYSSEY (
    MSG_TYPE, SCHEDULE_TIME, SUBMIT_TIME,
    MESSAGE, CALLBACK_NUM, RCPT_DATA
) VALUES (
    1,                              -- 1 = SMS
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
    '[테스트] Odyssey 첫 발송 성공!',
    '0212345678',                   -- 회신번호 (특수문자 제외)
    '01012345678'                   -- 수신번호 (특수문자 제외)
);
```

발송 결과는 다음 3가지 채널 중 편한 곳에서 확인할 수 있습니다.

{% stepper %}
{% step %}
## 결과 확인 1 — 로그

```bash
# 전체 로그 (모든 모드)
tail -f log/agent.log

# 발송(KT) 채널만 보기
tail -f log/send_kt.log

# 에러만 보기
tail -f log/error.log
```

발송 성공 시 `Send Success` / `Report Success` 등의 메시지가 출력됩니다.
{% endstep %}

{% step %}
## 결과 확인 2 — Web UI (multi 모드)

모니터링 대시보드 접속 시, 파이프라인 그래프·TPS에서 메시지가 처리되는 과정을 시각적으로 확인할 수 있습니다.
{% endstep %}

{% step %}
## 결과 확인 3 — DB

발송이 완료되면 `ODYSSEY` 테이블의 `STATUS`와 `RESULT` 컬럼이 업데이트됩니다.

```sql
SELECT MSG_ID, STATUS, RESULT, RESULT_DESC, DELIVER_TIME
FROM ODYSSEY
WHERE MSG_TYPE = 1
ORDER BY MSG_ID DESC
LIMIT 10;
```

| 컬럼            | 의미               |
| ------------- | ---------------- |
| STATUS        | 2 = 1차 전송 완료     |
| RESULT        | 전송 결과 코드 (성공: 0) |
| RESULT\_DESC  | 결과 상세 메시지        |
| DELIVER\_TIME | 발송 시각            |
{% endstep %}
{% endstepper %}

수신자 휴대폰에 메시지가 도착했다면 첫 실발송 성공입니다.

## 7. 자주 막히는 지점

### 7-1. DB 접속 실패

**증상**: `log/agent.log`에 `Communications link failure` 또는 `Access denied for user` 에러.

**점검**:

* `application-HA.yaml`의 `jdbc-url`/`username`/`password` 값 확인
* DB 서버에서 Odyssey 서버 IP의 outbound 접속 허용 여부
* MySQL 8.x인 경우 `useSSL=false&allowPublicKeyRetrieval=true` 파라미터 필요
* 패스워드 암호화 사용 시 `common.user.otp` 값과 암호문이 짝이 맞는지

### 7-2. 세션 인증 실패

**증상**: 기동은 되지만 발송 시 `Auth Fail` / `Login Fail` 로그 반복.

**점검**:

* KT 크로샷: `auth-file` 값과 `auth/` 폴더의 `.cert` 파일명이 **대소문자까지 정확히 일치**하는지
* KT RCS / CPaaS: `rcs-id`/`rcs-secret` 또는 `api-id`/`api-pw` 발급값 확인
* 패스워드 암호화 적용 시 `common.user.otp`와 암호문 짝 확인

### 7-3. 발송은 시작되는데 결과가 안 옴

**증상**: `STATUS=1` (전송 중) 상태로 멈춰 있음.

**점검**:

* 게이트웨이 outbound 방화벽
* `report-cycle` 값이 너무 길지 않은지 (기본 `5000ms`)
* KT RCS의 `webhook-port`를 사용한다면 inbound 방화벽 허용 확인

### 7-4. 광고성 메시지 야간 차단 미설정

**증상**: 21:00 \~ 익일 08:00 시간대에 광고성 메시지 발송 후 정보통신망법 위반 통지.

**점검**:

* Web UI "발송 금지 시간" 화면에서 야간 차단을 드래그로 설정
* 설정값은 `PAUSE_INFO` 테이블에 저장

### 7-5. `max-cnt`가 계약 한도를 초과

**증상**: 게이트웨이에서 차단되어 일정 시간 발송 실패.

**점검**:

* 모든 세션의 `max-cnt`를 **KT/CPaaS와 계약한 초당 발송 한도와 정확히 동일**하게 설정
* 처리량을 늘리려면 `max-cnt` 증가가 아닌 **세션 수 추가** 또는 **계약 한도 상향**

### 7-6. Web UI가 안 열림

**증상**: 브라우저로 `http://[ip]:[port]` 접속 시 연결 거부.

**점검**:

* 기동 모드가 `multi`인지 확인 (pipeline 모드는 Web UI 미제공)
* 서버 방화벽에서 `server.port`(기본 `7090`) inbound 허용
* `application-HA.yaml`의 `server.port` 값과 실제 접속 포트 일치 여부

## Part 2. 설정 항목 상세

> Part 1에서 첫 실행에 꼭 필요한 핵심 설정만 다뤘다면, 본 Part는 `application-HA.yaml`과 `config/ha.properties`의 모든 옵션 reference입니다.

## 8. 환경설정 파일 개요

Odyssey의 환경설정은 두 개의 파일로 구성됩니다.

| 파일                  | 위치                      | 용도                                            |
| ------------------- | ----------------------- | --------------------------------------------- |
| application-HA.yaml | Odyssey 설치 폴더 / config/ | DB, 사용 서비스, 세션, Pipeline, Poseidon 등 모든 운영 설정 |
| ha.properties       | Odyssey 설치 폴더 / config/ | HA 이중화 노드 정보, DB Lease, 로드밸런싱 (HA 프로파일 전용)    |

{% hint style="info" %}
설정 파일을 변경한 경우 Odyssey를 재구동해야 적용됩니다. 단, 일부 항목은 내장 Web UI를 통해 무중단 변경이 가능합니다.
{% endhint %}

## 9. 패스워드 암호화

DB 패스워드, KT 크로샷 `SP_PWD`, `RCS_SECRET`, CPaaS `API_PW` 등 민감 정보는 암호화된 값을 YAML에 입력합니다. 암호화에 사용되는 OTP 값은 `common.user.otp` 옵션으로 지정합니다.

```yaml
common:
  user:
    otp: MONO # 암복호화에 사용되는 KEY
```

**암호화된 값 예시:**

```
패스워드 > test
암호화 사용 > f8jtIQQvu9flw+Th0EXCKQ==
```

{% hint style="info" %}
암호화 도구는 별도 배포되며 OTP 값을 입력하여 평문 → 암호문을 생성합니다. 평문 사용도 가능하지만 운영 환경에서는 반드시 암호화된 값을 사용하시기 바랍니다.
{% endhint %}

## 10. DB 설정

`application-HA.yaml`의 `spring.datasource.hikari` 영역에서 데이터베이스 연결 정보와 운영 옵션을 설정합니다.

```yaml
spring:
  datasource:
    hikari:
      driver-class-name: com.mysql.cj.jdbc.Driver
      jdbc-url: jdbc:mysql://{{ip}}:{{port}}/{{database}}?useUnicode=true&characterEncoding=UTF-8&useSSL=false&allowPublicKeyRetrieval=true
      username: {{id}}
      password: {{pw}}
      limit: 24
      backup: FIXED
      charset: UTF-8|UTF-8
```

### 항목별 설명

| 항목                | 설명                   | 권장값                                 |
| ----------------- | -------------------- | ----------------------------------- |
| driver-class-name | JDBC 드라이버 클래스명       | com.mysql.cj.jdbc.Driver (MySQL 고정) |
| jdbc-url          | DB 접속 URL            | 운영 환경 IP/포트로 치환                     |
| username          | DB 접속 계정명            | 고객사 DB 계정                           |
| password          | DB 접속 패스워드           | 암호화 적용 권장                           |
| limit             | 메시지 발송 타임아웃 (단위: 시간) | 12 (일반 환경)                          |
| backup            | 로그 테이블 생성 방식 (대문자)   | FIXED (소규모) / MONTHLY (중·대량)        |
| charset           | 인코딩\|디코딩 설정          | UTF-8\|UTF-8                        |

### `limit` — 메시지 발송 타임아웃

현재 시각 기준 `limit` 시간 이전에 예약된 메시지는 발송하지 않고 타임아웃 실패 처리합니다.

* 예) `limit=12`, 현재 시각 14시 → 02시 이후 예약 메시지만 발송, 02시 이전 메시지는 실패 처리

### `backup` — 로그 테이블 분할 정책

로그 테이블(`rv-submit-log`)이 누적되면 단일 테이블이 비대해져 조회·백업이 어려워집니다. 발송량에 따라 분할 정책을 선택합니다.

| 값       | 의미          | 테이블명 예시                |
| ------- | ----------- | ---------------------- |
| FIXED   | 로그테이블 고정 사용 | ODYSSEY\_LOG           |
| YEAR    | 연도별 분할      | ODYSSEY\_LOG\_2026     |
| MONTHLY | 월별 분할       | ODYSSEY\_LOG\_202604   |
| DAILY   | 일별 분할       | ODYSSEY\_LOG\_20260427 |

### `charset` — DB 인코딩

DB 통신 시 인코딩과 디코딩에 사용할 charset을 `|`로 구분하여 입력합니다.

* 예) `UTF-8|UTF-8` → encoding / decoding 모두 UTF-8 사용

### 권장 설정 (발송 환경별)

| 발송 환경             | limit   | backup  | 비고                  |
| ----------------- | ------- | ------- | ------------------- |
| 실시간 알림 (OTP·인증번호) | 1 \~ 2  | FIXED   | 오래된 메시지의 뒤늦은 발송 방지  |
| 일반 안내성 메시지        | 12 (기본) | FIXED   | 월 100만 건 미만 환경      |
| 대량 예약 발송 (광고 캠페인) | 24 이상   | MONTHLY | 예약 윈도우가 넓고 누적 로그 많음 |
| 일 100만 건 이상 대량 발송 | 24 이상   | DAILY   | 일별 분할로 조회·백업 편의성 확보 |

{% hint style="warning" %}
**자주 하는 실수**

1. **`limit`을 너무 짧게 설정** — 대량 예약 발송 환경에서 `limit=1~2`로 설정하면 02시 이전 예약 메시지가 전부 실패 처리됩니다. 대량 예약 환경은 반드시 `24` 이상으로 확보하세요.
2. **`backup=DAILY` + 보관 정책 부재** — 일별 로그 테이블이 무한 누적됩니다. 별도 보관 주기(예: 90일 이후 삭제) 정책을 함께 마련하세요.
3. **패스워드 평문 입력** — 운영 환경에서는 반드시 OTP 기반 암호화 적용 후 암호문을 입력하세요.
{% endhint %}

## 11. 사용 서비스

`common.execute` 와 `common.transmission` 영역에서 사용할 메시지 종류와 발송 경로를 설정합니다.

```yaml
common:
  execute:
    sms: true
    lms: true
    mms: true
    rcs: true
    kakao: true
    fetch: true
  transmission:
    msg: KT
    rcs: KT
    kakao: CPAAS
```

### common.execute (사용 메시지 종류)

| 옵션    | 설명                                   |
| ----- | ------------------------------------ |
| sms   | SMS 발송 사용 여부. (true/false)           |
| lms   | LMS 발송 사용 여부. (true/false)           |
| mms   | MMS 발송 사용 여부. (true/false)           |
| rcs   | RCS 발송 사용 여부. (true/false)           |
| kakao | 카카오 알림톡/친구톡 발송 사용 여부. (true/false)   |
| fetch | 로그 테이블 백업(이관) 기능 사용 여부. (true/false) |

{% hint style="info" %}
사용하지 않는 메시지 종류는 `false`로 두면 불필요한 DB 폴링이 줄어 DB 부하가 낮아집니다. `fetch`(로그 이관)는 HA 운영 시 `true` 권장 — 메인 발송 테이블이 비대해지는 것을 막아줍니다.
{% endhint %}

### common.transmission (발송 경로 선택)

각 메시지 그룹별로 어떤 게이트웨이를 통해 발송할지 지정합니다.

**`msg`** — 문자(SMS/LMS/MMS) 발송 경로

| 값     | 의미                 |
| ----- | ------------------ |
| KT    | KT 크로샷(직접 연동)으로 발송 |
| CPAAS | CPaaS API를 통해 발송   |

**`rcs`** — RCS 발송 경로

| 값     | 의미                    |
| ----- | --------------------- |
| KT    | KT RCS Hermes API로 발송 |
| CPAAS | CPaaS API를 통해 발송      |

**`kakao`** — 카카오 알림톡/친구톡 발송 경로

| 값     | 의미               |
| ----- | ---------------- |
| MN    | 엠앤와이즈 API로 발송    |
| CPAAS | CPaaS API를 통해 발송 |

{% hint style="info" %}
계약된 발송 경로와 **반드시 일치**해야 합니다. 경로가 이중화된 경우(KT 기본, CPaaS 백업 등) 장애 시에만 수동 변경하며, 평상시에는 계약 주 경로를 유지합니다.
{% endhint %}

## 12. 테이블명 & 건수 & 주기 설정

`common.tables` 영역에서 Odyssey가 사용할 테이블명, 서비스별 초당 발송 건수, 폴링 주기를 설정합니다.

```yaml
common:
  tables:
    table-name:
      rv-submit: ODYSSEY
      rv-submit-log: ODYSSEY_LOG
      rv-stat: ODYSSEY_STAT
      rv-file: ODYSSEY_RCSFILE
      rv-tmpl-stat: ODYSSEY_TEMPLATE_STAT
    fetch-count:
      sms: 260
      lms: 300
      mms: 40
      rcs: 120
      kakao: 400
      fetch: 1000
    cycle:
      fetch: 1000
      db-check-interval: 30000
```

### 항목별 설명

| 그룹          | 옵션                | 설명                     | 권장값                     |
| ----------- | ----------------- | ---------------------- | ----------------------- |
| table-name  | rv-submit         | 발송 테이블 (고객사 INSERT 대상) | ODYSSEY                 |
| table-name  | rv-submit-log     | 발송 완료 메시지 이관 테이블       | ODYSSEY\_LOG            |
| table-name  | rv-stat           | 발송 통계 집계 테이블           | ODYSSEY\_STAT           |
| table-name  | rv-file           | RCS 이미지 파일 테이블         | ODYSSEY\_RCSFILE        |
| table-name  | rv-tmpl-stat      | 템플릿별 발송 통계 테이블         | ODYSSEY\_TEMPLATE\_STAT |
| fetch-count | sms \~ kakao      | 메시지 타입별 초당 발송 건수       | 아래 fetch-count 표 참고     |
| fetch-count | fetch             | 로그 이관 초당 처리 건수         | 1000                    |
| cycle       | fetch             | 메시지 폴링 주기 (ms)         | 1000                    |
| cycle       | db-check-interval | DB 연결 체크 주기 (ms)       | 30000                   |

### `table-name` — 자동 생성 테이블명

기본값을 그대로 사용하며, 고객사 DB에 같은 이름의 기존 테이블이 있는 경우에만 충돌 방지를 위해 변경합니다. 운영 중 변경 시 기존 발송 데이터와의 연결이 끊어지므로 신규 환경 설치 시점에만 조정하세요.

### `fetch-count` — 서비스별 초당 발송 건수

각 서비스가 1초당 DB에서 가져와 발송할 최대 메시지 건수입니다. **각 세션의 `max-cnt` 합과 같거나 약간 크게** 설정하는 것이 원칙입니다.

| 메시지 타입 | 권장 기본값 | 산출 근거                 |
| ------ | ------ | --------------------- |
| sms    | 260    | KT 크로샷 1세션 (200) + 여유 |
| lms    | 300    | KT 크로샷 1세션 (200\~300) |
| mms    | 40     | KT 크로샷 1세션 (30) + 여유  |
| rcs    | 120    | KT RCS 1세션 (30) × 4   |
| kakao  | 400    | CPaaS 1세션 (20) × 20   |
| fetch  | 1000   | 로그 이관 처리량             |

### `cycle` — 폴링 주기

| 옵션                | 설명                             | 권장값         |
| ----------------- | ------------------------------ | ----------- |
| fetch             | 메시지 폴링(DB SELECT) 주기 (단위: 밀리초) | 1000 (1초)   |
| db-check-interval | DB 연결 상태 체크 주기 (단위: 밀리초)       | 30000 (30초) |

### 권장 설정 (발송량별)

| 발송 환경                 | fetch-count 조정                | cycle.fetch |
| --------------------- | ----------------------------- | ----------- |
| 소량 (월 100만 건 미만)      | 기본값 유지                        | 1000 (기본)   |
| 중량 (일 평균 10만\~100만 건) | 세션 1\~2개 추가 + 합산 max-cnt와 동기화 | 1000 (기본)   |
| 대량 (일 100만 건 이상)      | 세션 다수 추가 + 비례 조정              | 500 \~ 1000 |

{% hint style="info" %}
처리량은 `fetch-count` 증가가 아니라 **세션 추가 + 합산 `max-cnt` 동기화**로 늘립니다. `fetch-count`만 키우면 차이만큼 DB 부하만 증가하고 게이트웨이가 차단합니다.
{% endhint %}

## 13. 기본 설정 (common.user)

`common.user` 영역에서 Odyssey 동작과 관련된 기본값들을 설정합니다.

```yaml
common:
  user:
    shutdownhooker: 25201
    file-size: 512000
    file-upload: 109
    ping-time: 20
    ping-delay: 50
    restart-delay: 5
    rcsfile-yn: false
    rcs-auto-upload: false
    auth-dir: ./auth
    file-dir: ./upload
    filelist-check-interval: 86400
    retry-report-interval: 60000
    otp: MONO
    kisa-orig-code: ''
    agencykey: {{agency_key}}
    brandid: {{brand_id}}
    brandkey: {{brand_key}}
    rcs-stat-info: true
```

### 일반 옵션

**`shutdownhooker`** : Odyssey 관리용 포트. 동일 서버에 Odyssey를 여러 개 실행하는 경우 인스턴스마다 다른 값을 사용해야 합니다.

**`file-size`** : 업로드 이미지 파일 최대 크기. (단위: byte)

**`file-upload`** : 업로드 세션 개수.

**`ping-time`** : 세션 상태 체크 주기. (단위: 초)

**`ping-delay`** : 세션 상태 체크 응답 대기 시간. (단위: 초)

**`restart-delay`** : 세션 재시작 지연 시간. (단위: 초)

**`rcsfile-yn`** : RCS 첨부파일 사용 여부. RCS MMS 발송 시 이미지 파일 처리 활성화 여부를 결정합니다. (기본값: `false`)

**`rcs-auto-upload`** : RCS 첨부파일 자동 업로드 사용 여부. `true`이면 Odyssey가 `file-dir` 경로의 이미지를 RCS 게이트웨이에 자동 업로드합니다. (기본값: `false`)

**`auth-dir`** : 세션 인증파일(.cert) 경로.

**`file-dir`** : RCS MMS 이미지 파일 저장 경로. 절대경로 사용 시 빈 문자열로 둡니다.

**`filelist-check-interval`** : 업로드된 첨부파일 정보 캐시 유지시간. (단위: 초)

**`retry-report-interval`** : 발송 결과 재요청 주기. (단위: 밀리초)

* 발송 상태가 "전송대기" 또는 "전송중"인 메시지에 대해 결과를 재조회하는 간격.

**`otp`** : 암복호화 KEY. DB 패스워드, 세션 패스워드 등 모든 암호화 항목에 동일하게 사용됩니다.

### 발송 금지 시간 (pause)

발송 금지 시간은 `application-HA.yaml`에 직접 설정하지 않습니다. Web UI의 "발송 금지 시간" 화면에서만 편집 가능하며, 설정값은 `PAUSE_INFO` 테이블에 저장됩니다.

{% hint style="warning" %}
**반드시 설정하세요.** 광고성 메시지는 **정보통신망법에 따라 야간(21:00 \~ 익일 08:00) 발송이 금지**되어 있습니다. 해당 시간대를 차단하지 않으면 과태료 대상이 될 수 있으므로, 광고성 메시지를 발송하는 환경이라면 반드시 야간 차단을 설정해야 합니다.
{% endhint %}

### 기타 옵션

| 옵션             | 설명                                   |
| -------------- | ------------------------------------ |
| kisa-orig-code | KISA 코드. 재판매 사업자만 발급받은 코드를 설정합니다.    |
| agencykey      | agencyId(대행사 ID)에 매핑되는 대행사 KEY 값.    |
| brandid        | chatbotId(챗봇 ID) 소유 brandId(브랜드 ID). |
| brandkey       | brandId에 매핑되는 브랜드 KEY 값.             |
| rcs-stat-info  | RCS 고객반응 통계 기능 사용 여부. (true/false)   |

## 14. 계정 설정 (sessions)

각 게이트웨이별 세션 정보는 `kt` / `rcs` / `cpaas` / `kakao` 영역의 `sessions` 리스트에 입력합니다. 실제 사용하는 세션만 등록하고, 사용하지 않는 영역은 주석 처리하거나 통째로 삭제합니다.

### 세션 매핑

`common.transmission` 설정에 따라 사용하는 세션 영역이 결정됩니다.

| common.transmission 값 | 사용 세션 영역       | 게이트웨이              |
| --------------------- | -------------- | ------------------ |
| msg: KT               | kt.sessions    | KT 크로샷 (문자 직접 연동)  |
| msg: CPAAS            | cpaas.sessions | KT CPaaS (문자 API)  |
| rcs: KT               | rcs.sessions   | KT RCS Hermes API  |
| rcs: CPAAS            | cpaas.sessions | KT CPaaS (RCS API) |
| kakao: MN             | kakao.sessions | 엠앤와이즈 직접 연동        |
| kakao: CPAAS          | cpaas.sessions | KT CPaaS (카카오 API) |

### kt.sessions (KT 크로샷 직접 연동 - 문자)

```yaml
kt:
  socket:
    runtime: netty # 소켓 런타임 (netty 권장)
  sessions:
    - seq: 1
      rcs-ip: rcs.xroshot.com
      sp-id: {{xroshot_id}}
      sp-pwd: {{xroshot_pw}}
      end-user: {{user}}
      auth-file: {{auth_file_name}}
      max-cnt: 200
      sms: true
      lms: true
      mms: true
```

| 옵션              | 설명                             | 권장값                                                                  |
| --------------- | ------------------------------ | -------------------------------------------------------------------- |
| seq             | 세션 일련번호 (다중 세션 시 1, 2, 3 …)    | 1                                                                    |
| rcs-ip          | 크로샷 센터 IP:PORT                 | 1센터: rcs.xroshot.com / 2센터: rcs2.xroshot.com / 차세대: info.xroshot.com |
| sp-id           | 크로샷 ServiceProvider 아이디        | 발급받은 값                                                               |
| sp-pwd          | 크로샷 패스워드                       | 암호화 적용 권장                                                            |
| end-user        | 크로샷 EndUser ID                 | 발급받은 값                                                               |
| auth-file       | 세션 인증파일 명 (.cert, **대소문자 구분**) | auth/ 폴더 파일명과 정확히 일치                                                 |
| max-cnt         | 초당 발송 건수                       | KT 계약 한도와 일치 (기본 200)                                                |
| sms / lms / mms | 해당 세션의 메시지 종류 사용 여부            | true / false                                                         |

### rcs.sessions (KT RCS Hermes API)

```yaml
rcs:
  sessions:
    - seq: 1
      send-url: https://agency.hermes.kt.com/corp/v1
      report-url: https://query.hermes.kt.com/corp/v1
      rcs-stat-url: https://api.rcsbizcenter.com/api/1.1
      rcs-stat-id: {{stat_id}}
      rcs-stat-secret: {{stat_secret}}
      rcs-id: {{rcs_id}}
      rcs-secret: {{rcs_pw}}
      webhook-port: ''
      agencyid: ktbizrcs
      expiry-option: 2
      report-cycle: 5000
      max-cnt: 30
```

| 옵션              | 설명                             | 권장값                                                                                     |
| --------------- | ------------------------------ | --------------------------------------------------------------------------------------- |
| seq             | 세션 일련번호                        | 1, 2, 3 …                                                                               |
| send-url        | 메시지 발송 API URL                 | 운영: https://agency.hermes.kt.com/corp/v1 / 개발: https://agency-stg.hermes.kt.com/corp/v1 |
| report-url      | 메시지 리포트 API URL                | 운영: https://query.hermes.kt.com/corp/v1 / 개발: https://query-stg.hermes.kt.com/corp/v1   |
| rcs-stat-url    | RCS 고객반응 통계 API URL            | rcs-stat-info=true 인 경우만 입력                                                             |
| rcs-stat-id     | RCS Biz Center 가입 ID           | rcs-stat-info=true 인 경우만 입력                                                             |
| rcs-stat-secret | RCS Biz Center API KEY (자동 생성) | rcs-stat-info=true 인 경우만 입력                                                             |
| rcs-id          | KT RCS 청약 ID                   | 발급받은 값                                                                                  |
| rcs-secret      | KT RCS SECRET 키                | 암호화 적용 권장                                                                               |
| webhook-port    | 리포트 수신 방식                      | 아래 webhook-port 설명 참고                                                                   |
| agencyid        | 대행사 ID                         | 운영: ktbizrcs / 개발: ktrcsdev                                                             |
| expiry-option   | 메시지 결과 처리 옵션                   | 2 (통신사 정책시간)                                                                            |
| report-cycle    | API 방식 리포트 조회 주기 (ms)          | 5000                                                                                    |
| max-cnt         | 초당 발송 건수                       | KT RCS 계약 한도와 일치 (기본 30)                                                                |

#### `webhook-port` — 리포트 수신 방식

| 값              | 방식      | 동작                                       |
| -------------- | ------- | ---------------------------------------- |
| 포트번호 (예: 8443) | WEBHOOK | KT가 해당 포트로 리포트를 push (inbound 방화벽 허용 필요) |
| 빈 문자열 ('')     | API     | Odyssey가 report-cycle 주기로 결과를 pull       |

#### `expiry-option` — 결과 WEBHOOK 유효 시간

| 값 | 의미                                        |
| - | ----------------------------------------- |
| 1 | 최대 3일까지 결과 WEBHOOK 전송                     |
| 2 | 통신사 정책 시간까지 결과 WEBHOOK 전송 (10초 \~ 3분, 권장) |

### cpaas.sessions (KT CPaaS API)

```yaml
cpaas:
  sessions:
    - seq: 1
      send-url: https://api.communis.kt.com/cpaas/v2.0
      report-url: https://api.communis.kt.com/cpaas/v2.0
      api-id: {{communis_id}}
      api-pw: {{communis_pw}}
      sender-key: {{kakao_senderkey}}
      alimtalk-param: false
      expiry-option: 2
      agency-id: ktbizrcs
      report-cycle: 5000
      max-cnt: 20
      worker-count: 5
```

| 옵션             | 설명                               | 권장값                                        |
| -------------- | -------------------------------- | ------------------------------------------ |
| seq            | 세션 일련번호                          | 1, 2, 3 …                                  |
| send-url       | CPaaS 발송 API URL                 | 운영: https://api.communis.kt.com/cpaas/v2.0 |
| report-url     | CPaaS 결과 조회 API URL              | 운영: https://api.communis.kt.com/cpaas/v2.0 |
| api-id         | CPaaS API 사용 ID                  | 발급받은 값                                     |
| api-pw         | CPaaS API 사용 패스워드                | 암호화 적용 권장                                  |
| sender-key     | 카카오 SENDER KEY                   | 발송 테이블 K\_SENDERKEY 비어 있는 경우 fallback      |
| alimtalk-param | 카카오 알림톡 치환 문자열만 입력하는 발송 방식 사용 여부 | 일반 발송 false                                |
| expiry-option  | 메시지 결과 처리 옵션 (RCS와 동일)           | 2 (통신사 정책 시간)                              |
| agency-id      | 대행사 ID                           | ktbizrcs                                   |
| report-cycle   | 리포트 조회 주기 (단위: 밀리초)              | 5000                                       |
| max-cnt        | 초당 발송 건수                         | CPaaS 계약 한도와 일치 (기본 20)                    |
| worker-count   | 세션당 병렬 worker 슬롯 수               | 1 (기본) \~ 5 (응답 지연 시)                      |

### kakao.sessions (엠앤와이즈 카카오 직접 연동)

`common.transmission.kakao = MN` 인 경우에 사용합니다. CPaaS 경유 카카오 발송을 사용한다면 본 영역은 비워두어도 됩니다.

```yaml
kakao:
  sessions:
    - seq: 1
      send-url: https://wt-api.carrym.com:8443/v3
      report-url: https://wt-api.carrym.com:8443/v3
      api-id: ''
      api-key: ''
      sender-key: ''
      report-cycle: '5000'
      max-cnt: 0
```

| 옵션           | 설명                  | 권장값                               |
| ------------ | ------------------- | --------------------------------- |
| seq          | 세션 일련번호             | 1                                 |
| send-url     | 엠앤와이즈 발송 API URL    | https://wt-api.carrym.com:8443/v3 |
| report-url   | 엠앤와이즈 결과 조회 API URL | https://wt-api.carrym.com:8443/v3 |
| api-id       | 엠앤와이즈 발급 API ID     | 발급받은 값                            |
| api-key      | 엠앤와이즈 발급 API KEY    | 발급받은 값                            |
| sender-key   | 카카오 SENDER KEY      | 발급받은 값                            |
| report-cycle | 리포트 조회 주기 (ms, 문자열) | '5000'                            |
| max-cnt      | 초당 발송 건수            | 엠앤와이즈 계약 한도와 일치                   |

### 권장 설정 (게이트웨이별)

| 메시지 종류          | 사용 게이트웨이       | 설정해야 할 세션 영역   | max-cnt 기본 |
| --------------- | -------------- | -------------- | ---------- |
| SMS / LMS / MMS | KT 크로샷 (직접 연동) | kt.sessions    | 200        |
| SMS / LMS / MMS | KT CPaaS       | cpaas.sessions | 20         |
| RCS             | KT RCS Hermes  | rcs.sessions   | 30         |
| RCS             | KT CPaaS       | cpaas.sessions | 20         |
| 카카오 알림톡/친구톡     | 엠앤와이즈          | kakao.sessions | (계약값)      |
| 카카오 알림톡/친구톡     | KT CPaaS       | cpaas.sessions | 20         |

{% hint style="warning" %}
**모든 세션의 `max-cnt`는 게이트웨이와 계약한 초당 발송 한도와 정확히 일치해야 합니다.** 처리량을 늘리려면 `max-cnt`를 키우는 것이 아니라 **세션을 추가**하거나 **계약 한도를 상향**합니다.
{% endhint %}

{% hint style="warning" %}
**자주 하는 실수**

1. **`max-cnt`를 계약 한도보다 크게 설정** — 게이트웨이가 초과분을 차단하여 일정 시간 발송이 실패합니다. 계약값과 정확히 동일하게 설정하세요.
2. **`auth-file` 대소문자 불일치** — Linux 환경에서 `auth-file: test391.cert`와 실제 파일 `Test391.cert`는 다른 파일로 인식됩니다.
3. **`webhook-port` 입력 시 inbound 방화벽 미허용** — KT RCS WEBHOOK 방식 사용 시 해당 포트로 inbound 패킷이 들어와야 합니다.
4. **사용하지 않는 세션 영역을 빈 값으로 둠** — 사용하지 않는 영역은 통째로 주석 처리하거나 삭제하세요.
{% endhint %}

## 15. HA 이중화 설정 (ha.properties)

HA 프로파일에서 사용하는 이중화 노드 정보, 게이트웨이 감시, DB 기반 분산 락(Lease), 로드밸런싱 비율을 정의합니다. 파일 위치는 Odyssey 설치 폴더의 `config/ha.properties` 입니다.

```properties
NODE_CNT=2
NODE_NUM=1
HA_MODE=AA # AA | AS | STANDALONE
HA_MASTER_SLAVE=MASTER # MASTER | SLAVE
HA_AUTO_SWITCH=N # Y | N (AS mode only)

# NETWORK
HA_PORT=12001
INT_PEER_NODE_CHECK=N
INT_PEER_NODE_IP=127.0.0.1
INT_PEER_NODE_HA_PORT=9999
EXT_PEER_NODE_CHECK=Y
EXT_PEER_NODE_IP={{ip}}
EXT_PEER_NODE_HA_PORT=12000

# GATEWAY CHECK
PING_CMD=ping 127.0.0.1 -n 1
PING_SUCCESS_KEY=TTL=
PING_INTERVAL=1000
PING_TIMEOUT=5000

# HA TIMING (ms)
NODE_CHECK_INTERVAL=1000
NODE_CHECK_TIMEOUT=3000
NODE_ACTIVATING_INTERVAL=3000

# SAFETY / STABILITY
FAILBACK_STABILIZATION_MS=30000
SPLIT_BRAIN_PROTECTION=N
PEER_FRESHNESS_MS=3000

# DB LEASE
DB_LEASE_ENABLED=Y
DB_LEASE_FAIL_CLOSED=Y
DB_URL=jdbc:mysql://{{ip}}:{{port}}/{{database}}?useUnicode=true&characterEncoding=UTF-8&useSSL=false&allowPublicKeyRetrieval=true
DB_USER={{id}}
DB_PASSWORD={{pw}}
DB_LEASE_NAME=ha_lease_master
DB_LEASE_TTL_MS=5000
DB_LEASE_RENEW_INTERVAL_MS=1000

# LOAD BALANCE RATIO
LOAD_BALANCE_PERCENT=60
ENFORCE_LOAD_BALANCE_RATIO=Y
```

### 항목별 설명

| 그룹       | 옵션                                         | 설명                          | 권장값                         |
| -------- | ------------------------------------------ | --------------------------- | --------------------------- |
| 노드 정보    | NODE\_CNT                                  | 이중화 참여 노드 수                 | 2                           |
| 노드 정보    | NODE\_NUM                                  | 본 노드 번호                     | 1 또는 2 (양 노드 다른 값)          |
| 노드 정보    | HA\_MODE                                   | 이중화 모드                      | AA (권장) / AS / STANDALONE   |
| 노드 정보    | HA\_MASTER\_SLAVE                          | 본 노드 역할                     | MASTER 또는 SLAVE             |
| 노드 정보    | HA\_AUTO\_SWITCH                           | AS 모드 자동 역할 전환              | N (수동, 권장)                  |
| 네트워크     | HA\_PORT                                   | 본 노드 HA 통신 포트               | 12001                       |
| 네트워크     | INT\_PEER\_NODE\_CHECK / \_IP / \_HA\_PORT | 내부 네트워크 Peer 감시             | 보통 N                        |
| 네트워크     | EXT\_PEER\_NODE\_CHECK / \_IP / \_HA\_PORT | 외부 네트워크 Peer 감시             | Y + 상대 노드 IP/포트             |
| PING     | PING\_CMD                                  | 게이트웨이 생존 확인 명령              | OS에 맞게 (한 번만 수정)            |
| PING     | PING\_SUCCESS\_KEY                         | PING 성공 인식 문자열              | TTL=                        |
| PING     | PING\_INTERVAL / PING\_TIMEOUT             | PING 주기 / 응답 대기 (ms)        | 1000 / 5000                 |
| 타이밍      | NODE\_CHECK\_INTERVAL / \_TIMEOUT          | Peer 상태 체크 주기 / 응답 대기 (ms)  | 1000 / 3000                 |
| 타이밍      | NODE\_ACTIVATING\_INTERVAL                 | Activating → Active 대기 (ms) | 3000                        |
| 안정성      | FAILBACK\_STABILIZATION\_MS                | Failback 안정 대기 (ms)         | 30000                       |
| 안정성      | SPLIT\_BRAIN\_PROTECTION                   | Split-Brain 보호 모드           | N (필요 시 Y)                  |
| 안정성      | PEER\_FRESHNESS\_MS                        | Peer 상태 유효 기간 (ms)          | 3000                        |
| DB Lease | DB\_LEASE\_ENABLED                         | DB Lease 사용                 | HA 운영 시 Y                   |
| DB Lease | DB\_LEASE\_FAIL\_CLOSED                    | DB 실패 시 본 노드 정지 여부          | Y (권장)                      |
| DB Lease | DB\_URL / DB\_USER / DB\_PASSWORD          | Lease DB 접속 정보              | 메인 DB와 동일                   |
| DB Lease | DB\_LEASE\_NAME                            | Lease 식별자                   | ha\_lease\_master (양 노드 동일) |
| DB Lease | DB\_LEASE\_TTL\_MS / \_RENEW\_INTERVAL\_MS | Lease 만료 / 갱신 주기 (ms)       | 5000 / 1000                 |
| 로드밸런싱    | LOAD\_BALANCE\_PERCENT                     | 본 노드 처리 비율 (%)              | 양 노드 합이 정확히 100             |
| 로드밸런싱    | ENFORCE\_LOAD\_BALANCE\_RATIO              | 로드밸런싱 비율 강제 여부              | Y (엄격)                      |

### 노드 정보 / HA 모드

`HA_MODE`는 이중화 운영 방식을 결정합니다.

| 모드                  | 동작                    | 처리량 | 권장 사용처        |
| ------------------- | --------------------- | --- | ------------- |
| AA (Active-Active)  | 두 노드가 동시에 발송 (로드밸런싱)  | 2배  | 일반 운영 환경 (권장) |
| AS (Active-Standby) | Master만 발송, Slave는 대기 | 1배  | 단순 동작이 필요한 환경 |
| STANDALONE          | 단일 노드, 이중화 미사용        | 1배  | 개발 / 테스트      |

`HA_AUTO_SWITCH`는 AS 모드에서 SLAVE가 활성된 동안 MASTER가 복구되면 자동으로 역할을 되돌릴지 여부입니다. **`N` (수동 전환) 유지를 권장**합니다 — 자동 전환 시 역할이 왔다갔다하는 플리커링이 발생할 수 있습니다.

### 네트워크 / Peer 감시

양 노드의 IP와 HA 포트를 교차 등록합니다. 동일 호스트에서 다중 인스턴스 테스트가 필요할 때만 `INT_PEER_NODE_CHECK=Y`를 사용합니다.

### Gateway PING 체크

게이트웨이 생존을 주기적으로 확인하여 네트워크 단절 시 자동으로 Failover를 트리거합니다.

| OS      | PING\_CMD                |
| ------- | ------------------------ |
| Linux   | ping -c 1 -W 1 \[target] |
| Windows | ping \[target] -n 1      |

{% hint style="info" %}
`[target]`은 게이트웨이 IP 또는 기본 게이트웨이(라우터) IP를 입력합니다. 설치 시 OS 유형에 맞춰 **한 번만** 수정하면 운영 중 바꿀 일이 없습니다.
{% endhint %}

### HA 타이밍 / 안정성 / Split-Brain 방지

Peer 노드 감시 주기, Failback 안정화 대기, Split-Brain 보호 동작 등을 제어합니다. **기본값 유지를 강력히 권장**합니다 — 임의 변경 시 장애 감지 속도와 스플릿-브레인 방지 안정성 사이의 균형이 깨집니다.

### DB Lease (DB 기반 분산 락)

Odyssey HA는 두 노드의 활성/정지를 DB 테이블(`ha_lease`)에 기록되는 임차권(Lease) 기반으로 관리합니다. `ha_lease` 테이블은 최초 기동 시 자동 생성됩니다.

* **`DB_LEASE_NAME`**: 동일 클러스터의 두 노드는 **같은 값**을 사용해야 같은 Lease를 두고 경쟁합니다.
* **`DB_LEASE_TTL_MS` / `RENEW_INTERVAL_MS`**: 갱신 주기는 TTL의 1/3 \~ 1/5 사이를 권장합니다 (기본 `5000` / `1000`).
* **`DB_LEASE_FAIL_CLOSED=Y`** (권장): DB 연결이 끊기면 본 노드가 즉시 정지해 split-brain 위험을 차단합니다.

### 로드밸런싱 (AA 모드 전용)

`LOAD_BALANCE_PERCENT`는 본 노드가 처리할 메시지 비율(%)이며, **양 노드의 합이 정확히 100**이 되어야 합니다. 합이 어긋나면 중복 발송 또는 누락이 발생할 수 있습니다.

| 노드 사양                   | 1번 노드    | 2번 노드    |
| ----------------------- | -------- | -------- |
| 동등 사양                   | 50       | 50       |
| 1번이 더 좋음 (CPU/메모리/네트워크) | 60 \~ 70 | 40 \~ 30 |
| 2번이 더 좋음                | 30 \~ 40 | 70 \~ 60 |

`ENFORCE_LOAD_BALANCE_RATIO=Y` (엄격) 설정 시 비율을 어기는 메시지 fetch를 차단합니다. `N`은 권고치로만 사용합니다.

### 권장 설정 (HA 모드별)

| HA 모드               | HA\_AUTO\_SWITCH | LOAD\_BALANCE\_PERCENT | DB\_LEASE\_FAIL\_CLOSED |
| ------------------- | ---------------- | ---------------------- | ----------------------- |
| AA (일반 운영)          | —                | 양 노드 합 100 (기본 50:50)  | Y                       |
| AS (단순 운영)          | N (수동)           | — (사용 안함)              | Y                       |
| STANDALONE (개발/테스트) | —                | —                      | N (선택)                  |

{% hint style="warning" %}
**자주 하는 실수**

1. **양 노드에 같은 `NODE_NUM` 입력** — 1번 노드는 `NODE_NUM=1`, 2번 노드는 `NODE_NUM=2`로 정확히 다르게 설정하세요.
2. **`LOAD_BALANCE_PERCENT` 합이 100이 아님** — 합이 100을 초과하면 중복 발송, 미만이면 일부 메시지가 영원히 처리되지 않습니다.
3. **`DB_LEASE_NAME`을 노드별로 다르게 설정** — 동일 클러스터는 같은 `DB_LEASE_NAME`을 사용하세요.
4. **`DB_LEASE_TTL_MS` / `_RENEW_INTERVAL_MS` 임의 조정** — 기본값 유지 권장.
5. **운영 중 `HA_MODE` 변경** — HA 모드 변경 시 양 노드를 정지 후 동시 재기동하세요.
{% endhint %}

## 16. Poseidon 모니터링 연동

**Poseidon**은 ㈜모노커뮤니케이션즈가 운영하는 통합 모니터링 플랫폼입니다. Odyssey HA 프로파일은 Poseidon 클라우드와 연동하여 인스턴스 상태, 시작/종료 알림, 하트비트, 에러 보고 등을 주기적으로 전송합니다. 운영 에러는 `libs/` 의 모니터링 네이티브 라이브러리를 통해 보고됩니다.

```yaml
poseidon:
  url: http://{{MONO_IP}}:{{MONO_PORT}}/api/v1/odyssey-instances
  auth-key: {{발급받은 Auth 키}}
  contact-email: {{email}}
  heartbeat:
    interval-ms: 30000
```

| 옵션                             | 설명                                      |
| ------------------------------ | --------------------------------------- |
| poseidon.url                   | Poseidon API 엔드포인트 URL. 운영 환경 별로 별도 발급. |
| poseidon.auth-key              | Poseidon 인증 키. 인스턴스별 발급된 값을 입력.         |
| poseidon.contact-email         | 장애 발생 시 연락받을 담당자 이메일. (고객사)             |
| poseidon.heartbeat.interval-ms | 하트비트 전송 주기. 기본 30,000 (30초).            |

{% hint style="info" %}
Poseidon 연동을 사용하지 않는 경우 본 영역을 통째로 주석 처리하거나 `url`, `auth-key`를 빈 값으로 두면 됩니다.
{% endhint %}

```
INFO Poseidon integration disabled (poseidon.url not configured) — skipping start notification, heartbeat, error reporting
```

미연동 상태에서는 Poseidon 으로의 외부 호출이 일절 발생하지 않습니다.

{% hint style="info" %}
Poseidon 연동을 사용하는 경우 **고객사 방화벽에 Poseidon 서버 IP를 등록**해 주셔야 합니다. Odyssey가 주기적으로 외부의 Poseidon 클라우드(`poseidon.url` 항목에 명시된 호스트)로 HTTPS 요청(하트비트, 알림)을 송신해야 하므로 outbound 통신이 차단되어 있는 경우 연동이 동작하지 않습니다. 정확한 IP 및 포트 정보는 별도 안내드립니다.
{% endhint %}

## Part 3. 발송 쿼리 모음

> 메시지 타입별 INSERT 쿼리, MSG\_TYPE / STATUS 코드, 테이블 컬럼 레이아웃을 reference로 정리합니다.

## 17. 메시지 타입별 INSERT

고객사 시스템에서 Odyssey 발송 테이블(기본 `ODYSSEY`)에 INSERT 함으로써 메시지가 발송됩니다.

### SMS 발송 (msg\_type=1)

```sql
INSERT INTO ODYSSEY (
msg_type, submit_time, schedule_time, message, callback_num, rcpt_data
) VALUES (
1,
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'SMS 테스트 발송입니다.',
'발신번호',
'수신번호'
);
```

### LMS 발송 (msg\_type=2)

```sql
INSERT INTO ODYSSEY (
msg_type, submit_time, schedule_time, subject, message, callback_num, rcpt_data
) VALUES (
2,
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'LMS 발송',
'LMS 테스트 발송입니다.',
'발신번호',
'수신번호'
);
```

### MMS 발송 (msg\_type=3)

```sql
INSERT INTO ODYSSEY (
msg_type, submit_time, schedule_time, subject, message,
callback_num, rcpt_data, file_count, file_name1
) VALUES (
3,
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'MMS 발송',
'MMS 테스트 발송입니다.',
'발신번호',
'수신번호',
1,
'test.jpg' -- 첨부파일명 (file-dir 폴더에 사전 저장)
);
```

### 카카오 알림톡 발송 (msg\_type=6)

```sql
INSERT INTO ODYSSEY (
msg_type, submit_time, schedule_time, subject,
callback_num, rcpt_data, k_tmplcode, k_message, k_option
) VALUES (
6,
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'카카오 알림톡 테스트',
'발신번호',
'수신번호',
'템플릿코드',
'알림톡 메시지 내용',
'버튼(JSON) 내용'
);
```

### 카카오 알림톡 강조표기 / 아이템 하이라이트 작성

`K_OPTION` 컬럼에 JSON 형식으로 입력합니다.

```json
// 강조 표기
{"attachment":{"title":"강조 표기"}}

// 강조 표기 + 버튼
{"attachment":{"button":[{"name":"버튼
이름","type":"AC"}],"title":"강조 표기"}}

// 아이템 하이라이트
{"attachment":{"button":[{"name":"채널
추가","type":"AC"}],
"itemHighlight":{"title":"메시지 전송","description":"아이템리스트형
테스트"},
"item":{"list":[{"title":"등록일시","description":"20240801"},
{"title":"전송결과","description":"#{변수1}"}]}}}
```

### 카카오 알림톡 - alimtalk-param=true 모드

CPaaS 세션에서 `alimtalk-param=true` 로 설정한 경우, `K_MESSAGE` 컬럼에 치환 변수만 JSON으로 입력합니다.

```sql
-- 템플릿 본문 (사전 등록)
-- #{이름}님, 저희 제품을 구매해주셔서 감사합니다.
-- 문의: #{개별1}

INSERT INTO ODYSSEY (
subject, msg_type, schedule_time, submit_time,
callback_num, rcpt_data, k_message, k_tmplcode, k_adflag
) VALUES (
'카카오 테스트',
6,
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'발신번호',
'수신번호',
'{"이름":"홍길동","개별1":"연구소"}',
'템플릿코드',
'N'
);
```

{% hint style="info" %}
템플릿 본문에 치환 문자가 없으면 `K_MESSAGE` 에 NULL 또는 빈 문자열을 입력합니다.
{% endhint %}

### RCS SMS 발송 (msg\_type=9)

```sql
INSERT INTO ODYSSEY (
msg_type, subject, submit_time, schedule_time,
callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
r_copyallowed, r_agencyid
) VALUES (
9,
'RCS SMS 발송',
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'발신번호',
'수신번호',
'SS000000',
'"body":{"description":"RCS 단문 테스트"}',
'버튼 JSON 내용',
'N',
'AGENCYID'
);
```

### RCS LMS 발송 (msg\_type=10)

```sql
INSERT INTO ODYSSEY (
msg_type, subject, submit_time, schedule_time,
callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
r_copyallowed, r_agencyid
) VALUES (
10,
'RCS LMS 발송',
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'발신번호',
'수신번호',
'SL000000',
'"body":{"description":"RCS 장문 테스트"}',
'버튼 JSON 내용',
'N',
'AGENCYID'
);
```

### RCS MMS 발송 (msg\_type=11) - File ID 자동 치환

`upload` 폴더에 이미지를 저장하고 `FILE_NAMEn` 컬럼에 파일명을 지정하면 Odyssey가 자동으로 업로드 후 `R_BODY` 의 `REPLACE_FILE_NAMEn` 문자열을 실제 File ID로 치환합니다.

```sql
INSERT INTO ODYSSEY (
msg_type, subject, submit_time, schedule_time,
callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
r_copyallowed, file_count, file_name1, r_agencyid
) VALUES (
11,
'RCS MMS 발송',
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'발신번호',
'수신번호',
'SMwThM00',
'"body":{"title":"RCS MMS 테스트","description":"RCS MMS
테스트","media":"maapfile://REPLACE_FILE_NAME1"}',
'버튼 JSON 내용',
'N',
1,
'test.jpg',
'AGENCYID'
);
```

{% hint style="info" %}
파일이 2개, 3개인 경우 `REPLACE_FILE_NAME1` / `REPLACE_FILE_NAME2` / `REPLACE_FILE_NAME3` 을 각각 사용하며, `FILE_NAME1~3` 컬럼에 대응되는 파일명을 저장합니다. 이미지는 발송 실패 시 MMS 대체발송을 고려하여 최대 3개까지 지원합니다.
{% endhint %}

### KT RCS TMPL 발송 (msg\_type=12)

```sql
INSERT INTO ODYSSEY (
msg_type, subject, submit_time, schedule_time,
callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
r_copyallowed, r_agencyid
) VALUES (
12,
'RCS TMPL 발송',
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'발신번호',
'수신번호',
'템플릿ID',
'"body":{"title":"RCS TMPL 테스트","description":"템플릿 변수에 해당하는 값을
포함하여 구성"}',
'버튼 JSON 내용',
'N',
'AGENCYID'
);
```

### KT RCS ITMPL 발송 (msg\_type=13)

```sql
INSERT INTO ODYSSEY (
msg_type, subject, submit_time, schedule_time,
callback_num, rcpt_data, r_messagebaseid, r_body, r_button,
r_copyallowed, r_agencyid
) VALUES (
13,
'RCS ITMPL 발송',
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'발신번호',
'수신번호',
'템플릿ID',
'"body":{"title":"RCS ITMPL 테스트","description":"템플릿 변수에 해당하는
값을 포함하여 구성"}',
'버튼 JSON 내용',
'Y',
'AGENCYID'
);
```

### CPAAS RCS 템플릿 (치환 문자 사용)

CPaaS RCS 템플릿 발송 시 치환 변수만 `R_BODY` 에 JSON 으로 입력합니다.

```sql
-- 템플릿 본문 (사전 등록)
-- 안녕하세요. {{이름}}님, 회원가입이 정상적으로 완료되었습니다.

INSERT INTO ODYSSEY (
subject, msg_type, schedule_time, submit_time,
callback_num, rcpt_data, r_body, r_messagebaseid
) VALUES (
'RCS 테스트',
12,
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'발신번호',
'수신번호',
'{"이름":"홍길동"}',
'템플릿코드'
);
```

{% hint style="info" %}
치환 문자가 없는 경우 `R_BODY` 컬럼에 NULL 또는 빈 문자열을 입력합니다. 텍스트/이미지 템플릿 사용 방식은 동일합니다.
{% endhint %}

### FALLBACK 발송 (1차 실패 시 2차/3차 순차 발송)

1차 발송이 실패한 경우 2차, 3차 발송을 자동으로 시도합니다. `msg_type` / `msg_type_second` / `msg_type_third` 가 발송 순서이며, 각 메시지에 필요한 모든 컬럼을 함께 입력하고 `FAIL_SEND` 를 `'Y'`로 설정해야 합니다.

```sql
-- 예) 1차 카카오 알림톡 -> 실패 시 2차 LMS
INSERT INTO ODYSSEY (
msg_type, msg_type_second, subject,
submit_time, schedule_time, message,
callback_num, rcpt_data, fail_send,
k_tmplcode, k_message, k_option
) VALUES (
6,
2,
'제목',
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
DATE_FORMAT(NOW(), '%Y%m%d%H%i%s'),
'LMS 메시지 내용',
'발신번호',
'수신번호',
'Y',
'템플릿코드',
'알림톡 메시지 내용',
'버튼(JSON) 내용'
);
```

## 18. MSG\_TYPE / STATUS 코드

### MSG\_TYPE 코드

| 코드 | 구분        | 설명            |
| -- | --------- | ------------- |
| 1  | SMS       | 단문 문자         |
| 2  | LMS       | 장문 문자         |
| 3  | MMS       | 멀티미디어 문자      |
| 6  | A\_KAKAO  | 카카오 알림톡       |
| 7  | F\_KAKAO  | 카카오 친구톡       |
| 8  | AI\_KAKAO | 카카오 알림톡 (이미지) |
| 9  | RCSSMS    | RCS 단문        |
| 10 | RCSLMS    | RCS 장문        |
| 11 | RCSMMS    | RCS 멀티미디어     |
| 12 | RCSTMPL   | RCS 텍스트 템플릿   |
| 13 | RCSITMPL  | RCS 이미지 템플릿   |

### STATUS 코드

| 코드 | 의미                  |
| -- | ------------------- |
| 0  | 1차 전송 대기            |
| 1  | 1차 전송 중             |
| 2  | 1차 전송 완료            |
| 3  | 2차 전송 대기 (FALLBACK) |
| 4  | 2차 전송 중             |
| 5  | 2차 전송 완료            |
| 6  | 3차 전송 대기 (FALLBACK) |
| 7  | 3차 전송 중             |
| 8  | 3차 전송 완료            |
| 9  | 로그테이블 이관 실패         |

## 19. 테이블 레이아웃 (MySQL)

Odyssey 최초 기동 시 `common.tables.table-name` 에 지정된 이름으로 테이블이 자동 생성됩니다. 아래는 발송 테이블(`rv-submit`, 기본 `ODYSSEY`)의 컬럼 레이아웃입니다.

| 컬럼명                | 데이터 타입                     | NN                             | 기본값                          | 설명                   |
| ------------------ | -------------------------- | ------------------------------ | ---------------------------- | -------------------- |
| MSG\_ID            | BIGINT(20) AUTO\_INCREMENT | Y                              | 메시지당 유니크한 번호 (PK)            |                      |
| LB\_ID             | BIGINT(20)                 | Y                              | 0                            | 로드밸런싱 ID (HA 분산 처리용) |
| SUBJECT            | VARCHAR(40)                | 메시지 제목                         |                              |                      |
| MSG\_TYPE          | TINYINT(2)                 | Y                              | 1차 메시지 구분 (아래 코드 표 참고)       |                      |
| MSG\_TYPE\_SECOND  | TINYINT(2)                 | Y                              | 0                            | 2차 메시지 구분 (FALLBACK) |
| MSG\_TYPE\_THIRD   | TINYINT(2)                 | Y                              | 0                            | 3차 메시지 구분 (FALLBACK) |
| STATUS             | SMALLINT                   | 0                              | 메시지 상태 (아래 표 참고)             |                      |
| SCHEDULE\_TIME     | VARCHAR(16)                | Y                              | 발송 시작 시각 (YYYYMMDDHH24MISS)  |                      |
| SUBMIT\_TIME       | VARCHAR(16)                | Y                              | 메시지 등록 시각 (YYYYMMDDHH24MISS) |                      |
| MESSAGE            | TEXT                       | 메시지 내용                         |                              |                      |
| CALLBACK\_NUM      | VARCHAR(20)                | Y                              | 회신번호 (특수문자 제외)               |                      |
| RCPT\_DATA         | VARCHAR(20)                | Y                              | 수신번호 (특수문자 제외)               |                      |
| FILE\_COUNT        | TINYINT(1)                 | 0                              | MMS 첨부 파일 개수                 |                      |
| FILE\_NAME1        | VARCHAR(128)               | MMS 첨부 파일 1                    |                              |                      |
| FILE\_NAME2        | VARCHAR(128)               | MMS 첨부 파일 2                    |                              |                      |
| FILE\_NAME3        | VARCHAR(128)               | MMS 첨부 파일 3                    |                              |                      |
| HEADER             | TINYINT(1)                 | CPAAS HEADER (광고 표기)           |                              |                      |
| FOOTER             | VARCHAR(20)                | CPAAS FOOTER (수신거부 번호)         |                              |                      |
| CDR\_ID            | VARCHAR(20)                | 과금 ID                          |                              |                      |
| RESULT             | MEDIUMINT(6)               | 전송 결과 코드 (SMS/LMS/MMS)         |                              |                      |
| RCS\_RESULT        | MEDIUMINT(6)               | 전송 결과 코드 (RCS)                 |                              |                      |
| KKO\_RESULT        | MEDIUMINT(6)               | 전송 결과 코드 (KAKAO)               |                              |                      |
| RESULT\_DESC       | VARCHAR(200)               | 결과코드 상세 내용                     |                              |                      |
| DELIVER\_TIME      | VARCHAR(16)                | 전송 시각 (마지막 발송)                 |                              |                      |
| REPORT\_RECV\_TIME | VARCHAR(16)                | 리포트 수신 시각                      |                              |                      |
| TELCOINFO          | VARCHAR(4)                 | 수신자 이통사 정보                     |                              |                      |
| FAIL\_SEND         | VARCHAR(1)                 | 'N'                            | 실패 재발송(FALLBACK) 여부 (Y/N)    |                      |
| K\_TMPLCODE        | VARCHAR(30)                | 알림톡 템플릿 코드                     |                              |                      |
| K\_MESSAGE         | TEXT                       | 알림톡 메시지 내용                     |                              |                      |
| K\_OPTION          | TEXT                       | 알림톡 button(JSON)               |                              |                      |
| K\_SERIAL\_NM      | VARCHAR(40)                | 알림톡 시리얼명                       |                              |                      |
| K\_ADFLAG          | VARCHAR(1)                 | 'N'                            | 알림톡 광고 문구 여부 (Y/N)           |                      |
| K\_SENDERKEY       | VARCHAR(40)                | 알림톡 발신 프로필 키                   |                              |                      |
| R\_MESSAGEBASEID   | VARCHAR(40)                | RCS messageBaseId              |                              |                      |
| R\_BODY            | TEXT                       | RCS body (JSON)                |                              |                      |
| R\_BUTTON          | TEXT                       | RCS button (JSON)              |                              |                      |
| R\_HEADER          | TINYINT(1)                 | RCS 광고 문구 여부 (0/1)             |                              |                      |
| R\_FOOTER          | VARCHAR(20)                | RCS 수신거부 번호 (R\_HEADER=1 시 필수) |                              |                      |
| R\_COPYALLOWED     | VARCHAR(1)                 | 'N'                            | RCS 메시지 복사 허용 여부 (Y/N)       |                      |
| R\_QUERYID         | VARCHAR(60)                | RCS 리포트 요청 queryId             |                              |                      |
| RESERVED01         | VARCHAR(60)                | 예약 필드 1                        |                              |                      |
| RESERVED02         | VARCHAR(60)                | 예약 필드 2                        |                              |                      |
| RESERVED03         | VARCHAR(60)                | 예약 필드 3                        |                              |                      |
| KISA\_ORIG\_CODE   | VARCHAR(9)                 | KISA 코드                        |                              |                      |
| R\_AGENCYID        | VARCHAR(60)                | RCS agencyId                   |                              |                      |
| R\_AGENCYKEY       | VARCHAR(256)               | RCS agencyKey                  |                              |                      |
| R\_BRANDKEY        | VARCHAR(256)               | RCS brandKey                   |                              |                      |
| R\_CDR\_ID         | VARCHAR(20)                | RCS 과금 ID                      |                              |                      |
| TRACKING\_ID       | VARCHAR(40)                | 리포트 요청 TRACKING ID             |                              |                      |
| TOKEN              | VARCHAR(100)               | 리포트 요청 TOKEN                   |                              |                      |
| C\_STATUS          | VARCHAR(1)                 | CPaaS 전송 결과 STATUS             |                              |                      |
| SUB\_KEY           | VARCHAR(100)               | CPAAS 부서/과금 분리 코드              |                              |                      |

### rv-file (M2X\_RCSFILE) 테이블

| 컬럼명          | 데이터 타입                     | NN                     | 기본값                 | 설명 |
| ------------ | -------------------------- | ---------------------- | ------------------- | -- |
| ID           | BIGINT(20) AUTO\_INCREMENT | Y                      | 첨부파일 유니크 번호 (PK)    |    |
| FILE\_PATH   | VARCHAR(200)               | Y                      | 발송테이블에 사용된 파일 경로    |    |
| DESCRIPTION  | VARCHAR(500)               | 파일 최종 수정 정보 (동명 파일 대비) |                     |    |
| STATUS       | SMALLINT                   | 0                      | 0=대기, 2=치환 가능, 3=실패 |    |
| FILEID       | VARCHAR(64)                | 자동 업로드된 파일 ID          |                     |    |
| SUBMIT\_TIME | VARCHAR(16)                | Y                      | 등록 시각               |    |
| UPLOAD\_TIME | VARCHAR(16)                | 업로드 시각                 |                     |    |
| EXPIRY\_TIME | VARCHAR(16)                | 만료 시각                  |                     |    |
| RESULT       | INT(6)                     | -2                     | 업로드 결과값             |    |
| RESULT\_DESC | VARCHAR(1000)              | 결과값 상세                 |                     |    |
| RCS\_ID      | VARCHAR(20)                | 발송 세션 RCS\_ID          |                     |    |

## Part 4. 운영 가이드

> Web UI, 게이트웨이 네트워크 정보, 로그 분석, 부가 설명 등 운영 중 참고하는 자료를 모았습니다.

## 20. Web UI 상세

Odyssey는 브라우저 기반의 웹 설정 UI를 제공합니다. YAML 파일을 직접 편집하지 않고도 주요 설정을 변경하고, 실시간 모니터링 및 로그 관리를 수행할 수 있습니다.

### 접속 방법

Odyssey가 구동된 상태에서 브라우저로 다음 주소에 접속합니다.

```
http://[서버IP]:[포트]
```

{% hint style="info" %}
권장 브라우저: Chrome, Edge (최신 버전). IE는 지원하지 않습니다.
{% endhint %}

### 화면 구조

웹 UI는 **헤더**, **사이드바**, **콘텐츠 영역** 3개 부분으로 구성됩니다.

* **헤더**: 상단 고정. 애플리케이션 타이틀("Odyssey 설정")과 버전 정보를 표시합니다.
* **사이드바**: 좌측 메뉴. 각 설정 화면으로 이동하며, 하단에 "설정 적용" 버튼이 있습니다.
* **콘텐츠 영역**: 선택한 메뉴에 해당하는 설정 화면이 표시됩니다.

| 메뉴       | 설정 화면                          | 대응 YAML 설정      |
| -------- | ------------------------------ | --------------- |
| 모니터링     | 실시간 발송 현황 + 발송 통계 (일/주/월)      | — (조회 전용)       |
| 데이터베이스   | DB 연결 정보 및 옵션                  | DB 설정           |
| 상세 설정    | 서비스 토글, 발송 파라미터                | 사용 서비스 \~ 기본 설정 |
| 세션 설정    | 통신사별 계정 관리                     | 계정 설정           |
| 발송 금지 시간 | 시간대별 발송 차단                     | 기본 설정           |
| 로그 저장    | 로그 파일 조회 및 다운로드                | 로그 / 에러 분석      |
| 이중화 설정   | HA 운영 모드 선택 + ha.properties 편집 | HA 이중화 설정       |

### 모니터링

Odyssey의 실시간 발송 상태와 발송 통계를 시각적으로 확인하는 대시보드입니다.

#### 실시간 발송 현황

* **파이프라인 시각화**: DB 조회 → 전송 대기 → 발송 처리 흐름을 단계별로 표시합니다.
* **큐 사이즈**: 전송 유형(SMS/LMS/MMS/RCS/카카오)별 대기 건수를 표시합니다.
* **TPS**: 초당 처리 건수(Transactions Per Second)를 실시간으로 표시합니다.
* **CPU / 메모리 사용률**: 원형 게이지로 서버 리소스 사용 현황을 표시합니다.

!\[모니터링 화면 — 실시간 발송 현황]\(./images/01. 모니터링 화면.png)

그림 10. 모니터링 화면 — 실시간 발송 현황 (파이프라인, 큐 사이즈, TPS, 리소스 게이지)

#### 발송 통계

일/주/월 단위로 집계된 발송 통계를 차트로 확인하고, 결과를 CSV·Excel로 내려받을 수 있습니다.

* **메시지 타입별 통계**: SMS / LMS / MMS / RCS / Kakao 등 메시지 종류별 발송 건수
* **시간대별 발송 추이**: 00시 \~ 23시 시간대별 발송 추이 차트 (일/주/월 단위 선택)
* **템플릿별 발송 추이**: RCS·Kakao 알림톡 템플릿 코드별 발송 건수 (템플릿 코드 검색 지원)

!\[모니터링 화면 — 발송 통계]\(./images/01-1. 모니터링 화면 - 통계.png)

그림 11. 모니터링 화면 — 발송 통계 (메시지 타입별 / 시간대별 / 템플릿별, CSV·Excel 내보내기)

{% hint style="info" %}
실시간 발송 현황은 WebSocket을 통해 실시간 갱신되며, 발송 통계는 약 14초 주기로 자동 갱신됩니다. 모니터링 화면 자체에서 설정을 변경하는 기능은 없습니다.
{% endhint %}

### 데이터베이스 설정

DB 연결 정보를 확인하고 옵션을 변경할 수 있습니다. YAML의 `spring.datasource.hikari` 항목에 해당합니다.

* **DB 타입**: MariaDB, MySQL, MSSQL, Oracle, PostgreSQL 중 선택
* **JDBC URL / 사용자명**: 보안상 읽기 전용으로 표시됩니다 (YAML에서 직접 수정)
* **옵션**: Limit(발송 제한 시간), Backup mode, Charset
* **테이블 설정**: 테이블명 및 관련 옵션

!\[데이터베이스 설정]\(./images/02. 데이터베이스 화면.png)

그림 12. 데이터베이스 설정 — 연결 정보 (DB 타입, JDBC URL, 사용자명)

{% hint style="info" %}
JDBC URL과 사용자명/비밀번호는 보안 정책에 따라 Web UI에서 수정할 수 없습니다. 변경이 필요한 경우 YAML 파일을 직접 편집하십시오.
{% endhint %}

### 상세 설정

서비스 사용 여부, 발송 경로, 각종 운영 파라미터를 설정합니다. YAML의 `common.execute`, `common.transmission`, `common.user` 항목에 해당합니다.

**서비스 토글 영역**

* SMS / LMS / MMS 사용 여부 (ON/OFF 토글)
* 발송 경로 선택 (KT 크로샷 / CPaaS)
* RCS / 카카오 발송 사용 여부
* Fetch 사용 여부

!\[상세 설정 - 서비스 토글]\(./images/03. 상세 설정.png)

그림 13. 상세 설정 — 애플리케이션 설정, 메시지 전송 토글, RCS/Kakao 전송 설정

**사용자 옵션 영역**

* 기본 설정: 파일 크기 제한, 업로드 한도, 멀티플라이어 카운트
* 타이밍 설정: ping time, ping delay, restart delay
* 디렉토리 / 인증: auth dir, file dir, OTP
* RCS 설정: 파일 YN, 자동 업로드, 리포트 카운트, 캐싱
* 기타: KISA 코드, 대행사 KEY / 브랜드 ID, RCS 통계 사용 여부

!\[상세 설정 - 사용자 옵션]\(./images/03-1. 상세 설정 - 사용자 설정.png)

그림 14. 사용자 설정 — 타이밍, 디렉토리/인증, RCS 옵션

{% hint style="info" %}
설정 변경 후 "저장" 버튼을 클릭하면 사이드바에 변경 내역이 표시됩니다. 최종적으로 사이드바 하단의 **"설정 적용"** 버튼을 눌러야 Odyssey에 반영됩니다.
{% endhint %}

### 세션 설정

통신사별 세션(계정) 정보를 카드 형태로 관리합니다. YAML의 `kt` / `rcs` / `cpaas` / `kakao` 영역의 `sessions`에 해당합니다.

* **KT 크로샷 세션**: RCS IP:PORT, SP ID, SP Password, End User, Auth file 등
* **KT RCS 세션**: Send URL, Auth URL, 인증 정보 (ID, Secret 등)
* **카카오 세션**: 엠앤와이즈 카카오 직접 연동 정보
* **CPaaS 세션**: KT CPaaS API 연동 정보

각 세션은 카드 UI로 표시되며, **추가/삭제** 버튼으로 세션을 관리할 수 있습니다.

!\[세션 설정 - KT 크로샷]\(./images/04. 세션 설정 - KT Xroshot.png)

그림 15. 세션 설정 — KT 크로샷 (SP ID, 접속 정보, SMS/LMS/MMS 토글)

!\[세션 설정 - KT RCS]\(./images/04-1. 세션 설정 - RCS.png)

그림 16. 세션 설정 — KT RCS (Send/Auth URL, 인증 정보, Report Cycle)

!\[세션 설정 - 카카오]\(./images/04-2. 세션 설 정- kakao.png)

그림 17. 세션 설정 — 카카오 (엠앤와이즈 카카오 직접 연동)

!\[세션 설정 - CPaaS]\(./images/04-3. 세션 설정 - cpaas.png)

그림 18. 세션 설정 — CPaaS (KT CPaaS API)

### 발송 금지 시간

요일별·시간대별 발송 차단 스케줄을 시각적으로 설정합니다.

* **시간 그리드**: 7일(월\~일) × 24시간 격자를 **드래그**하여 차단 시간대를 선택합니다.
* **우클릭**: 연결된 차단 블록을 한번에 해제합니다.
* **템플릿**: 자주 사용하는 차단 패턴을 저장/불러오기/삭제할 수 있습니다.

!\[발송 금지 시간 설정]\(./images/05. 발송 금지 시간 설정.png)

그림 19. 발송 금지 시간 설정 — 요일×시간 그리드 + 템플릿 관리

{% hint style="info" %}
설정값은 yaml이 아닌 `PAUSE_INFO` 테이블에 저장됩니다. 광고성 메시지는 정보통신망법에 따라 야간(21:00\~08:00) 발송이 금지되어 있으므로 해당 시간대를 차단 설정해야 합니다.
{% endhint %}

### 로그 관리

Odyssey 로그 파일을 브라우저에서 조회하고 다운로드할 수 있습니다.

* **날짜 필터**: 시작일\~종료일 범위로 로그 파일을 필터링합니다.
* **파일 브라우저**: `log/` 폴더와 `log_backup/` 폴더를 아코디언 형태로 탐색합니다.
* **다운로드**: 개별 파일 다운로드, 전체 ZIP 다운로드, 선택 파일 ZIP 다운로드를 지원합니다.

!\[로그 관리]\(./images/06. 로그 저장.png)

그림 20. 로그 관리 — 날짜 필터, log/log\_backup 디렉토리 탐색, 파일 선택 다운로드

### 이중화 설정

HA 운영 모드 선택, 부하 분산, `ha.properties` 직접 편집을 한 화면에서 처리합니다.

| 운영 모드              | 설명                                        | 부하 분산 / HA.PROPERTIES              |
| ------------------ | ----------------------------------------- | ---------------------------------- |
| **Standalone**     | 단일 노드 운영. 이중화 미사용.                        | 부하 분산 비활성, HA.PROPERTIES 비활성       |
| **Active/Active**  | 두 노드가 동시에 메시지를 나눠 발송. 처리량 ↑, 부하 분산.       | 부하 분산 활성, Load Balance Ratio 조정 가능 |
| **Active/Standby** | Master 한 대만 발송, Slave는 대기. 장애 시 자동/수동 전환. | HA\_AUTO\_SWITCH 활성, 부하 분산 비활성     |

!\[이중화 설정 - Standalone 모드]\(./images/07. 이중화설정 - SA.png)

그림 21. 이중화 설정 — Standalone 모드 (부하 분산 · HA.PROPERTIES 비활성)

!\[이중화 설정 - Active/Active 모드]\(./images/07-1. 이중화설정 - AA.png)

그림 22. 이중화 설정 — Active/Active 모드 (부하 분산 활성, Load Balance Ratio 조절 가능)

!\[이중화 설정 - Active/Standby 모드]\(./images/07-2. 이중화설정 - AS.png)

그림 23. 이중화 설정 — Active/Standby 모드 (HA\_AUTO\_SWITCH 활성)

{% hint style="info" %}
HA 프로파일로 기동한 경우에만 본 메뉴가 활성화됩니다. AS/SA 프로파일에서는 메뉴가 표시되지 않거나 일부 옵션이 비활성화될 수 있습니다.
{% endhint %}

## 21. 게이트웨이 IP / PORT

각 게이트웨이의 네트워크 정보입니다. (변동 시 별도 안내)

### 크로샷 2센터 서버 정보

| 구분             | 서버 IP                  | PORT | 비고               |
| -------------- | ---------------------- | ---- | ---------------- |
| 자원 관리 서버       | 210.105.195.140        | 80   | rcs2.xroshot.com |
| 메시지 연동 서버      | 210.105.195.150 \~ 155 |      |                  |
| 파일 연동 서버       | 210.105.195.145 \~ 147 |      |                  |
| 221.148.244.77 |                        |      |                  |

### 크로샷 차세대 서버 정보

| 구분        | 서버 IP                                                          | PORT | 비고               |
| --------- | -------------------------------------------------------------- | ---- | ---------------- |
| 자원 관리 서버  | 14.32.72.193 / 14.32.72.178 / 221.148.244.20 / 221.148.244.212 | 80   | info.xroshot.com |
| 메시지 연동 서버 | 14.32.72.20 / 14.32.72.148 / 221.148.244.22 / 221.148.244.194  | 8900 |                  |
| 파일 연동 서버  | 14.32.72.151 / 221.148.244.77                                  | 80   |                  |

### 크로샷 테스트 서버 정보

| 구분        | 서버 IP          | PORT |
| --------- | -------------- | ---- |
| 자원 관리 서버  | 112.175.63.229 | 80   |
| 메시지 연동 서버 | 112.175.63.228 |      |
| 파일 연동 서버  | 112.175.63.238 |      |

### Communis (CPaaS) 서버 정보

| 구분        | 내용                                                                                                                                                                                 |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 메인 도메인    | api.communis.kt.com                                                                                                                                                                |
| AWS ELB   | [http://nlb-ct01-prod-cpaas-public-01-aa0e5d0276f7ae6a.elb.ap-northeast-2.amazonaws.com/](http://nlb-ct01-prod-cpaas-public-01-aa0e5d0276f7ae6a.elb.ap-northeast-2.amazonaws.com/) |
| Public IP | 3.36.182.139, 15.165.192.121                                                                                                                                                       |
| PORT      | 443                                                                                                                                                                                |

## 22. 로그 / 에러 분석

### 22-1. Odyssey 로그 파일 구성

Odyssey의 로그는 `log/` 폴더에 출력되며, 일별로 압축되어 `log_backup/` 폴더에 보관됩니다. 주요 로그 파일은 다음과 같습니다.

| 로그 파일                                  | 내용                                                        |
| -------------------------------------- | --------------------------------------------------------- |
| agent.log                              | **전체 로그(catch-all)** — 모든 서비스 모듈 + HA 모듈 + Spring/DB 등 전반 |
| error.log                              | 에러 전용 로그 (장애 발생 시 우선 확인)                                  |
| router.log                             | Router 모듈 — 메시지 라우팅, 채널 분기                                |
| collect.log                            | Collector 모듈 — KT/RCS/카카오 수집 결과                           |
| send\_kt.log                           | KT 크로샷 발송 (SMS/LMS/MMS, legacy socket)                    |
| send\_rcs.log                          | KT RCS Hermes 발송                                          |
| send\_kko.log                          | 카카오 알림톡/친구톡 발송                                            |
| report.log                             | 리포트 처리 (수신 결과 콜백)                                         |
| cpaas.log                              | CPaaS API 발송/리포트 (legacy/kakao/rcs)                       |
| odyssey-app.out / odyssey-pipeline.out | JVM 콘솔 안전망 — Spring 부트 init, JVM 크래시 등 logback이 못 잡는 출력   |

{% hint style="info" %}
`agent.log`는 모든 모듈 로그를 통합해서 받는 전체 로그입니다. 특정 채널/모듈만 추적하고 싶을 땐 모듈별 파일을 참고하세요. 로그 파일 명은 logback 설정에 따라 환경별로 다를 수 있습니다. 정확한 파일명은 운영 환경의 `log/` 폴더를 확인하시기 바랍니다.
{% endhint %}

### 22-2. Odyssey 내부 에러 코드

Odyssey 자체에서 발생하는 내부 에러 코드입니다.

| CODE | CONTENT                 | 설명                          |
| ---- | ----------------------- | --------------------------- |
| 16   | Time out                | 발송 시간이 지난 메시지 (limit 옵션 참고) |
| 34   | Blank MsgType           | 메시지 타입 오류                   |
| 35   | Blank Number            | 수/발신 번호 비어있음                |
| 36   | cdr\_id Invalid Token   | 과금 정보 매칭 실패                 |
| 90   | SPAM Message            | 발송 금지 시간에 인입되어 자동 실패 처리됨    |
| 91   | Invalid File Extension  | 파일 형식 오류 (jpg/JPG 외)        |
| 92   | Different Content Count | 파일 개수 또는 파일 이름 오류           |
| 93   | Attached File Error     | 업로드 대상 첨부파일이 없거나 에러 상태      |
| 94   | File Upload Time out    | 파일 업로드 60초 이상 결과 없음         |
| 96   | IOException             | 입출력 작업 중 예외 발생              |
| 97   | NullPointerException    | Null 호출 예외 발생               |
| 98   | SQLException            | DB 예외 발생                    |
| 99   | Exception               | 기타 예외 발생                    |
| 403  | BlockedNumber           | 차단된 번호                      |
| 9998 | AgentStop               | Odyssey 종료                  |
| -92  | ImageDownload Failed    | 파일 다운로드 실패                  |

## 23. 부가 설명

### KT 크로샷 재접속 차단 기능

KT 크로샷으로 메시지(SMS/LMS/MMS)를 발송 중 특정 결과 코드를 수신할 경우, 세션을 끊고 재접속을 차단합니다. 이 경우 **원인을 해결한 뒤 Odyssey를 재구동**해야 세션 접속이 다시 가능합니다.

| 결과코드 | 설명                     |
| ---- | ---------------------- |
| 1    | 시스템 장애                 |
| 2    | 인증 실패 (인증 파일을 찾을 수 없음) |
| 5    | 인증 티켓 유효성 오류           |
| 6    | 가입 정보 없음               |
| 7    | 계정 패스워드 틀림             |
| 8    | 계정 일시정지                |
| 9    | 해지된 계정                 |
| 10   | 계정이 존재하지 않음            |
| 11   | 이미 연결되어 있음             |
| 17   | 인증 권한 없음 (접근 가능 IP 아님) |
| 18   | 다른 IP 로 중복 접속함         |
| 29   | 인증 티켓 만료               |

* **KT Xroshot 결과 코드**: `MCS_MSG_Error_코드표(TCS_RESULT).xlsx` (별도 제공)
* **KT RCS 중계 상품/밸리데이션**: `[별첨 1] KT RCS 중계 상품_리스트+밸리데이션-v2.1.xlsx`
* **KT RCS 에러 코드**: `[별첨 3] KT RCS 중계-ErrorCode-v2.1.xlsx`
* **엠앤와이즈 알림톡/친구톡**: `엠앤와이즈 알림톡/친구톡 설치가이드.pdf`

***

_Odyssey 통합 매뉴얼 v2 — © ㈜모노커뮤니케이션즈_

© 2026 ㈜모노커뮤니케이션즈. All rights reserved.
