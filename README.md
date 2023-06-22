# 개요

인프런 스프링 MVC 1편 - 백엔드 웹 개발 핵심 기술 강의를 듣고 정리한 문서  

[![Velog's GitHub stats](https://velog-readme-stats.vercel.app/api?name=2jooin1207&slug=스프링-mvc-프로젝트)](https://velog.io/@2jooin1207/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8)

# 웹 기본 동작 방식

Get 방식
- 주소창에 원하는 데이터를 적거나 링크를 클릭해서 호출

post 방식
- 입력 화면에서 필요한 내용을 작성후에 전송 같은 버튼을 클릭해서 호출 

정적 데이터
- 항상 동일하게 고정된 데이터를 전송하는 방식
- web server 

동적 데이터
- 매번 다른 데이터를 동적으로 구성해서 전송
- WAS

## 웹 mvc

>데이터는 컨트롤러에서, 결과는 뷰에서 처리

Model - View - Controller

## PRG 패턴

post 방식과 redirect를 결합해서 사용하는 PRG 패턴

1. 사용자는 컨트롤러에 원하는 작업을 post방식으로 처리하기를 요청
2. post 방식을 컨트롤러에서 처리하고 브라우저는 다른 경로로 이동(get)하라는 응답(redirect)
3. 브라우저는 get방식으로 이동

# 세션과 필터

- 무상태에서 과거를 기억하는 법
- HTTP에서 쿠키를 사용하여 세션 트랙킹을 진행한다

# 스프링

>객체지향의 의존성 주입 기법을 적용할 수 있는 객체지향 프레임워크

## 의존성 주입

>스프링의 구조는 ApplicationContext라는 개체 안에 Bean으로 등록된 객체들이 생성되어서 관리되는 구조

ApplicationContext
- bean이라는 객체들을 관리하기 위해 존재하는 저장소

Bean
- 주로 오랜시간 동안 프로그램 내에서 상주하면서 중요한 역할을 하는 '역할 중심'의  객체
- DAO, VO같은 데이터에 중점을 둔 객체들을 bean으로 등록되지 않는다
- 등록만 해두면 원하는 곳에서 쉽게 다른 객체를 사용할 수 있다.

필드주입(field Injection) 방식
- 맴버 변수에 직접 @Autowired를 선언하는 방식
- 맞는 타입의 빈이 존재하는 지를 확인 후, 의존성을 주입

각종 어노테이션

- @Controller: MVC의 컨트롤러를 위한 어노테이션
- @Service: 서비스 계층의 객체를 위한 어노테이션
- @Repository: DAO와 같은 객체를 위한 어노테이션
- @Component: 일반 객체나 유틸리티 객체를 위한 어노테이션

생성자 주입 방식
- 주입 받아야 하는 객체의 변수는 final로 작성
- 생성자를 이용해서 해당 변수를 생성자의 파라미터로 지정

## 스프링 mvc

1. front-controller패턴을 이용하여 모든 흐름의 사전/사후 처리를 가능하게 설계
2. 어노테이션을 적극적으로 활용하여 최소한의 코드로 많은 처리가 가능
3. 상당히 추상적인 방식으로 개발가증

Front-Controller 패턴
- 모든 요청이 반드시 하나의 객체를 지나서 처리 되므로, 모든 공통적인 처리를 객체에서 가능

### 컨트롤러

@Controller
- 해당클리스가 컨트롤러 역할을 한다는 것을 의미
- bean으로 사용

@RequestMapping
- 특정한 경로의 요청을 지정

@Get/PostMapping

@RequestParam
- 요청에 전달된 파라미터 이름을 기준으로 동작할때 기본 값을 지정할 수 있다
- 파라미터에 값이 도착하지 않았을 때를 대비

### Model

모델에 데이터를 답아 View로 전달

Model.addAttridute
- 뷰에 전달할 '이름'과 '값'을 지정할 수 있다

~~~
//컨트롤러
public void model(Model model, Data data){
	model.addAttribute("message", data);
}

//뷰
<h1>${message}</h1>
~~~

@Model.addAttridute
- 지정된 변수명 외에 다른 이름을 사용하고 싶은 경우 사용

RedirectAttribute
- 사용하는 메소드는 다음과 같다
- .addAtrribute(키, 값): 리다이렉트시 쿼리 스트링이 될 값을 지정
- .addFlashAttribute(키, 값): 일회용으로만 데이터를 전달하고 삭제되는 값을 지정
-> URL에 값은 안보임


### 주로 사용되는 어노테이션

컨트롤러
- @Controller
- @RestController: rest방식의 처리를 위한 컨트롤러
- @RequestMapping: 특정 url패턴에 맞는 컨트롤러인지를 명시

메소드 선언부
- @Get/Post/Delete...Mapping
- @RequestMapping: get/post 방식 둘다 지원하는 경우
- @ResponseBody: rest 방식에서 사용

메소드의 파라미터에 사용
- @RequestParam: request에 있는 특정한 이름의 데이터를 파라미터로 받아서 처리
- @PathVariable: url 경로의 일부를 변수로 삼아서 처리하기 위해서 사용
- @ModelAttribute: 해당 파라미터는 반드시 model에 포함되어서 다시 view로 전달됨을 명시

기타
@Configuration: 해당 클래스가 스프링 빈에 대한 설정을 하는 클래스임을 명시


