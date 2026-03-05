# 🏆 SQLD 자격검정 대비: 관리 구문(DDL, DML, TCL, DCL) 끝장 정리

본 문서는 2024년 개편된 SQLD 출제 기준에 맞추어 작성되었습니다. 벤더별(Oracle, MSSQL, MySQL) 문법 차이를 중심으로 상세히 다룹니다.

---

## 1. DDL (Data Definition Language, 데이터 정의어)
데이터베이스의 **구조(Schema)**를 정의, 변경, 삭제합니다. 실행 즉시 DB에 반영(Auto Commit)됩니다.

### 📋 [시나리오] 서비스 운영을 위한 '상품(PRODUCT)' 테이블 관리

#### 1-1. 테이블 생성 (CREATE)
벤더별로 데이터 타입과 자동 증가(Identity) 설정 방식이 다릅니다.



* **Oracle**
    ```sql
    CREATE TABLE PRODUCT (
        PROD_ID    NUMBER(10) PRIMARY KEY,     -- 숫자형
        PROD_NAME  VARCHAR2(100) NOT NULL,     -- 가변 문자형 (2000/4000자 제한)
        PRICE      NUMBER(10) DEFAULT 0,
        REG_DATE   DATE DEFAULT SYSDATE        -- 현재 시간
    );
    -- 자동 증가가 필요할 경우: GENERATED AS IDENTITY 사용 (12c 이상)
    ```

* **SQL Server (MSSQL)**
    ```sql
    CREATE TABLE PRODUCT (
        PROD_ID    INT PRIMARY KEY IDENTITY(1,1), -- 자동 증가 (시작, 증가)
        PROD_NAME  VARCHAR(100) NOT NULL,
        PRICE      INT DEFAULT 0,
        REG_DATE   DATETIME DEFAULT GETDATE()     -- 현재 시간
    );
    ```

* **MySQL**
    ```sql
    CREATE TABLE PRODUCT (
        PROD_ID    INT PRIMARY KEY AUTO_INCREMENT, -- 자동 증가
        PROD_NAME  VARCHAR(100) NOT NULL,
        PRICE      INT DEFAULT 0,
        REG_DATE   TIMESTAMP DEFAULT CURRENT_TIMESTAMP -- 현재 시간
    );
    ```

#### 1-2. 테이블 구조 변경 (ALTER) - ★시험 빈출★
컬럼을 추가, 수정, 삭제하는 문법은 벤더별로 가장 많이 헷갈리는 부분입니다.

| 작업 내용 | Oracle | SQL Server (MSSQL) | MySQL |
| :--- | :--- | :--- | :--- |
| **컬럼 추가** | `ADD (CNT NUMBER)` | `ADD CNT INT` | `ADD CNT INT` |
| **컬럼 수정** | `MODIFY (NAME VARCHAR2(50))` | `ALTER COLUMN NAME VARCHAR(50)` | `MODIFY COLUMN NAME VARCHAR(50)` |
| **컬럼 삭제** | `DROP COLUMN CNT` | `DROP COLUMN CNT` | `DROP COLUMN CNT` |
| **컬럼명 변경**| `RENAME COLUMN A TO B` | `sp_rename 'TAB.A', 'B', 'COLUMN'` | `CHANGE COLUMN A B VARCHAR(20)` |
| **제약조건 삭제**| `DROP CONSTRAINT 명칭` | `DROP CONSTRAINT 명칭` | `DROP FOREIGN KEY 명칭` |

---

## 2. DML (Data Manipulation Language, 데이터 조작어)
테이블 내의 **데이터(행, Row)**를 관리합니다. TCL을 통해 확정 전까지 취소가 가능합니다.

#### 2-1. 데이터 입력, 수정, 삭제 (INSERT, UPDATE, DELETE)
```sql
-- [입력] 공통 문법
INSERT INTO PRODUCT (PROD_ID, PROD_NAME, PRICE) VALUES (101, '노트북', 1500000);

-- [수정] 공통 문법
UPDATE PRODUCT SET PRICE = 1400000 WHERE PROD_ID = 101;

-- [삭제] 행 단위 삭제, Rollback 가능
DELETE FROM PRODUCT WHERE PROD_ID = 101;
```

#### 2-2. 조회 제한 (Top-N Query) - ★무조건 출제★
특정 개수의 행만 추출하는 방식은 벤더마다 완전히 다릅니다.
```sql
Oracle: SELECT * FROM (SELECT * FROM PRODUCT ORDER BY PRICE DESC) WHERE ROWNUM <= 3; (또는 12c 이후 FETCH FIRST 3 ROWS ONLY)
```

## 3. TCL (Transaction Control Language, 트랜잭션 제어어)
DML 작업 단위를 제어하여 데이터의 무결성을 유지합니다.
- **COMMIT**: 작업을 영구 저장합니다.
- **ROLLBACK**: 작업을 취소하고 이전 상태로 되돌립니다.
- **SAVEPOINT**: 특정 지점을 저장하여, 전체가 아닌 해당 지점까지만 ROLLBACK 할 수 있게 합니다.
- **Oracle**: SAVEPOINT SV1; -> ROLLBACK TO SV1;
- **MSSQL**: SAVE TRANSACTION SV1; -> ROLLBACK TRANSACTION SV1;
**💡 [중요] 자동 커밋(Auto-Commit)의 차이**
**Oracle**: DML은 수동 커밋이 기본입니다. 하지만 DDL(CREATE, ALTER 등)을 실행하면 이전의 DML 작업까지 자동으로 COMMIT 되어 버리니 주의해야 합니다.

**MSSQL/MySQL**: 기본적으로 모든 명령어가 Auto-Commit 모드입니다. 트랜잭션을 수동으로 관리하려면 BEGIN TRAN 혹은 START TRANSACTION을 명시해야 합니다.
MSSQL: SELECT TOP 3 * FROM PRODUCT ORDER BY PRICE DESC;

## 4. DCL (Data Control Language, 데이터 제어어)
사용자 권한 및 접근을 제어합니다. (※ 2024년 SQLD 개편으로 출제 비중이 거의 없으나 용어는 알아야 함)
- **GRANT**: 권한 부여 (GRANT SELECT, INSERT ON PRODUCT TO USER_A;)
- **REVOKE**: 권한 회수 (REVOKE INSERT ON PRODUCT FROM USER_A;)
