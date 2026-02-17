# 1과목 (데이터 모델링의 이해)
## 1장
1. 함수적 종속성을 제거한다 -> 2차 정규화
2. 도메인: 어떤 데이터가 어떻게 어떤 형태로 얼만큼의 크기로 저장이 되어야 하는지 정의하는 것
3. 시스템카탈로그: 어떤 테이블이던가 여러가지 오브젝트들이 어떻게 저장되는지 저장이 되어 있음
4. 용어 사전: 데이터베이스에서 사용하는 용어들
5. 속성 사전: 속성에 대해 정의되어 있는 것
6. 참여자의 수: 관계차수 (Relationship degree)

## 2장
1. 정규화와 성능에 대한 설명
	- 중복 속성을 제거하여 용량을 최소화시킬 수 있음
	- 느려질 수 있음
	- 조회 성능을 향상시킬 수도 있고 아닐 수도 있다.
	- 일반적으로 데이터처리 성능이 향상됨
2. 관계(relationship), 조인(join)에 대한 설명
	- 조인이란 식별자를 상속하고 상속된 속성을 매핑키로 활용하여 데이터를 결합하는 것
	- 관계를 맺는다는 것은 식별자를 상속시키고 해당 식별자를 매핑키로 활용해 데이터를 결합해 보겠다는 것을 의미함
	- 부모의 식별자를 자식의 일반속성으로 상속하면 비식별관계, 부모의 식별자를 자식의 식별자에 포함하면 식별 관계
3. 

# 2과목 (SQL 기본 및 활용)
## 1장
1. DML (Data manipulation language)
	- Insert는 테이블에 데이터를 입력할 때 사용한다.
	- update는 입력한 정보 중에 잘못 입력되거나 변경이 필요하여 정보를 수정할 때 사용한다.
	- delete는 테이블의 정보가 필요 없게 되었을 경우 데이터 삭제를 수행한다.

2. select문
	- from 절이 없는 select문은 에러가 걸린다.
	- distinct 옵션을 통해 중복된 데이터가 있을 경우 1건으로 처리해 출력할 수 있음
	- where 절은 필수가 아니므로 생략 가능
	- select list에 서브쿼리가 사용될 수 있음
	- where절에는 집계함수(sum, avg, max, min)가 올 수 없음

3. sql server에서 ''는 공백도 null아니다
	- 오라클에서 ''는 null로 입력된다.

4. group by와 having절
	- 집계 함수의 통계 정보는 null값을 가진 행을 포함하여 수행할 수 없음
		- null값은 집계함수에서 데이터 취급을 하지 않는다.
	- group by 절에서는 select 절과 같이 alias 명을 사용할 수 없다.
	- having 절은 무조건 group by 절 뒤에 위치한다.
	- 집계 함수는 where 절에 올 수 없다.

5. 실행 결과가 다른 하나 문제 푸는 법
	- 먼저 select list를 보고 다른 게 있으면 소거
	- 그다음 order by를 본다.
	- order by에서 숫자는 select list에서의 순서를 숫자로 나타내는 것

6. 실행 결과
	- round(4.875, 2) = 4.88
	- length('korean') = 6
	- date_format('2024-11-02', '%Y-%m-%d') = 2024-11-02
	- substr('south korea', 8, 4) = 'orea'
		- 8번째부터 4개를 출력

7. select colb
    , max(cola) as cola1
	, min(cola) as cola2
	, sum(cola + colc) as sumac
	from tab
	group by colb 의 수행결과 보는 법
	- 먼저 groub by colb를 보고 맨 앞에 colb가 나오는지 또 똑같은 값으로 묶었는지 확인
	- 소거법을 하고 값이 다른 것을 찾아야 함

8. GROUP BY 사용 시 ORDER BY에는 그룹 기준 컬럼을 쓰거나 집계 함수를 써야 하며, 일반 컬럼을 단독으로 쓰면 오류가 발생

9. 오라클에서 from 절에 ,로 있고 where절이 없는 조인이면 카티션 곱(cross join)임

## 2장
1. 집합 연산자
	- union: 합집합 중복제거 
	- minus: 차집합
	- intersect: 교집합
	- except: 차집합

2. union all, union
	- union all: 양 테이블을 합침
	- union: 중복 제거하고 출력