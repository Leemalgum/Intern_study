# spring boot
## 9월13일
### @RequiredArgsConstructor
- final, @NotNull 이 붙은 변수들을 가진 생성자를 자동으로 생성해주는 lombok 어노테이션이다. 
또한 변수 선언 시 @Autowired 어노테이션을 사용하지 않아도 된다. 변수 정의에 final 이나 @NotNull이 없을데 사용할 경우
오류가 발생한다.

### @getter/setter  
- lombok 라이브러리가 자동으로 getter/setter 메서드를 생성해서 관리해 주며, 실제로 코드가 보이지 않아 깔끔하다. 
단점으로 getter/setter 메서드가 필요없는 경우에도 자동으로 생성하게 되니 주의해야 한다.

### Bean Validation 2.0이 제공하는 어노테이션
- @PositiveOrZero : 0 또는 양수인지 검사하며 null은 유효하다고 판단한다.
- @Past / @PastOrPresent : 해당 시간이 과거 시간인지 / 현재 또는 과거 시간인지 검사한다. 마찬가지로 null은 유효하다고 판단한다.
- @email : 이메일 주소가 유효한지 검사한다.

### vaild spring boot
- springboot가 @Valid 주석이 달린 인수를 찾으면 자동으로 기본 JSR 380구현인 Hibernate Validator를 부트스트랩하고 인수를 검증한다. 대상 인수가
유효성 검사를 통과하지 못하면 MethodArgumentNotValidException 예외를 throw한다.
- ApiParam
- restcontrolleradvice
- builder.append
- @Repository = ioc 컨테이너에 올리는 법

## 9월14일
### 캡슐화
- 연관있는 속성과 메서드를 하나의 클래스로 묶고, 외부에서 직접 접근하지 못하도록 은닉하여 데이터를 보호하는 것이다.

### 캡슐화의 효과
- 추상화 : 실제 메소드의 동작을 외부에서 이해할 필요가 없고 이를 단순 호출만으로 기능을 실행할 수 있다.
- 재사용성의 향상 : 한 객체에 관련된 속성 및 메소드는 모두 캡슐화의 형태로 제공되어 객체의 모듈성(구성 요소 변경이 용이한 정도)과 응집도(내부 요소들의 연관 정도)가 높아지고 이를 통해 재사용성이 높아진다.
- 위의 두 가지의 이유로 유지보수의 효율성이 향상한다.
- 무결성 보장 : 보통의 캡슐화 코딩이란 변수는 private, 메소드는 public으로 선언하고, 이는 객체의 무결성을 보장한다.

## 9월15일
### Controller
- **사용자의 요청을 어떻게 처리할지 결정**하는 파트이다.
- @Controller, @RestController 어노테이션을 사용한다.
  - @Controller : Model 객체를 만들어 데이터를 담고 View를 찾는 역할이다.
  - @RestController : @Controller + @ResponseBody의 조합으로 RESTful 웹 서비스를 보다 쉽게 개발할 수 있도록 해준다. @Controller와 다르게 단순히 객체만을 반환하고 객체 데이터는 JSON 또는 XML 형식으로 HTTP 응답에 담아서 전송한다.
- @RequestMapping(value="", method=) : Controller에 들어온 요청을 처리하는 기준점이다. 서버의 URL+value로 매핑되며,
최상단 API 경로를 설정한다.

### Service
- **사용자의 요청에 대해 어떤 처리를 할지 결정**하는 파트이다. Controller가 받은 요청에 대해 알맞은 정보를 가공해서 다시
Controller에게 데이터를 넘긴다. 실제 비지니스 로직은 여기서 수행되진 않는다.
- @Service 어노테이션을 사용한다.

### DAO(Data Access Object)
- DB의 data에 접근하기 위한 객체이다. DB에 접근하는 코드는 SQL이기 때문에 자바에서 SQL을 사용하려면 Connection을 생성하고 직접 쿼리문을 작성하여 Connection을 닫는 과정이 필요하다.

### DTO(Data Trasnfer Ojbect)
- **계층 간의 데이터 교환을 위한 Java Bean**을 말하며 VO(Value Object)와 유사하다. 클라이언트가 요청할 양식와 요청을 처리하는 과정에서 기준이 되는 틀을 정의하는 것이다.
  - Java Bean : JavaBean API Specification에 따른 표준이다. 즉 아래 3가지 규칙을 지키는 클래스이다.
      1. 모든 필드는 private이며, getter/setter메서드를 통해서만 접근이 가능하다.
      2. Argument가 없는 기본 생성자를 가진다.
      3. java.io.Serializable 인터페이스를 구현한다.  
      ~~~java
      @ToString
      @Getter
      @Setter
      @NoArgsConstructor
      public class SystemMenuTemp {

          private String MenuCode;
          private byte MenuLevel;
      }
      ~~~
- Springboot는 Presentation Layer(Controller)<->Business Layer(Service)<->Persistence Layer(JDBC, ORM)<->Database(MySQL, MariaDB) 계층 간의 데이터 교환이 이루어진다.

