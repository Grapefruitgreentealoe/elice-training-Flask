## 목차
#### 1. 관계형데이터베이스 
#### 2.RDB와 Flask의 상호작용 
#### 3. 간단한 게시판 만들기 
#### 4.Flask JWT

## 수강 목표
- 데이터베이스의 종류를 안다. 
- Flask에서 DB가 하는 역할을 이해하고, Database를 사용해서 서비스를 작성할 수 있습니다. 
- JWT의 개념을 이해하고, 사용하는 방법과 이유를 설명할 수 있습니다

### 1. 관계형데이터베이스 

##### 데이터베이스
    데이터 베이스는 관계형 데이터베이스, NoSQL로 나누어져 있다.

##### 관계형 데이터베이스(RDB)
    :키와 값들의 간단한 관계를 테이블화 시킨 데이터베이스

##### RDB의 특징
    DML을 사용하여 데이터 간 결합,
    제약조건 등의 설정을 통해 데이터를 추출할 수 있다. 
    테이블간의 데이터 관계를 설정할 수 있다.     

##### RDB의 형태
|id|name|phone|address|birth|age|
|-|-|-|-|-|-|
|1|1|1|1|1|1|
|2|2|2|2|2|2|
|3|3|3|3|3|3|
|4|4|4|4|4|4|

- RDB는 정형화된 데이터를 저장하고 있습니다.(다른 형태의 데이터가 들어올 수 없습니다)
- 각 칼럼(세로줄)마다 데이터의 형태가 동일합니다.
- SQL 질의어(SQL 쿼리)를 사용합니다.


### 2.RDB와 Flask의 상호작용

#### RDB와 Flask
파이썬은 오픈소스와 상용 데이터베이스에 대한 대부분의 데이터베이스 엔진을 위한 패키지를 가지고 있습니다. 
Flask에서 입력받은 내용을 DB에 저장할 수 있습니다. → 효율적인 데이터관리 가능

(person<->Webbrowser) ->http/

JWT<-(Flask->Python object/
<- SQLAlchemy->SQL statement/
<- MySQL)

### 3. 간단한 게시판 만들기

#### 구현 사항

데이터베이스에 저장되는 데이터를 활용해서 사용자를 <u>검색</u>해 봅니다.
 데이터베이스에 저장되는 데이터를 활용해서 사용자를 <u>추가</u>해 봅니다. 
 단, <u>중복 사용자</u>를 방지합니다. 
 게시판 내용을 <u>생성, 조회, 수정, 삭제</u>해봅니다.

#### 게시판 등록
#####게시판의 기능을 DB에 적용하기 위해서는 리소스를 다뤄야 합니다.
- 아이템 리소스를 데이터베이스에 쓰기(Create)
- 데이터베이스에서 아이템 리소스 검색(Read)
- 데이터베이스에서 아이템 리소스 수정(Update)
- 데이터베이스에서 아이템 리소스 삭제(Delete)

### 4. Flask JWT

##### JWT(JSON Web Token)란?
웹 표준(RFC 7519)으로서 두 개체에서 JSON 객체를 사용하여 통신합니다.
-JSON 포맷을 이용하여 사용자에 대한 속성을 저장하는 Web Token
-토큰 자체를 정보로 사용하는 Self-Contained 방식으로 정보를 안정하게 전달

##### JWT의 생김새
|header.|payload.|signature|
|-|-|-|
- header : 토큰의 알고리즘 저장
- payload : 토큰에 담을 정보 넣음
- signature : 헤더와 정보의 인코딩 값들과 관련된 비밀키가 들어있음.

##### JWT의 구조
- JWT는 header, payload, signature의 3가지로 이루어지며, json 형태인 각 부분은 base64로 인코딩되어 표현.
- 각각의 부분을 이어주기 위해 . 구분자를 사용하여 구분.
- Base 64는 암호화된 문자열이 아니고 동일한 문자열에 대해 항상 같은 인코딩 문자열 반환.

##### Header
     토큰의 헤더는 typ과 alg 총 두가지 정보로 구성
     {"typ" : "JWT", "alg" : "HS256}



##### Payload
- 토큰의 Payload에는 토큰에서 사용할 정보의 조각들인 <u>Claim</u>이 담겨있다.
- 클래임은 총 3가지로 나누어지며, JSON 형태로 다수의 정소를 넣을 수 있다.

###### 1)등록된 클래임
: 토큰 정보를 표현하기 위해 이미 정해진 종류의 데이터이다. 모두 선택적으로 작성이 가능하며 사용하는 것을 권장.

###### 2)공개된 클래임
: 충돌이 방지된 이름을 가지고 있어야한다. 충돌을 방지하기 위해 클레임 이름을 URI 형식으로 짓는다.
> {https://elice.io : true}

###### 3) 비공개 클래임
: 등록과 공개를 제외한 클래임이자, 사용자 정의 클레임으로 서버와 클라이언트 협의로 사용되는 클레임.
<strong>서버와 클라이언 사이에 임의로 지정한 정보 저장</strong>, 이 클레임은 공개 클레임과 달리 이름이 중복되어 충돌될 수 있으니 유의할 것.
>  {"studend_name" : "elice"}

##### Signature
 토큰을 인코딩하거나 유효성 검증을 할 때 사옹하는 고유한 암호화 코드.
서명은 헤더의 인코딩값과 정보의 인코딩 값을 합친 후 주어진 비밀키로 해시를 하여 생성.


 

