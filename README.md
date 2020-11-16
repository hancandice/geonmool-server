**6:33:05 / Pagination**

# geonmool-server

## ORM이란

Object Relational Mapping, 객체-관계 매핑

객체와 관계형 데이터베이스의 데이터를 자동으로 매핑(연결)해주는 것을 말한다.
객체 지향 프로그래밍은 **클래스**를 사용하고, 관계형 데이터베이스는 **테이블**을 사용한다.
객체 모델과 관계형 모델 간에 불일치가 존재한다.
**ORM을 통해 객체 간의 관계를 바탕으로 SQL을 자동으로 생성하여 불일치를 해결한다.**
데이터베이스 데이터 <—매핑—> Object 필드
객체를 통해 간접적으로 데이터베이스 데이터를 다룬다.
Persistant API라고도 할 수 있다.
Ex) JPA, Hibernate 등
https://gmlwjd9405.github.io/2019/02/01/orm.html

## ORM의 장단점

- 장점

  객체 지향적인 코드로 인해 더 직관적이고 비즈니스 로직에 더 집중할 수 있게 도와준다.
  ORM을 이용하면 SQL Query가 아닌 직관적인 코드(메서드)로 데이터를 조작할 수 있어 개발자가 객체 모델로 프로그래밍하는 데 집중할 수 있도록 도와준다.
  선언문, 할당, 종료 같은 부수적인 코드가 없거나 급격히 줄어든다.
  각종 객체에 대한 코드를 별도로 작성하기 때문에 코드의 가독성을 올려준다.
  SQL의 절차적이고 순차적인 접근이 아닌 객체 지향적인 접근으로 인해 생산성이 증가한다.
  재사용 및 유지보수의 편리성이 증가한다.
  ORM은 독립적으로 작성되어있고, 해당 객체들을 재활용 할 수 있다.
  때문에 모델에서 가공된 데이터를 컨트롤러에 의해 뷰와 합쳐지는 형태로 디자인 패턴을 견고하게 다지는데 유리하다.
  매핑정보가 명확하여, ERD(Entity-relationship model)를 보는 것에 대한 의존도를 낮출 수 있다.
  DBMS​(Database Management System)에 대한 종속성이 줄어든다.
  객체 간의 관계를 바탕으로 SQL을 자동으로 생성하기 때문에 RDBMS의 데이터 구조와 Java의 객체지향 모델 사이의 간격을 좁힐 수 있다.
  대부분 ORM 솔루션은 DB에 종속적이지 않다.
  종속적이지 않다는것은 구현 방법 뿐만아니라 많은 솔루션에서 자료형 타입까지 유효하다.
  프로그래머는 Object에 집중함으로 극단적으로 DBMS를 교체하는 거대한 작업에도 비교적 적은 리스크와 시간이 소요된다.
  또한 자바에서 가공할경우 equals, hashCode의 오버라이드 같은 자바의 기능을 이용할 수 있고, 간결하고 빠른 가공이 가능하다.

- 단점

  완벽한 ORM 으로만 서비스를 구현하기가 어렵다.
  사용하기는 편하지만 설계는 매우 신중하게 해야한다.
  프로젝트의 복잡성이 커질 경우 난이도 또한 올라갈 수 있다.
  **잘못 구현된 경우에 속도 저하 및 심각할 경우 일관성이 무너지는 문제점**이 생길 수 있다.
  일부 자주 사용되는 대형 쿼리는 속도를 위해 SP를 쓰는등 별도의 튜닝이 필요한 경우가 있다.
  DBMS의 고유 기능을 이용하기 어렵다. (하지만 이건 단점으로만 볼 수 없다 : 특정 DBMS의 고유기능을 이용하면 이식성이 저하된다.)
  procedure가 많은 시스템에선 ORM의 객체 지향적인 장점을 활용하기 어렵다.
  이미 procedure가 많은 시스템에선 다시 객체로 바꿔야하며, 그 과정에서 생산성 저하나 리스크가 많이 발생할 수 있다.
  https://gmlwjd9405.github.io/2019/02/01/orm.html

## Cookie와 Session

### Cookie

Cookie는 웹서버가 브라우저를 통해 클라이언트에 일시적으로 데이터를 저장하는 방식이다.

Cookie를 이용하면 다음과 같은 과정으로 매 접속마다 재인증을 피할 수 있다.

클라이언트에서 서버로 최초의 요청을 보낸다.
서버에서는 응답을 보낼 때 Cookie값을 저장하고 이를 응답 헤더에 넣어 보낸다.
클라이언트에서는 응답 헤더에 있는 Cookie정보를 브라우저에 저장한다.
이후 클라이언트에서는 요청을 보낼 때 해당 Cookie 정보를 같이 담아 서버로 보낸다. 이를 통해 서버에서는 인증을 완료한 사용자를 구분할 수 있게 된다.
쿠키는 클라이언트(브라우저)에 위에서 말했듯이 세션에 비해 보안에 취약하다. 따라서 아이디와 비밀번호를 쿠키에 저장하는 것은 치명적일 수 있다.

### Session

Session은 Cookie를 기반으로 하고 있지만 Cookie와 다르게 상태를 서버에 저장한다.

서버에서는 클라이언트를 구분하기 위해 각각의 클라이언트에 Session ID를 부여한다. 클라이언트가 서버에 접속해서 브라우저를 종료할 때까지 인증상태를 유지하게 된다.

서버에 사용자 정보를 저장하기 때문에 Cookie보다 보안에 좋지만 사용자가 많아지게 되면 서버에 부하를 줄 수 있다.
접속 시간에 일반적으로 제한을 두기 때문에 일정 시간 클라이언트로부터 요청이 오지 않는다면 Session을 만료시킨다. 이를 통해 부하를 줄일 수는 있지만 동시접속자가 많은 경우라면 서버 메모리를 많이 차지하기 때문에 문제가 될 수 있다.

Cookie에는 SessionID(우리가 Dev Tools를 통해 흔히 볼 수 있는 JSessionID)만 저장하고 이를 이용해 참조된 사용자 정보를 사용하는 것이 방법이 Cookie-Based Session이다.

## Redis를 이용한 Session 관리

Redis는 **Remote Dictionary Server**의 약자로서 'key-value' 구조의 비관계형 데이터를 저장하고 관리하기 위한 NoSQL의 일종이다.

휘발성 데이터를 저장하는 용도로 사용되며 디스크 기반이 아닌 메모리 기반의 데이터 저장소다.

명시적으로 삭제나 만료를 설정하지 않으면 데이터는 삭제되지 않는다. 하지만 메모리를 사용하기 때문에 안전한 데이터의 보관을 위해 백업을 권장한다. 다른 서버의 메모리를 사용하거나 디스크에 데이터를 저장하는 방법을 통해 데이터를 백업할 수 있다.

Redis를 이용하여 Session을 관리하는 이유은 Session의 영속적 관리와 복수 서버 환경에서의 Session 공유다.

Redis를 사용하면 프로세스가 종료되어도 Session 정보를 보존할 수 있다.

복수 서버 환경에서는 Session Clustering을 통해 Session을 서버마다 공유하는 방법이 있다.

하지만 Redis를 사용하면 Session을 Redis에서 관리하기 때문에 Session Clustering 없이도 복수 서버 환경에서 세션을 공유할 수 있게 된다.

## Redis를 이용한 Session 관리까지 살펴보았는데 최근에는 클라이언트와 서버 간에 상태 공유를 위해 Token을 기반으로 한 방식도 많이 사용되고 있다.

클라이언트에서 서버에 요청을 보낼 때마다 토큰을 전달하고 해당 토큰이 유효한지 검증하여 처리하는 방식이다.

해당 방식의 장점은 서버측에서는 사용자의 세션을 유지 할 필요가 없다는 것이다. 즉, 사용자의 요청이 들어오면 서버 측에서는 토큰의 유효성만 확인하면 되기 때문에 서버 자원을 아낄 수 있게 된다. 대표적인 방식으로는 **JWT(JSON Web Token)**가 있다.

## SESSION

req.session.userId = user.id
{userId:1} -> send that to redis
sess:qijdfljaslkdjfie -> {userId:1}
