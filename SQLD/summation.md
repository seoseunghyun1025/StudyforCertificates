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