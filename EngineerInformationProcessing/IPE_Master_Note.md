01. 요구사항 & 설계 (UML/디자인 패턴)
🔴 UML (Unified Modeling Language)
구조적(정적): 클래스, 객체, 컴포넌트, 배치, 복합체, 패키지. (클/객/컴/배/복/패)
행위적(동적): 유스케이스, 시퀀스, 커뮤니케이션, 상태, 활동, 상호작용, 타이밍. (유/시/커/상/활/상/타)
관계(Relationship) 기호: * 집단(Aggregation): 빈 마름모. 부분-전체 관계. 독립적임.
포함(Composition): 채워진 마름모. 생명주기 같이함. 종속적임.
일반화(Generalization): 상속(Inheritance). 부모-자식 관계. 빈 화살표.
실체화(Realization): 인터페이스 구현. 점선 화살표.

🔴 디자인 패턴 (GoF 23종) - 무조건 나옴
생성(5개): 추상 팩토리, 빌더, 팩토리 메서드, 프로토타입, 싱글톤. (추/빌/팩/프/싱)
싱글톤: 인스턴스 딱 하나. 전역 접근.
구조(7개): 어댑터, 브리지, 컴포지트, 데코레이터, 퍼사드, 플라이웨이트, 프록시. (어/브/컴/데/퍼/플/프)
어댑터: 인터페이스 호환성 해결.
데코레이터: 기능 동적 추가.
행위(11개): 옵저버, 전략(Strategy), 템플릿 메서드, 커맨드, 상태, 반복자 등. (옵/전/템/커/상/반...)
전략: 알고리즘 캡슐화해서 교체.
옵저버: 1:N 상태 변화 통지.

02. 데이터베이스 (SQL & 정규화)
🔴 정규화 (도부이결다조)
1NF: 원자값(Atomic value).
2NF: 부분 함수 종속 제거 (완전 함수 종속).
3NF: 이행 함수 종속 제거.
BCNF: 모든 결정자가 후보키.
4NF: 다치 종속(Multi-valued) 제거.
5NF: 조인 종속 제거.

🔴 트랜잭션 (ACID)
Atomicity(원자성): All or Nothing.
Consistency(일관성): 트랜잭션 후에도 DB 규정 유지.
Isolation(격리성): 끼어들기 금지.
Durability(영속성): 결과 영구 저장.

🔴 SQL 핵심 요약
DML: SELECT, INSERT, UPDATE, DELETE.
DDL: CREATE, ALTER, DROP, TRUNCATE.
DCL: GRANT, REVOKE. (WITH GRANT OPTION 주의)
TCL: COMMIT, ROLLBACK, SAVEPOINT.
JOIN: NATURAL JOIN(중복 속성 제거), CROSS JOIN(카테시안 곱).

03. 운영체제 & 네트워크 (계산 지옥)
🔴 OS 스케줄링
비선점: FCFS, SJF, HRN.
선점: RR, SRT, MLQ, MLFQ.

🔴 네트워크 (OSI 7계층 & 프로토콜)
L2(데이터링크): MAC 주소, 스위치. ARP(IP→MAC), RARP(MAC→IP).
L3(네트워크): IP, ICMP(에러메시지), IGMP(멀티캐스트), 라우팅(OSPF, BGP).
L4(전송): TCP(신뢰성, 3-way), UDP(속도). 포트 번호.
L7(응용): HTTP, FTP, DNS(도메인↔IP), SNMP(망 관리).

04. 프로그래밍 (코딩 파트)
🔴 C언어 함정
포인터: *p는 값, &p는 주소. char *p = "Hello";에서 p[1]은 'e'.
증감 연산: ++a는 먼저 더하고 계산, a++는 계산 후 더함.
구조체/공용체: 구조체는 각각 메모리 점유, 공용체는 가장 큰 거 공유.

🔴 Java & Python
Java: extends(상속), implements(인터페이스). super()는 부모 생성자 호출.
Python: range(1, 10, 2) -> [1, 3, 5, 7, 9]. 슬라이싱 a[1:3] -> 인덱스 1부터 2까지.
오버로딩(Overloading): 이름 같음, 파라미터 다름.
오버라이딩(Overriding): 부모꺼 재정의.

05. 애플리케이션 테스트 (QA)
🔴 화이트박스 vs 블랙박스
화이트박스(구조): 기초 경로, 제어 구조, 데이터 흐름 검사.
커버리지: 구문, 결정, 조건, 결정/조건.
블랙박스(기능): 동등 분할, 경계값 분석, 원인-효과 그래프, 오류 예측, 비교 검사.

🔴 통합 테스트
상향식(Bottom-Up): 하위 모듈부터. 드라이버(Driver) 필요.
하향식(Top-Down): 상위 모듈부터. 스텁(Stub) 필요.
V-모델: 단위 - 통합 - 시스템 - 인수 테스트.

06. 보안 & 신기술 (암기 파트)
🔴 암호화 알고리즘
대칭키(Secret): AES, DES, SEED, ARIA. (속도 빠름, 키 관리 힘듦)
비대칭키(Public): RSA, ECC. (속도 느림, 키 관리 쉬움)
해시(Hash): SHA-256, MD5. (복호화 불가능)

🔴 공격 기법
DDoS: 자원 고갈. (TearDrop, Smurfing, Land Attack).
Injection: SQL 쿼리 조작.
XSS: 스크립트 삽입해서 쿠키 탈취.
사회공학: 사람 심리 이용.