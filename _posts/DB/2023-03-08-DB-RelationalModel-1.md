---
title: "[DB]관계형 모델(1)"
excerpt: "관계형 모델"

categories:
  - DB
tags:
  - [데이터베이스, 관계형 모델]

toc: true
toc_sticky: true

date: 2023-03-08
---

## 📚관계형 데이터베이스 구조
관계형 모델은 테이블, 컬럼, 기본키-외래키 참조 관계 등으로 현실 관계를 표현합니다. 단순하면서도 직관적인 데이터 표현이 가능하다는 점에서 대다수의 DBMS가 관계형 모델을 사용하고있습니다.

<br>

### 📄릴레이션

  ![릴레이션](/assets/images/DB/img_mysql_table.png)
  <br><br>
  출처: [http://www.tcpschool.com/mysql/mysql_intro_relationalDB](http://www.tcpschool.com/mysql/mysql_intro_relationalDB/)
  <br><br>
  정보를 체계적으로 저장하기 위해 표라는 2차원 데이터 구조를 자주 사용하는데 관계형 모델에서 표와 매우 흡사한 구조를 릴레이션이라고 합니다.
  <br><br>

  * 관계형 모델의 용어와 의미
    - 컬럼: 열에 해당하는 값의 집합(필드, 속성)
    - 레코드: 각 컬럼 순서에 맞게 나열된 값의 집합(행, 투플)
    - 도메인: 컬럼이 가질 수 있는 값의 범위
    - 차수: 릴레이션에 존재하는 컬럼의 수
    - 카디널리티: 릴레이션에 존재하는 레코드의 수
  <br><br>

  * 릴레이션의 특징
    - 레코드의 유일성: 하나의 릴레이션에는 중복되는 레코드가 존재할 수 없습니다.
    - 레코드의 무순서성: 릴레이션에 있는 레코드는 순서가 정해져 있지 않습니다.
    - 컬럼의 무순서성: 릴레이션에 있는 컬럼은 순서가 정해져 있지 않습니다.
    - 컬럼값의 원자성: 컬럼은 분해가 불가능하며 원자적입니다.
  <br><br>
  컬럼의 부분집합은 레코드를 유일하게 식별하는 역할을 하는데 이런 컬럼 또는 컬럼 집합을 **키**라고 합니다.
  
  <br>

  - 키의 특징
    + 유일성: 키 값은 중복될 수 없습니다. 한 개의 키 값은 한 레코드에만 해당됩니다.
    + 최소성: 키는 유일성을 유지하기 위한 최소의 컬럼으로만 구성됩니다.
      <br><br>
    
    릴레이션의 키 중 적어도 한 키에 포함되는 컬럼을 주속성이라고 하고 그렇지 않은 속성을 비주속성이라고 합니다.
    <br><br>
    하나의 릴레이션에서 레코드를 구별할 수 있는 컬럼 집합이 여러개 있을 수 있는데 이런 집합을 **수퍼키**라고 합니다. 수퍼키는 한 개 이상의 컬럼으로 구성될 수 있습니다.
    <br>
    수퍼키 중에서도 최소한의 컬럼으로 구성된 수퍼키를 **후보키**라고 합니다
    <br>
    레코드를 구분하기 위해 지정한 후보키 중 하나를 **기본키**라고 합니다.
    <br>
    외래키나 일반 컬럼은 널 값을 가질 수 있지만키는 널 값을 가질 수 없습니다.

<br><br><br>

### 📄릴레이션 스키마
  - 릴레이션 스키마
  <br>
  테이블에서 사용되는 컬럼과 컬럼이 지니는 데이터 타입을 정의한 것을 의미합니다. 일반적으로 릴레이션 스키마는 잘 변하지 않습니다.

  <br>

  - 릴레이션 인스턴스
  <br>
  변수에 저장되어있는 값과 유사합니다. 시간이 지나면서 변할 수 있는 값들입니다.

<br><br><br>
  
### 📄관계형 모델의 제약조건
릴레이션의 모든 인스턴스들이 만족해야하는 조건입니다.

- 영역 제약조건: 특정 컬럼이 가질 수 있는 값은 도메인에 포함되며 원자적이어야하는 조건
- 키 제약조건: 레코드를 구별하기 위해 특정 컬럼의 값들이 릴레이션 내부의 레코드를 고유하게 식별할 수 있어야한다는 조건
- 개체 무결성 제약조건: 기본키 값으로 널(NULL) 값을 저장할 수 없다는 조건
- 참조 무경성 제약조건: 한 릴레이션에 있는 레코드가 다른 릴레이션의 레코드를 참조하려면 반드시 참조되는 레코드가 해당 릴레이션 안에 있어야 한다는 조건

  <br><br>