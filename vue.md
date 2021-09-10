# Vue.js 끝장내기
<details>
    <summary>목차</summary>
 
- [9월6일](#9월6일)
  * [웹 서비스 개발 절차](#웹-서비스-개발-절차)
  * [프론트엔드 개발자의 역할](#프론트엔드-개발자의-역할)
  * [API 문서](#API-문서)
- [9월7일](#9월7일)
  * [Hash Mode](#Hash-Mode)
  * [History Mode](#History-Mode)
  * [코드 스플리팅](#코드-스플리팅)
- [9월8일](#9월8일)
  * [env 설정](#env-설정)
  * [.env 파일 규칙](#.env-파일-규칙)
  * [axios](#axios)
  * [Async, Await](#Async,-Await)
- [9월9일](#9월9일)
  * [vuejs 파일 구조](#vuejs-파일-구조)
  * [vue state](#vue-state)
  * [axios interceptors](#axios-interceptors)

</details>

# 9월6일
## 웹 서비스 개발 절차
- 요구사항 -> 서비스 기획 -> UI/UX 상세 설계 -> GUI 디자인 -> 퍼블리싱 -> 백엔드 API 개발 -> 프론트엔드 개발 -> QA

## 프론트엔드 개발자의 역할
- 화면단 코든 작성
- 기획, 디자인, 퍼블리싱, 백엔드 개발자와의 소통

## API 문서
- Swagger = API 문서 자동화 도구

## preset
- 미리 정의된 옵션과 플러그인을 포함하는 JSON 객체

## vue-til 구조
- modules = package.json의 내용들
- public = html, index 파일들
- browserslistrc, eslintrc, jest, babel = 설정 파일

## eslint
- 자바스크립트 문법에서 에러를 표시해주는 도구
- eslintrc 파일 안에 prettier 작성 = 충돌방지를 위해

## prettier
- 코드 스타일을 정리해주는 도구

# 9월7일
## Hash Mode
- 모든 URL을 HASH(#)형태로 서비스
- URL이 변경될 때까지 페이지가 다시 로드 되지 않는다.

## History Mode
- 페이지를 다시 로드하지 않고 URL을 탐색할 수 있다.

## 코드 스플리팅
- spa의 단점은 js번들 파일에 어플리케이션에 대한 모든 로직을 불러오기 때문에 규모와 함께 용량이 커지면서 로딩속도가 지연될 수 있다. 이러한 단점을 필요에 따라 여러개의 파일로 분리시키는 코드 스플리팅을 통해 해결할 수 있다.

# 9월8일
## env 설정
- 프로젝트 루트 경로에 .env 파일을 생성한다.
- .env 파일은 키 = 값 형태로 정의할 수 있는 환경 변수 파일이다.
- VUE_APP_API_URL=http://localhost:3000/ -> VUE_APP 이 포함된 환경 변수는 따로 import하지 않아도 자동으로 사용할 수 있다.
- src/api/index.js
~~~javascript
import axios from 'axios';

const axiosService = axios.create({
  baseURL: process.env.VUE_APP_API_URL,
});

function registerUser(userData) {
  return axiosService.post('signup', userData);
}

export { registerUser };
~~~

## .env 파일 규칙
- .env.development = 개발 모드에서만 동작한다, 개발 모드에서는 우선순위가 가장 높다.
- .env.production = 배포 모드에서만 동작한다.
- .env 파일이 우선순위가 가장 낮으며, 위 두 파일에 없는 공통의 값을 지정하기 위해 사용한다.

## axios
- javascript의 플러그인으로 Promise 기반의 비동기 처리방식을 사용한다.

## Async, Await
- javascript의 ES6 문법에서 사용하는 비동기 처리 패턴이다.
- async는 현재 사용할 함수를 비동기로 처리하겠다는 선언자이다.
- await은 비동기로 순차 처리하기 위해서 수행할 API에 붙이는 선언자이다.

# 9월9일
## vuejs 파일 구조
- dependencies = npm run build의 결과물에 포함되며 어플리케이션을 동작시킬 때 필요한 라이브러리들
- devdependencies = npm run build의 결과물에 포함되지 않는 ESLint같은 도구들

## vue state

## axios interceptors
-  로그인 시 Request Header에 토큰값을 가져와야 하는데, api가 실행되기 전에 이미 axios instance가 생성되어 로그인을 하여도 토큰 값을 가져오지 않는다.
-  이를 해결하기 위해 store에 토큰값을 저장하고 axios interceptors를 사용해서 토큰값을 axios instance에 넣어준다.
~~~javascript
// src/api/index.js
// 액시오스 초기화 함수
function createInstance() {
  const instance = axios.create({
    baseURL: process.env.VUE_APP_API_URL,
  });
  return setInterceptors(instance);
}

// src/api/common/interceptors.js
export function setInterceptors(instance) {
    // 요청 인터셉터
  instance.interceptors.request.use(
    function(config) {
      // 요청 성공 직전 호출
      // console.log(config);
      config.headers.Authorization = store.state.token;
      return config;
    },
    function(error) {
      // 요청 에러 직전 호출
      return Promise.reject(error);
    },
  );
  
  // 응답 인터셉터
  instance.interceptors.response.use(
    function(response) {
      // http status가 200인 경우, 응답 성공 직전 호출
      return response;
    },
    function(error) {
      // http status가 200이 아닌 경우, 응답 에러 직전 호출
      return Promise.reject(error);
    },
  );
  return instance;
~~~
