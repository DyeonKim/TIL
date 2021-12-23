# REST 통신의 이해와 구현을 위한 참고자료
 - 이해 : [REST 통신이란?](https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html)
 - 구현 : [Python 을 이용한 REST 통신 구현](https://twpower.github.io/124-python-requests-usage)
 - 구현 : [Java 를 이용한 REST 통신 구현](https://zoomkoding.github.io/codingtest/java/2019/09/20/REST-JSON.html)
 - 구현 : [Curl 을 이용한 REST 통신](https://www.lesstif.com/pages/viewpage.action?pageId=14745703)

<hr/>

## 이해
### REST의 개념
"Representational State Transfer" 의 약자<br/>
자원을 **이름**(_자원의 표현_)으로 구분하여 해당 자원의 **상태**(_정보_)를 주고받는 모든 것을 의미<br/>
자원의 표현에 의한 상태 전달
 - 자원의 표현
   - 자원<br/>
     해당 소프트웨어가 관리하는 모든 것<br/>
     _문서, 그림, 데이터, 해당 소프트웨어 자체 등_
   - 자원의 표현<br/>
     그 자원을 표현하기 위한 이름<br/>
     _자원이 DB의 학생 정보라면 자원의 표현은 'students'로 정한다._
 - 상태 전달
   - 데이터가 요청되어지는 시점에서 자원의 상태(_정보_)를 전달
   - JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적.<br/>
     `불필요한 태그를 줄인 JSON이 보편적으로 사용된다.`

웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 **웹의 장점을 최대한 활용할 수 있는 아키텍쳐 스타일**이다.<br/>
네트워크 상에서 Client와 Server 사이의 통신 방식 중 하나  

<br/>

HTTP URI를 통해 자원을 명시하고 HTTP MEthod를 통해 해당 자원에 대한 CRUD Operation을 적용<br/>
자원 기반의 구조(ROA, Resource Oriented Architecture) 설계의 중심에 자원이 있고 HTTP Method를 통해 자원을 처리하도록 설계된 아키텍쳐
|    | CRUD Operation | HTTP Method |
| -- | -------------- | ----------- |
| 생성 | Create | POST |
| 조회 | Read | GET |
| 수정 | Update | PUT |
| 삭제 | Delete | DELETE |
| 정보 조회 | Head | HEAD |

<br/><br/>

### REST의 장단점
장점
 - HTTP 프로토콜의 인프라를 그대로 사용하므로 HTTP API 사용을 위한 별도읜 인프라를 구축할 필요가 없다.<br/>
 - HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용 가능하다.
 - Hypermedia API의 기본을 충실히 지키면서 **범용성을 보장**한다.
 - 의도하는 바를 쉽게 파악할 수 잇다.
 - Server와 Cleint의 역할을 명확하게 구분한다.

단점
 - 표준이 존재하지 않는다.

<br/><br/>

### REST가 필요한 이유
 - 애플리케이션 분리 및 통합
 - 다양한 클라이언트의 등장
 - 멀티 플랫폼(Web, iOS, AOS 등)에 대한 지원에 효과적

<br/><br/>

### REST 구성 요소
1. 자원(Resource)<br/>
   - 모든 (Server에 존재하는)자원에 고유한 ID가 존재
   - URI(Uniform REsource Identifier) : '/groups/:group_id'
   - Client는 URI를 이용해서 자원을 지정, 해당 자원의 상태에 대한 조작을 Server에 요청한다.
2. 행위(Verb)
   - HTTP Method를 사용
   - GET, POST, PUT, DELETE와 같은 메서드를 제공
3. 표현(Representation of Resource)
   - Client가 자원의 상태에 대한 조작을 요청하면 Server는 이에 적절한 응답(Representation)을 보낸다.
   - JSON, XML, TEXT, PSS 등 여러 형태의 응답으로 나타내어 질 수 있다ㅏ.
   - JSON, XML이 일반적

<br/><br/>

### REST의 특징
1. Server - Client 구조<br/>
   서로 간 의존성이 줄어든다.
   - Server<br/>
     자원이 있는 쪽
     API를 제공하고 비즈니스 로직 처리 및 저장을 책임진다.
   - Client<br/>
     사용자 인증이나 context(세션, 로그인 정보) 등을 직접 관리하고 책임진다.
<br/>

2. Stateless (무상태)
   - HTTP 프로토콜은 Stateless Protocol이므로 REST 역시 무상태성을 갖는다.
     - Client의 context를 Server에 저장하지 않는다.
       - Session과 Cookie같은 context 정보를 신경쓰지 않아도 되므로 구현이 단순해진다.
     - Server는 각각의 요청을 완전히 별개의 것으로 인식하고 처리한다.
       - 이전 요청이 다음 요청의 처리에 연관되어서는 안된다.
       - 이전 요청이 DB를 수정하여 DB에 의해 바뀌는 것은 허용한다.
       - Server의 처리 방식에 일관성을 부여하고 부담이 줄어들며, 서비스의 자유도가 높아진다.
<br/>

3. Cacheable (캐시 처리 가능)
   - 웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용할 수 있다.
     - 캐싱 기능 적용 가능
     - Last-Modified나 E-Tag를 이용하면 캐싱 구현이 가능
   - 대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다.
   - 캐시 사용을 통해 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있다.
<br/>

4. LayeredSystem (계층화)
   - API Server는 순수 비즈니스 로직을 수행하고 그 앞단에 보안, 로드밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의 유연성을 줄 수 있다.<br/>
     로드밸런싱, 공유 캐시 등을 통해 확장성과 보안성을 향상시킬 수 있다.
   - PROXY, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있다.
<br/>

5. Code-On-Demand
   - Server로부터 스크립트를 받아서 Client에서 실행한다.
   - 반드시 충족할 필요는 없다.
<br/>

6. Uniform Interface (인터페이스 일관성)
   - URI로 지정한 Resource에 대한 조직을 통일되고 한정적인 인터페이스로 수행한다.
   - 특정 언어나 기술에 종속되지 않는다.
<br/>

### REST API의 개념
**API(Application Programming Interface)란?**
   - 식당의 메뉴판과 같은 것.
   > 메뉴판의 역할<br/>
     손님(Client)과 주방(Server) 사이에 요리(정보) 교환이 가능하도록 하는 것

REST API<br/>
 : REST 기반으로 서비스 API를 구현한 것.

<br/><br/>

### REST API 특징
 - HTTP를 지원하는 프로그램 언어로 Client, Server를 구현할 수 있다.
 - 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있다.

<br/><br/>

### REST API 설계 규칙
> 도큐먼트 : 객체 인스턴스, 데이터베이스 레코드와 유사한 개념<br/>
  컬렉션 : 서버에서 관리하는 디렉터리라는 리소스<br/>
  스토어 : 클라이언트에서 관리하는 리소스 저장소<br/>

1. URI는 정보의 자원을 표현해야한다.
    - 명사 사용. 대문자보다는 소문자 사용
       - 도큐먼트 이름 : 단수 명사
       - 컬렉션 이름 : 복수 명사
       - 스토어 이름 : 복수 명사
2. 자원에 대한 행위는 HTTP Method로 표현한다.
    - URI에 HTTP Method가 들어가면 안된다.<br/>
      `GET /members/delete/1` (X)
    - URI에 행위에 대한 동사 표현이 들어가면 안된다.<br/>
      (CRUD 기능을 나타내는 것은 URI에 사용하지 않는다.)<br/>
      `GET /members/show/1` (X) -> `GET /members/1` (O)
    - 경로 부분 중 변하는 부분은 유일한 값으로 대체한다.<br/>
      id는 하나의 특정 resource를 나타내는 고유값
3. 슬래시 구분자(/)는 계층 관계를 나타내는데 사용한다.
4. URI 마지막 문자로 슬래시(/)를 포함하지 않는다.
   - REST API는 분명한 URI르 만들어 통신을 해야하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/)를 사용하지 않는다.
5. 하이픈(-)은 URI 가독성을 높이는 데 사용한다.
6. 밑줄(_)은 URI에 사용하지 않는다.
7. URI경로에는 소문자가 적합하다.
   RFC3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문
8. 파일 확장자는 URI에 포함하지 않는다.
   - Accept header를 사용한다.<br/>
     `http://restapi.example.com/members/soccer/345/photo.jpg` (X)<br/>
     `GET / members/soccer/345/photo HTTP/1.1 Host: restapi.example.com Accept: imgae/jpg` (X)
9. 리소스 간에는 연관 관계가 있는 경우<br/>
   `/리소스명/리소스ID/관계가 있는 다른 리소스명`<br/>
   예) `GET : /users/{userid}/devices`(일반적으로 소유 'has'의 관계를 표현할 때)

<br/>

> 응답 상태 코드<br/>
  1XX : 전송 프로토콜 수준의 정보 교환<br/>
  2XX : 클라이언트 요청이 성공적으로 수행됨<br/>
  3XX : 클라이언트는 요청을 완료하기 위해 추가적인 행동을 취해야 함.<br/>
  4XX : 클라이언트의 잘못된 요청<br/>
  5XX : 서버쪽 오류로 인한 상태코드<br/>


### RESTful 개념
**RESTful이란?**
REST라는 아키텍쳐를 구현하는 웹 서비스를 나타내기 위해 사용되는 용어
REST API를 제공하는 웹 서비스를 RESTful 하다고 할 수 있다.
REST 원리를 따르는 시스템은 RESTful이란 용어로 지칭된다.

### RESTful의 목적
- 이해하기 쉽고 사용하기 쉬운 REST API를 만드는 것
- 일관적인 컨벤션을 통한 API의 이해도 및 호환성을 높이는 것이 주 동기
- 성능이 중요한 상황에서는 굳이 RESTful한 API를 구현할 필요는 없다.

### RESTful 하지 못한 경우
 - CRUD 기능을 모두 POST로만 처리하는 API
 - route에 resource, id 외의 정보가 들어가는 경우

<br/><br/>
