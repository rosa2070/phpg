# Database
- 종류
    * 텍스트 기반 데이터베이스 .csv .tsv, .md
        - text기반 파일형
        - 장점: 가볍다 *, 제작이 쉽다, 검색이 쉽다
        - 단점: 중복제어가 어렵다,불필요한 데이터가 많아진다.
        - 시스템
            - 계층형 데이터베이스 .md
                - 나열형 csv
            - 네트워크형: 파일별 키값 도입으로 네트워크적 트리를 구성
            
    * RDBMS(Relational DataBase Management System)
        - 키기반의 연결형 데이터 베이스
        - 장점: 키기반으로 불필요한 데이터를 줄일수 있다. 연결형 데이터로 데이터간 관계분석
        - 단점: 데이터 비용이 높다. 데이터 복구에 많은 자원 필요
        - 시스템
            - Oracle *
            - MS-SQL
            - MySQL *
            - SQlite *
            - PostGre
            - Sybase
            - Cubrid -네이버
    * NoSQL
        - 검색시장의 발달로 빅데이터 형성에 따른 데이터 가치 감소
        - 데이터 입력 비용이 낮은 데이터 베이스 필요
        - 관계형과 텍스트데이터 베이스의 중간형
        - 키:밸류 로 이어진 텍스트 기반의 데이터 베이스
        - 장점: 검색이 빠르다, 가볍다
        - 단점: 중복제어가 어렵다, 데이터 보관의 역할 증대
        - 시스템
            - Mongo
            - Couch
            - 빅데이터/분석
                - 하둡, Hbase, Spark
                - Casandra
- 시스템 (데이터가 다양한 대기업 기준)
    - 날데이터 RAWDATA
    - 수집 : DataLake 데이터 호수
        - RDBMS * 
        - NoSQL * 검색을 위한 서브DB 활용
        - text파일(로그*,csv,tsv,) *
    - 통합
        - HADOOP File System(HDFS)->BigData
        - 파이썬으로 가져오기 어려움 ->PySpark * ->ML
        - SPARK(메모리기반 데이터 저장)-> Caffe ML
    - 검색 쉽게 변형(DW: DataWareHouse 데이터창고) SQL
        - RedShift => Bigdata 분석
        - python ML/DL

- RDBMS 조건
    - 구조와 제약조건을 만족: Schema
    - Schema 3계층
        - 외부 스키마 : 사용자가 직접 DB를 접속하여 접속된 정보의 데이터 스키마
            - DB 전문가/프로그래머/분석가
        - 개념 스키마 : 사용자 테이블간의 릴레이션된 관계등의 제약조건이 달린 스키마
            - DB 아키텍쳐
                - 보안 : 내외부 접근 허용및 포트사용
                - 접근성 : 접근 가능자와 권한
                - 무결성: 무결성 제약 조건
                    - 삭제 이상 Delete Anormaly
                    - 삽입 이상 insert Anormaly
                    - 갱신 이상 update Anormaly
                - 정규화 작업을 통해 해결
                    - 무결성 이상현상 제거
                    - 데이터 저장공간 줄이기
                    - 자료가 불일치성 줄이기
                    - 구조적 안정화
        - 내부 스키마 : 내부적으로 정의된 DB의 구성 제약 mysql infomation_schema
            - DB 엔지니어
                - DB 튜닝

- 정규화 
    - 1NF :원자화 중복성
        * 중복금지조항 - > 도메인(입력값)은 원자(성질을 유지하되 더이상 쪼개지지 않는)값으로 되어있어야 한다.

* 기초테이블

|id|name|subject|
|---|---|---|
|1|홍길동|국어,수학|
|2|박문수|국어|
|2|박문수|국어|

* 원자화/ 중복제거

|id|name|sub1|sub2|
|---|---|---|---|
|1|홍길동|국어|수학|
|2|박문수|국어||

    - 2NF : 테이블에서의 이상현상
        * 부분함수 종속성(각각의 테이블에서 이상현상) 제거
* user ->subject

|id|name|sub1|
|---|---|---|
|1|홍길동|1|
|1|홍길동|2|
|2|박문수|1|

*subject

|id|name|
|---|---|
|1|국어|
|1|수학|

* 2nf 처리 user->ttable->subject

* user

|id|name|
|---|---|
|1|홍길동|
|2|박문수|

* ttable

|uid|sid|uname|
|---|---|---|
|1|1|홍길동|
|1|2|홍길도|
|2|1|박문수|

    - 3NF : 이행함수 종속성 해결 x(user)->y(ttable):중복이름이 있으면 안됨->z(subject)
        - 반드시 키값에 의해서만 다음 속성을 정의할수 있다.

* user

|id|name|
|---|---|
|1|홍길도|
|2|박문수|

* ttable

|uid|sid|
|---|---|
|1|1|
|1|2|
|2|1|

*subject

|id|name|teacher|
|---|---|---|
|1|국어|김교수|
|2|수학|허교수|
|3|과학|김교수|

    - BCNF 3Nf 의 강화버전
        - 후보키가 고유해야한다.

*subject : 과목당 교수는 중복해서 가르칠수 없다라고 했을 경우 후보키로 교수키가 unique 하게 됨

|id|name|tid:unique|
|---|---|---|
|1|국어|1|
|2|수학|2|
|3|과학|3|

* teacher

|id|name|
|---|---|
|1|김교수|
|2|허교수|
|3|박교수|

* 무결성
    - 개체 무결성
        - 모든 데이터는 기본키를 가져야 하고 기본키는 중복이나 NULL 가져서는안된다.
    - 참조 무결성
        - 참조의 일관성이 있어야한다. A->B 를 참조하고 있는경우 A가 삭제 되면 B도 같이 삭제되어야한다.
        - AA->B, AB->B 인경우 AA가 삭제됬다고 B를 삭제해서는 안된다. 둘다 삭제되면 안된다.
    - 도메인 무결성
        - 후보키중 unique 한경우 NULL 값이어서는 안된다.
    - 통합 무결성
        - 데이터 통합하였을때 결함이 있으면 안된다.( 모든 제약사항을 지켜야 한다.)

* 데이터 아키텍쳐
    - 배경 : IOT
    - 광의 : 데이터 생성 -> 저장 -> 보관  -> 안전 데이터 라이프 사이클
    - 협의 : 데이터 베이스 설계
    - 핵심 : 분산처리 -> 뇌가 복잡하지 않게 잘 처리하자

    - 데이터 모델의 종류
        - 개념모델 : 유스케이스*
            - 테이블 : 엔터티 클래스 -> 비지니스 목적에 맞는 객체
            - 액션: 관계
            - 관계에 따른 제약사항
            - 무결성

        - 논리모델 : 액티비티*
            - 컬럼(도메인)의 성격
            - 도메인의 관계성
            - 데이터 무결성
            - 시퀀스 UML*

        - 물리모델 : 데이터서버
            - RDBMS
                - Mysql
                - Oracle
    
    - 상호 영향 아키텍처
        - 비지니스 아키텍쳐 <-> 데이터아키텍처
        - 어플리케이션 아키텍처 => UX/UI
        - 기술 아키텍처 => JAV -> node+k8s
        - 데이터 아키텍처 
    
    - 데이터 아키텍쳐 시스템
        - 데이터 원천 -> 데이터수집
        - 데이터 레이크(DL:Data Lake)
            - 데이터의 종합
            - hadoop
                -> spark
            - M/L -> 차원축소 -> 정리저장 
        - 데이터 웨어하우스(DW)
            - 찾기 쉽게 만든 중앙집중 저장소
            - AWS: redshift
        - 데이터 마트
            - DW의 집중버전
            - 부서나 사업부별 필요데이터를 세트화 해서 관리
            - 즉시 사용을 통한 비지니스 역량 강화

    - 데이터 아키텍쳐 유형
        - 데이터 패브릭 = 데이터마트+외부데이터 
            - 데이터를 가공 분류 데이터솔루션으로 지원
            - 머신러닝등 각종 데이터 기법을 통해 고객에게 인사이트나 정리된 자료제공
            - 의사결정 지원

        - 데이터 메쉬: 안정성 권한배분을 통한 효율성
            - 데이터 분산처리를 통한 위험감소및 효율성 높임
            - 탈 중앙화형 데이터 위임처리
    
    - 데이터 아키텍처의 장점
        - 데이터 중복 감소
        - 데이터 품질향상
        - 효율적 통합 지원( 데이터 필요자 )
        - 데이터 라이프 사이클 관리를 통한 데이터 변화 도출

    - 데이터 아키텍처 UML
        - 아키텍쳐 설계도 
        - ERD Entity Relationship Diagram 
        - 데이터 모델(ERD) 다이어그램
        - 구성요소
            - 개체: Entity
                - 데이터 움직임의 기본틀
                - 관리정보의 실체
            - 속성: Attribute
                - 엔터티 구성요소
                - 엔터티의 성질
            - 관계: Relationship
                - 엔터티간의 관계 -> 행동을 한다 -> 데이터를 전달한다
                - 1:1
                - 1:다
                - 다:1
                - 다:다









