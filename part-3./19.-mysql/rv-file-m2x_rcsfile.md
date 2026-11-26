# RCS 파일 (M2X\_RCSFILE) 테이블

{% hint style="info" %}
컬럼의 데이터 타입은 DBMS 에 따라 다릅니다. DBMS 별 데이터 타입은 표 아래의 [DBMS 별 테이블 생성문](#create-table) 에서 확인하세요.
{% endhint %}

<table><thead><tr><th width="135.20001220703125">컬럼명</th><th width="171.79998779296875">데이터 타입</th><th width="79">NN</th><th width="93">기본값</th><th width="220.199951171875">설명</th></tr></thead><tbody><tr><td><strong><code>ID</code></strong></td><td>BIGINT(20) AUTO_INCREMENT</td><td>Y</td><td></td><td>첨부 파일 유니크 번호 (PK)</td></tr><tr><td><strong><code>FILE_PATH</code></strong></td><td>VARCHAR(200)</td><td>Y</td><td></td><td>발송 테이블에 사용된 파일 경로</td></tr><tr><td><strong><code>DESCRIPTION</code></strong></td><td>VARCHAR(500)</td><td></td><td></td><td>파일 최종 수정 정보 (동명 파일 대비)</td></tr><tr><td><strong><code>STATUS</code></strong></td><td>SMALLINT</td><td></td><td>0</td><td>0=대기, 2=치환 가능, 3=실패</td></tr><tr><td><strong><code>FILEID</code></strong></td><td>VARCHAR(64)</td><td></td><td></td><td>자동 업로드 된 파일 ID</td></tr><tr><td><strong><code>SUBMIT_TIME</code></strong></td><td>VARCHAR(16)</td><td>Y</td><td></td><td>등록 시각</td></tr><tr><td><strong><code>UPLOAD_TIME</code></strong></td><td>VARCHAR(16)</td><td></td><td></td><td>업로드 시각</td></tr><tr><td><strong><code>EXPIRY_TIME</code></strong></td><td>VARCHAR(16)</td><td></td><td></td><td>만료 시각</td></tr><tr><td><strong><code>RESULT</code></strong></td><td>INT(6)</td><td></td><td>-2</td><td>업로드 결과 값</td></tr><tr><td><strong><code>RESULT_DESC</code></strong></td><td>VARCHAR(1000)</td><td></td><td></td><td>결과값 상세</td></tr><tr><td><strong><code>RCS_ID</code></strong></td><td>VARCHAR(20)</td><td></td><td></td><td>발송 세션 RCS_ID</td></tr></tbody></table>

## <mark style="color:blue;">DBMS 별 테이블 생성문</mark> <a href="#create-table" id="create-table"></a>

<mark style="color:red;">**`config/mapper/{{DBMS}}/table.xml`**</mark> 의 `createRcsFileTable` 내용입니다. 테이블은 Odyssey 가 최초 기동 때 자동으로 만듭니다.

{% tabs %}
{% tab title="MySQL" %}
```sql
CREATE TABLE IF NOT EXISTS M2X_RCSFILE (
    ID BIGINT(20) NOT NULL AUTO_INCREMENT,
    FILE_PATH VARCHAR(200) NOT NULL,
    DESCRIPTION VARCHAR(500) NULL,
    STATUS SMALLINT(6) NULL DEFAULT '0',
    FILEID VARCHAR(64) NULL DEFAULT NULL,
    SUBMIT_TIME VARCHAR(16) NOT NULL,
    UPLOAD_TIME VARCHAR(16) NULL DEFAULT NULL,
    EXPIRY_TIME VARCHAR(16) NULL DEFAULT NULL,
    RESULT INT(6) NULL DEFAULT '-2',
    RESULT_DESC VARCHAR(1000) NULL,
    RCS_ID VARCHAR(20) NULL DEFAULT NULL,
    PRIMARY KEY(ID)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci
```
{% endtab %}

{% tab title="MariaDB" %}
```sql
CREATE TABLE IF NOT EXISTS M2X_RCSFILE (
    ID BIGINT(20) NOT NULL AUTO_INCREMENT,
    FILE_PATH VARCHAR(200) NOT NULL,
    DESCRIPTION VARCHAR(500) NULL,
    STATUS SMALLINT(6) NULL DEFAULT '0',
    FILEID VARCHAR(64) NULL DEFAULT NULL,
    SUBMIT_TIME VARCHAR(16) NOT NULL,
    UPLOAD_TIME VARCHAR(16) NULL DEFAULT NULL,
    EXPIRY_TIME VARCHAR(16) NULL DEFAULT NULL,
    RESULT INT(6) NULL DEFAULT '-2',
    RESULT_DESC VARCHAR(1000) NULL,
    RCS_ID VARCHAR(20) NULL DEFAULT NULL,
    PRIMARY KEY(ID)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci
```
{% endtab %}

{% tab title="PostgreSQL" %}
```sql
CREATE TABLE IF NOT EXISTS M2X_RCSFILE (
    ID          BIGSERIAL     PRIMARY KEY,
    FILE_PATH   VARCHAR(200)  NOT NULL,
    DESCRIPTION VARCHAR(500),
    STATUS      SMALLINT      DEFAULT 0,
    FILEID      VARCHAR(64),
    SUBMIT_TIME VARCHAR(16)   NOT NULL,
    UPLOAD_TIME VARCHAR(16),
    EXPIRY_TIME VARCHAR(16),
    RESULT      INTEGER       DEFAULT -2,
    RESULT_DESC VARCHAR(1000),
    RCS_ID      VARCHAR(20)
)
```
{% endtab %}

{% tab title="Oracle" %}
```sql
DECLARE
    v_new BOOLEAN := TRUE;
BEGIN
    BEGIN
        EXECUTE IMMEDIATE 'CREATE TABLE M2X_RCSFILE (
    ID          NUMBER(20)    PRIMARY KEY,
    FILE_PATH   VARCHAR2(200) NOT NULL,
    DESCRIPTION VARCHAR2(500),
    STATUS      SMALLINT      DEFAULT 0,
    FILEID      VARCHAR2(64),
    SUBMIT_TIME VARCHAR2(16)  NOT NULL,
    UPLOAD_TIME VARCHAR2(16),
    EXPIRY_TIME VARCHAR2(16),
    RESULT      NUMBER(6)     DEFAULT -2,
    RESULT_DESC VARCHAR2(1000),
    RCS_ID      VARCHAR2(20)
)';
    EXCEPTION WHEN OTHERS THEN
        IF SQLCODE = -955 THEN v_new := FALSE; ELSE RAISE; END IF;
    END;
    IF v_new THEN
        BEGIN
            EXECUTE IMMEDIATE 'CREATE SEQUENCE SQ_M2X_RCSFILE START WITH 1 INCREMENT BY 1';
        EXCEPTION WHEN OTHERS THEN
            IF SQLCODE != -955 THEN RAISE; END IF;
        END;
        EXECUTE IMMEDIATE 'CREATE OR REPLACE TRIGGER TR_M2X_RCSFILE BEFORE INSERT ON M2X_RCSFILE FOR EACH ROW WHEN (NEW.ID IS NULL) BEGIN SELECT SQ_M2X_RCSFILE.NEXTVAL INTO :NEW.ID FROM DUAL; END;';
    END IF;
END;
```
{% endtab %}

{% tab title="SQL Server" %}
```sql
IF OBJECT_ID('M2X_RCSFILE', 'U') IS NULL
CREATE TABLE M2X_RCSFILE (
    ID          BIGINT         IDENTITY(1,1) PRIMARY KEY,
    FILE_PATH   NVARCHAR(200)  NOT NULL,
    DESCRIPTION NVARCHAR(500),
    STATUS      SMALLINT       DEFAULT 0,
    FILEID      NVARCHAR(64),
    SUBMIT_TIME NVARCHAR(16)   NOT NULL,
    UPLOAD_TIME NVARCHAR(16),
    EXPIRY_TIME NVARCHAR(16),
    RESULT      INT            DEFAULT -2,
    RESULT_DESC NVARCHAR(1000),
    RCS_ID      NVARCHAR(20)
)
```
{% endtab %}
{% endtabs %}
