# spring boot
<details>
    <summary>목차</summary>
 
- [9월13일](#9월13일)
  * [@RequiredArgsConstructor](#@RequiredArgsConstructor)
  * [@getter/setter](#@getter/setter)
  * [Bean Validation 2.0이 제공하는 어노테이션](#Bean-Validation-2.0이-제공하는-어노테이션])
  * [vaild spring boot](#vaild-spring-boot)
  * [Swagger 어노테이션](#Swagger-어노테이션)
  * [@RestControllerAdvice](#@RestControllerAdvice)
  * [builder.append](#builder.append)
- [9월14일](#9월14일)
  * [캡슐화](#캡슐화)
  * [캡슐화의 효과](#캡슐화의-효과)
- [9월15일](#9월15일)
  * [Controller](#Controller)
  * [Service](#Service)
  * [DAO(Data Access Object)](#DAO(Data-Access-Object))
  * [DTO(Data Trasnfer Ojbect)](#DTO(Data-Trasnfer-Ojbect))

</details>

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

### Swagger 어노테이션
- @Api : 클래스를 Swagger 리소스 대상으로 표시
- @ApiOperation : 요청 URL에 매핑된 API에 대한 설명
- @ApiParam : 요청 파라미터에 대한 설명 및 필수여부, 예제값 설정
- @ApiResponse : 응답에 대한 설명

### @RestControllerAdvice
- @ControllerAdvice : @ExceptionHandler, @ModelAttribute, @InitBinder가 적용된 메서드들을 AOP를 적용해 Controller 단에 적용하기 위해 고안된 어노테이션이다. 클래스에 선언하면 되고, 모든 @Controller에 대한 전역적으로 발생할 수 있는 예외를 잡아서 처리할 수 있다.
- @RestControllerAdvice : @ResponseBody + @ControllerAdvice를 합친 어노테이션이다. @ControllerAdvice와 동일한 역할을 수행하고, 추가적으로 @ResponseBody를 통해 객체를 리턴할 수 있다.
- 단순 예외 처리만 한다면 @ControllerAdvicef를 사용하고, 응답 시 객체를 리턴해야 한다면 @RestControllerAdvice를 사용하면 된다.

### builder.append
- String 클래스 오브젝트의 문자열은 + 연산자를 사용해 문자열을 결합한다. String 클래스는 고정 길이로 되어있기 때문에 한 번 작성한 문자열 뒤에 문자를 추가하게 되면 새로운 문자열을 작성한다. 반면 StringBuilder 클래스는 가변길이의 문자열을 사용하기 때문에 문자를 추가해도 새로운 문자열을 작성하지 않고 문자열에 추가만 한다.
- string + string : + 연산자를 사용해 문자열을 결합하면 매번 새로운 String 객체가 생성되고 이전의 문자열 객체는 가비지 값이 된다. 즉 메모리를 낭비하게 된다.
- StringBuilder.Append(string) : StringBuilder는 문자열 생성을 도와주는 클래스로 Append 함수를 사용해 문자열을 이어붙인다. 위와 다르게 결합할 때 마다 새로운 String 객체를 생성하지 않아 메모리 낭비를 방지할 수 있다.

### @Repository 
- @Repository 어노테이션을 사용한 클래스는 IoC 컨테이너에 빈(Bean) 객체로 생성해준다.
    - IoC(Inversion of Control) : 제어권의 역전이란 객체의 생성, 생명 주기의 관리까지 모든 객체에 대한 제어권이 바뀌었다는 것을 의미한다.
    - IoC 컨테이너 : 
        1. 객체의 생성을 책임지고 의존성을 관리한다. 
        2. POJO의 생성/초기화/서비스/소멸에 대한 권한을 가진다.
        3. 개발자들이 직접 POJO를 생성할 수 있지만 컨테이너에게 맡긴다.
    - IoC의 분류 : 
        - DL(Dependency Lookup) :  저장소에 저장되어 있는 Bean에 접근하기 위해 컨테이너가 제공하는 API를 이용하여 Bean을 Lookup 하는 것이다.
        - DI(Dependency Injection) : 각 클래스 간의 의존 관계를 Bean Definition 정보를 바탕으로 컨테이너가 자동을 연결해주는 것이다.

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

## 9월16일
- 코드에서 객체를 만들고 그것을 서버에 올리는 것이 인스턴스화이다.
- @Resource는 마이바티스에서 제공하는 어노테이션으로 name 속성 사용시 소문자로 시작해야 한다.
- spring boot JMeter : Apache에서 java로 만든 웹 어플리케이션 성능 테스트 오픈 소스이다.

### ioc 제어권의 역전
- 주로 의존성에 대한 제어권이 역전 되었음을 의미한다. 원래는 의존성에 대한 제어권은 자기 자신이 가진다.
- ioc 하지 않았다면 private OwnerRepository repository = new OwnerRepository(); -> 이렇게 작성함
- ioc 하였다면 private OwnerRepository repo; -> new 하지 않음  

- controller, repository 등 어노테이션이 붙은 클래스는 bean = ioc컨테이너에서 객체들을 만들고 의존성을 관리해준다.
- bean = 스프링 ioc 컨테이너가 관리하는 객체
- 어떻게 등록?
- component scanning : @component 어노테이션(@repository,@service,@controller)이 붙어있는 클래스들을 찾아서 bean으로 등록해준다
- 직접 xml이나 자바 설정 파일에 등록한다.
- @bean 이라고 직접 작성해주면 된다.
- @bean 어노테이션을 사용하려면 @configuration 어노테이션이 붙은 클래스에서만 사용 가능하다.
- @autowired를 사용해 bean을 꺼내서 사용할 수 있다. 

### DI 의존성 주입 
- @autowired/@inject : 생성자, 필드, setter에 붙여서 사용한다.

### AOP 
- 흩어진 코드를 한 곳으로 모은다.
- @LogExecutionTime = 어디에 적용할지 표시 해두는 용도

## 9월24일
- html-id/class 차이  

## 9월25일
- 리터럴로 문자열을 생성한 경우 "문자열"이 같으면 하나의 String인스턴스를 참조한다.
- 생성자로 문자열을 생성한 경우 서로 다른 인스턴스를 가진다.

## 9월28일
- extend jparepository
- @RequiredArgsConstructor // bean으로 등록되어있다면 자동으로 생성자 만들어줌

## 9월29일
- jpa를 상속받으면 crud를 사용할 수 잇음
- 암호화 솔트 찾아보기~
- spring security가 기본 계정 user를 만들어준다+csrf 기능이 자동으로 켜져있다=csrf token = html에 hidden 태그에 설정되어 있다


## 9월30일
- UsernamePasswordAuthenticationToken : 로그아웃 하지 않는 한 사용자에 대한 세션을 계속 가지고 잇다
- maven에서 npm도 함께 빌드 시키려면 pom.xml에 플러그인을 추가해줘야 한다.                 
- mvnw test 하면 프론트엔드 플러그인 설치도 완료되고 말그대로 test를 실행..? 찾아보기 -> maven의 명령어
- spring web 와 spring web service 의 차이점!!
- selectkey => mybatics에서 제공하는 태그
- 타임리프 프레그먼트 사용  = 뷰에 대한 중복 코드 제거, th:if 로 if문을 사용할 수 있다.
- package.json에 디펜던시에 패키지 추가하고 npm install하면 설치해줌~
- font-awesome = 이미지가 아니라 폰트이기 때문에 가벼움
- js는 태그 닫을때 </>로~
- html head에 node모듈 불러올때 순서 유의하기

## 10월 1일
- localdatatime에서 이메일 발신 주기를 1시간 등 이런식으로 설정할 수 있다.
- jsessionid로 spring security에서 사용자 정보를 가져와 맞춰본다.
- @WithMockUser
- jpa 영속성= db에 연결되어 있는 상태, 이 영속성을 끊고 객체에 불러와서 필요한 데이터만 객체로 불러와서 사용한다,
