## 1. SQL 연산 순서
- From 
- where
- group by
- having
- select
- Order by

- DML: select, insert, update, delete
- DDL: alter, create, modify, drop
- TCL: Rollback, commit
- DCL: grant, revoke

## 2. Distinct
어떤 컬럼값들의 중복을 제거한 결과를 출력한다.
- Select distinct col from table;
- Select distinct col1, col2 from table;의 경우엔 col1과 col2의 값이 모두 같지 않은 것만 출력한다.

## 3. **Alias**
select절에서 사용가능, where절에서는 사용불가
Select col as name from table; - select col name from table;
- as는 생략이 가능

## 4. concat
데이터를 붙이는 함수
- Select col1 + col2 + col3 from table; (SQL server (ms sql))
- select col1 || col2|| col3 from table; (oracle)
- select concat(col1, col2) from table; *concat()은 연산자가 2개

## 5. 논리연산자
1. NOT: ~가 아니다   
    - where not name = '한종구'
2. AND: A 그리고 B 
    - where A and B
3. OR: A 또는 B 
    - where A or B

## 6. SQL 연산자
- A between B and C
    - B <= A <= C
- A in (1, 2, 3) 
    - A = 1 or A = 2 or A = 3
- A like '_ble*'
    - A의 값 중 2, 3, 4번째 값이 ble인 모든 데이터 출력

## 7. escape
- _, *을 사용하고 싶을 때 사용
- and email like '@_%' escape '@'

## 8. rownum, top
- oracle에선 where절 옆에 rownum
    - where rownum <= 10 -> 10개의 데이터 row가 나옴
    - where rownum = 3 -> 이러면 아무 데이터도 안 나옴 (에러도 아님)
- SQL server의 경우 select 옆에 top
    - select top(3) name from table;
    - 이렇게 하면 3개가 나옴

## 9. null의 정의
- 모르는 값, 정의되지 않은 값(공백이나 0과는 다르다)
- 산술연산에서 null이 들어가면 null이 출력
    - null + 2, null * 4, null + null 모두 결과는 null
    - null + 100 > null + 1
- 조건절에 null이 들어가면 false를 반환
    - null = null, null = 2 -> false를 반환
- 집계함수(sum, count, min, max ---)에서 null은 데이터 대상에서 제외
- 정렬시에는 오라클에서는 가장 큰 값이 되고 SQL Server에서는 가장 작은 값이 됨
- Nvl(col, 0): col이 null이면 0 반환, 아니면 1 반환
- Nvl2(col, 1, 0): col이 null이면 0반환, 아니면 1 반환
- Isnull(col, 0): col이 null이면 0반환, 아니면 col 반환
- Nullif(col, 0): col이 0이면 null 반환, 아니면 col 반환
- Coalesce(col1, col2, col3): null이 아닌 첫 번째 값 반환
    - col1 = null, col2 = null, col3 != null -> col3 반환

## 10. 정렬
- 느려질 수 있음
- 가장 마지막에 실행
- null이 어디에 오는지

- 컬럼명으로 정렬, 앞의 기준이 같을 때 그 다음 컬럼으로 정렬
- 기본값은 asc(오름차순), desc(내림차순)
- Order by col1, col2 desc
    - col1을 정렬하고 같은 값이 있으면 col2로 내림차순 정렬

- 출력순서로 정렬, select 절의 출력순서로 지정

## 11. 숫자함수
- Round(222.45, 1) 소수점 둘째자리에서 반올림하여 첫째자리까지 출력
    - 222.5
- Round(225.67, 0) 소수점 첫째자리에서 반올림하여 정수만 출력
    - 226
- Round(226.35, -1) 1의 자리에서 반올림하여 정수만 출력
    - 230
- Ceil(oracle)/ceiling(SQL Server) 올림함수, 파라미터 사용법은 round와 같음
- Floor: 버림 함수, 파라미터 사용법은 round와 같음

## 12. 문자함수
- lower, upper: 소문자로, 대문자로
- Trim, itrim, rtrim: 양쪽공백제거 왼쪽, 오른쪽 공백제거
- lpad, rpad: 특정 자리를 정하고, 왼쪽/오른쪽의 공백을 채워주는 함수
    - select lpad('A', 5, '*') from dual;
    - \*\*\*\*A, rpad면 A****
- substr: select substr('korea', 2, 2) from dual
    - or이 출력
- instr: select instr('corporate floor','po') as idx from dual
    - 문자를 찾아내는 함수 앞에서부터 찾아서 위치 출력 1부터 시작
    - 4가 출력

## 13. 날짜함수
- to_char: 날짜형 데이터를 문자로 출력
    - select to_char(sysdate, 'YYYY MM DD') from dual;
    - 2026 02 13 출력
- to_date: 문자형 데이터를 날짜형으로 출력
    - select to_date('2022-09-22') from dual;
    - 2022-09-22로 출력함
    - 날짜형으로 출력하는 이유
        - 날짜 함수를 사용해서 더하거나 찾거나 월을 더하거나 뺄 수 있는 기능을 사용할 수 있어 날짜형이 있음
- sysdate (oracle), getdate() (SQL Server)
    - 현재 시간을 알 수 있는 함수

## 14. 조건문
- Decode
    - select decode(col1, 'A', 1, 'B', 2, 3) from dual;
    - col이 A면 1, B면 2 아니면 3
- case
    ```mysql
    case when col = 'A' then 1
         when col = 'B' then 2
         else 3 end;
    ```
    서로 같음
    ```mysql
    case col when 'A' then 1
             when 'B' then 2
             else 3 end; 
    ```

## 15. 집계함수
- cound, min, sum, max 등
    - null은 포함 X
        - null은 데이터가 없다고 생각
    - (1, null, 2, 3, null)의 데이터를 기준으로 결과는 다음과 같다.
        - count(): 3
        - sum(): 6
        - avg(): 2
        - min(): 1
        - max(): 3

    |col1|col2|col3|
    |----|----|----|
    |null|null|1|
    |1|null|null|
    - select sum(col1 + col2 + col3) from dual;
        - 여기에서 먼저 sum을 생각하지 말고 col1 + col2 + col3을 먼저 생각한다면 행은 null + null + 1이기에 null이 반환되고 마지막 세번째 행도 마찬가지 그러므로 두번째 행의 2 + 3 + 2의 값인 7이 결과가 됨
    - select sum(col1) + sum(col2) + sum(col3)
        - 3 + 3 + 3 = 9 

## 16. 그룹바이 group by
- 집약기능을 가지고 있음(다수의 행을 하나로 합침)
- Group by절에 온 컬럼만 select절에 올 수 있음

## 17. join
- natural join
    - 반드시 두 테이블 간의 동일한 이름, 타입을 가진 컬럼이 필요하다.
    - 조인에 이용되는 컬럼은 명시하지 않아도 자동으로 조인에 사용된다.
    - 동일한 이름을 갖는 컬럼이 있지만 데이터 타입이 다르면 에러가 발생한다.
    - 조인하는 테이블 간의 동일 컬럼이 select 절에 기술 되어도 테이블 이름을 생략해야 한다.
    - select department_id 부서, department_name 부서이름, location_id 지역번호, city 도시
        form department
        natural join locations
        where city = 'Seattle';
    
- Using
    - using절은 조인에 사용될 컬럼을 지정한다.
    - natural절과 using절은 함께 사용할 수 없다.
    - 조인에 이용되지 않은 동일 이름을 가진 컬럼은 컬럼명 앞에 테이블명을 기술한다.
    - 조인 컬럼은 괄호로 묶어서 기술해야 한다.
    - select department_id 부서번호, d.departmane_name 부서, location_id 지역번호, city 도시
        from departments.d
        join locations using (location_id);
    
- left outer join
    - from table a left outer join table b
        on a.col = b.col
    이것과 같은 오라클 sql 문법은
    = from table a, table b
        where a.col = b.col(+)

- join 순서
    - from a,b,c
        a와 b가 join되고, 그리고 c와 join 된다.

## 18. 서브쿼리
- select: 스칼라서브쿼리
- from: 인라인뷰(메인쿼리의 컬럼사용 가능)
- where: 중첩서브쿼리
- group by: 사용불가
- having: 중첩서브쿼리
- order by: 스칼라서브쿼리
- in: 서브쿼리출력값들 or 조건
- Any/some: 서브쿼리출력값들 중 가장 작거나 큰값과 비교
- All: any/some과 반대개념
- Exists: 서브쿼리 내 select절엔 뭐가 와도 상관없다. Row가 있으면 false

## 19. 집합연산자
- union: 정렬 O, 중복제거 O, 느리다
- intersect: 정렬 O, 교집합, 느리다
- Minus(except): 정렬 O, 차집합, 느리다
- union all: 정렬 X, 중복제거 X, 빠르다

## 20. DDL
- truncate: drop & create, 테이블 내부구조는 남아있으나 데이터가 모두 삭제됨
- drop: 테이블 자체가 없어짐 (당연히 데이터도 없음)
- delete: 데이터만 삭제
- rollback, commit과 항상 같이 나옴

## 21. DML
- insert: 데이터 넣는 명령: insert into 테이블(col1, col2, col3) values('11','22','33')
    - values를 기준으로 좌우의 괄호 속 개수가 맞는지
- update: 데이터의 특정 행 값을 변경(delete & insert)
    - update 테이블 set col = '값' where col1 = '조건';
- delete: 데이터의 특정 행을 삭제
    - delete from 테이블 where col = '조건';
- merge: 특정 데이터를 넣을 때 해당 테이블 키값을 기준으로 있으면 update, 없으면 insert를 한다.
위 문제 모두 commit, rollback, savepoint와 주로 출제

## 22. 제약조건
- pk: not null + unique
    - 테이블당 하나의 pk를 가질 수 있음(하나라는 게 컬럼이 아님, 복합키 가능)
- not null: 해당 컬럼에 null이 올 수 없음
- unique: 해당 컬럼에 중복값이 올 수 없음

## 23. DCL
- grant, revoke 문법
    - grant 시스템 권한명[ 시스템 권한명... | 롤명] TO 유저명[. 유저명... | 롤명... | PUBLIC | [WITH ADMIN OPTION]];
        - TO 유저
    - revoke { 권한명[. 권한명...] ALL} on 객체명 from {유저명[. 유저명...] | 룰명(ROLE) | PUBLC } [CASCADE CONSTRAINTS];
        - FROM 유저
    - role은 객체

## 24. VIEW
- 독립성, 편의성, 보안성
- sql을 저장하는 개념
- 인덱싱하기 힘들다
- insert update delete가 자유롭지 못하는 단점이 있음

## 25. 그룹함수
- roll up 
    - 한쪽에 NULL만 있음
- cube
    - 조합 가능한 모든 경우의 수를 보여줌
    - 모든 쪽에 NULL이 있음
- groupingsets
- grouping

**원본테이블**
|분류|내용|개수|금액| 
|----|----|----|----| 
|학용품|연필|1|400|
|학용품|지우개|3|1200|
|학용품|샤프|2|800|
|음식|김밥|1|2000|
|음식|제육덮밥|1|4800|
|음식|제육덮밥|2|9600|
|음식|게임|1|100|

**ROLLUP**
|분류|내용|개수|금액| 
|----|----|----|----| 
|기타|개임|1|100|
|기타|NULL|1|100|
|음식|김밥|1|2000|
|음식|제육덮밥|3|14400|
|음식|NULL|4|16400|
|학용품|샤프|2|800|
|학용품|연필|1|400|
|학용품|지우개|3|1200|
|학용품|NULL|6|2400|

**CUBE**
|분류|내용|개수|금액| 
|----|----|----|----| 
|기타|게임|1|100|
|NULL|게임|1|100|
|음식|김밥|1|2000|
|NULL|김밥|1|2000|
|학용품|샤프|2|800|
|NULL|샤프|2|800|
|학용품|연필|1|400|
|NULL|연필|1|400|
|음식|제육덮밥|3|14400|
|NULL|제육덮밥|3|14400|
|학용품|지우개|3|1200|
|NULL|지우개|3|1200|
|NULL|NULL|11|18900|
|기타|NULL|1|100|
|음식|NULL|4|16400|
|학용품|NULL|6|2400|
- ROLLUP
    - (GROUP BY에 있는 컬럼들은 오른쪽에서 왼쪽순으로 그룹 생성)
    - a, b로 묶이는 그룹의 값
    - a로 묶이는 그룹의 소계
    - 전체합계
- CUBE
    - (나올 수 있는 모든 경우의 수로 그룹 생성)
    - a, b로 묶이는 그룹의 값
    - a로 묶이는 그룹의 소계
    - b로 묶이는 그룹의 소계
    - 전체합계

    - \*rollup(A,B) != rollup(B,A), cube(A,B) = cube(B,A)

## 26. TCL
- Commit, rollback
    - auto commit, begin transaction(commit 기능 잠시 끄기) end

## 27. 윈도우함수
- rows between and 값이 증가한다.
    - rows between unbounded precending and current row as "직업별 합계"
        - 처음부터 지금까지의 어떤 값의 합계
    - rows between 1 precending and 1 FOLLOWING as "위아래 합계"
        - 내 앞의 값 1 내 뒤의 값 1
- range between and 값이 동일하다
    1. UNBOUNDED PRECENDING: 최종 출력될 값의 맨 처음 row의 값(Partition by 고려)
    2. CURRENT ROW: 현재 row의 값
    3. UNBOUNDED FOLLOWING: 최종 출력될 값의 맨 마지막 row의 값(partition by 고려)
        - partition by란 파티션 안에서 처음이나 마지막 값임
- rank -> 1, 1, 3, 4
- dense_rank -> 1,1,2,3
- partition by, order by
    - row_number() over (partition by col1 order by col2)
    - col1의 파티션에서 col2의 오름차순으로 번호를 매김 -> 이게 partition by

## 28. 계층형함수
- prior 자식데이터 = 부모데이터
- 부모데이터에서 자식데이터로 가면 순방향

- select level      \*순방향
    -           LPAD('', 4 * (level - 1)) || 사원사원,
                관리자,
                CONNECT_BY_ISLEAF ISLEAF
            FROM 사원
        START WITH 관리자IS NULL
    CONNECT BY PRIOR 사원 = 관리자;
- SELECT LEVEL,     \*역방향
                LPAD('', 4 * (LEVEL - 1)) | 사원사원,
                관리자,
                CONNECT_BY_ISLEAF ISLEAF
            FROM 사원
        START WITH 사원 = 'D'
    CONNECT BY PRIOR 관리자 = 사원;

## 29. 엔터티
- 관리해야 할 대상이 엔티티가 될 수 있다.
- 인스턴스 2개 이상
- 업무에서 사용해야 함(프로세스)
- 관계를 하나 이상 가져야 한다.

- 유형엔터티
    - 사람 물건 조직처럼 독립적으로 존재하는 대상
- 개념엔터티
    - 현실의 물체라기보다 업무에서 필요한 구분/정책/분류/코드 같은 개념
- 사건엔터티
    - 업무에서 발생하는 행위/거래/이력처럼 발생했다가 핵심 

- 기본엔터티  
    - 계좌, 고객
- 중심엔터티
    - 대출 상품, 다른 상품
- 행위엔터티
    - 계좌에 입출력, 대출금을 갚는 것

## 30. 속성
- 기본속성
    - 이름, 전화번호
- 설계속성
    - 실제로 데이터를 가지고 있지 않지만 아이디를 만든다거나 어떤 상태를 만드는 것
    - 어떤 로직에 의해서 만들어짐
- 파생속성
    - 합계, 평균값 다른 데이터 컬럼을 통해서 만들어진 것

## 31. 도메인
- 데이터유형
    - VARCHAR, NUMBER
- 크기
    - VARCHAR(100)
- 제약조건
    - check, primary key, foreign key, not null, unique 등

## 32. 식별자
- 유일성: 유일하게 인스턴스를 구분
- 최소성: 최소 컬럼으로
- 불변성: 값이 바뀌지 않아야 함
- 존재성: not null
    - 위 4개를 만족하면 후보키가 될 수 있으며, 그 중 하나, 대표하는 것이 기본키이다.

## 33. 식별자 & 비식별자
- 식별자
    - 강한관계
    - PK가 많아진다(조인시)
    - SQL이 복잡해짐
- 비식별자    
    - 약한관계
    - sql이 느려짐

## 34. ERD
- 그리는 방법
    - 좌상에서 우하로
    - 관계명은 반드시 표기하지 않아도 됨
    - UML은 객체지향에서만 쓰인다.

## 35. 성능 데이터 모델링
- 아키텍쳐모델링(먼저)
    - 테이블, 파티션, 컬럼 등의 정규화 및 반정규화
- sql 튜닝(그다음)
    - join 수행원리

## 36. 정규화
- 1차 원자성
- 2차 부분함수종속성제거
- 3차 이행함수종속성제거
    - 1,2,3차만 알고 있어도 됨
- BCNF

|정규화 절차|설명|
|----------|----|
|제1정규화|속성의 원자성을 확보, **기본키를 설정**|
|제2정규화|기본키가 2개 이상의 속성으로 이루어진 경우, **부분함수 종속성**을 제거(분해)|
|제3정규화|기본키를 제외한 칼럼 간에 종속성 제거, **이행함수 종속성**을 제거|
|BCNF|기본키를 제외하고 후보키가 있는 경우, 후보키가 기본키를 종속시키면 분해|
|제4정규화|여러칼럼들이 하나의 칼럼을 종속시키는 경우 분해하여 다중값 종속성을 제거|
|제5정규화|조인에 의해서 종속성이 발생되는 경우 분해|

- select시 join 때문에 느려질 수 있다.
- insert, update는 빨라질 수 있다.(테이블 사이즈가 작아져서)
- 1,2,3차만 외우기

## 37. 이상현상
1. 삽입 이상: 새 데이터를 삽입하기 위해 불필요한 데이터도 함께 삽입해야 하는 이상 문제
2. 갱신 이상: 중복튜플 중 일부만 변경하여 데이터가 불일치하게 되는 이상 문제
3. 삭제 이상: 튜플을 삭제하면 필요한 데이터까지 함께 삭제되는 이상 문제

## 38. 반정규화
- 데이터의 무결성을 해칠 수 있음
- 절차
    - 대량범위 빈도수 조사
        - 얼마나 자주 많은 데이터를 처리하는지 조사
    - 범위처리 빈도수
        - 여러 테이블이나 한 테이블에서 다수의 값을 처리해야 되는 빈도수
    - 통계처리 여부
- 종류
    - 테이블 병합 1:1 / 1:M
    - 슈퍼/서브타입 병합
    - 부분테이블 분할
    - 통계테이블 분할
    - 중복테이블 분할
    - 부분테이블 분할
    - 이력 컬럼 추가
    - 중복 컬럼 추가
    - PK를 일반 컬럼으로 병합
    - 파생 컬럼 추가
    - 응용시스템 오작동을 피하기 위한 임시값 컬럼 추가
    - 중복관계 추가

## 39. 슈퍼/서브타입
- 메인 엔터티가 있고 기능에 따라 테이블을 서브로 만듬
- 종류
    1. 1:1 타입 one to one type
        - 1:1로만 있음
    2. 슈퍼 + 서브타입
        - 아래로 여러 테이블을 만듬
    3. ALL in One 타입
        - 하나에만 다 넣는 것 