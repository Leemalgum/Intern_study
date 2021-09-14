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

# 9월14일
## 캡슐화
- 연관있는 속성과 메서드를 클래스로 묶고, 외부에서 직접 접근하지 못하도록 은닉하는 것 이다.

### 캡슐화의 효과
- 추상화 : 실제 메소드의 동작을 외부에서 이해할 필요가 없고 이를 단순 호출만으로 기능을 실행할 수 있다.
이를 통해 객체 단위의 프로그램 설계가 가능한다.
- 재사용성의 향상 : 한 객체에 관련된 속성 및 메소드는 모두 캡슐화의 형태로 제공되어 객체의 모듈성(구성 요소 변경이 용이한 정도)과 응집도(내부 요소들의 연관 정도)가 높아지고 이를 통해 재사용성이 높아진다.
- 위의 두 가지의 이유로 유지보수의 효율성이 향상한다.
- 무결성 보장 : 보통의 캡슐화 코딩이란 변수는 private, 메소드는 public으로 선언하고, 이는 객체의 무결성을 보장한다.

