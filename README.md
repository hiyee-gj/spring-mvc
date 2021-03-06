## Spring-MVC

### Spring-MVC-1 and Spring-MVC-2

### Spring-MVC-1

- 웹 어플리케이션 이해
- 서블릿
- 서블릿, JSP, MVC 패턴
- MVC 프레임워크 만들기
- 스프링 MVC - 구조 이해
- 스프링 MVC - 기본 기능
- 스프링 MVC - 웹 페이지 만들기

#### request.getParameter()

- `GET` 메서드의 `query parameter` 형식도 지원하고, `POST HTML Form` 형식도 둘 다 지원한다

> *참고*<br>
> 1. `content-type`은 `HTTP` 메시지 바디의 데이터 형식을 지정한다<br>
> 2. `GET URL query parameter` 형식으로 클라이언트에서 서버로 데이터를 전달할 때는`HTTP` 메시지 바디를 사용하지 않기 때문에 `content-type`이 없다
> 3. `POST HTML Form` 형식으로 데이터를 전달하면 `HTTP` 메시지 바디에 해당 데이터를 포함해서 보내기 때문에 바디에 포함된 데이터가 어떤 형식인지 `content-type`을 꼭 지정해야 한다.
     이렇게 폼으로 데이터를 전송하는 형식을 `application/x-www-form-urlencoded`라 한다.

#### MVC 패턴

- 기존 Sevlet과 JSP로 구현 시 문제점
    - 하나의 서블릿이나 JSP만으로 비즈니스 로직과 렌더링가지 모두 처리하게 되면 너무 많은 역할을 하게 됨
    - 유지보수가 어려워 짐(엄청 길어진 코드를 유지보수할 가능성이 높기 때문에)
    - 변경하는 라이프 사이클이 다르다는 큰 문제 UI 수정과 비즈니스 로직을 수정하는 일은 각각 다른 사유로 발생할 가능성이 높음
    - 대부분은 서로에게 영향을 주지 않는 코드들이 함께 있게 되는 문제
      <br><br>
- MVC 패턴
    - MVC 패턴은 컨트롤러, 뷰라는 영역으로 서로 역할을 나눈 것을 말한다
      <br><br>
- 컨트롤러
    - HTTP 요청을 받아서 파라미터를 검증하고, 비즈니스 로직을 실행한다.
    - 뷰에 전달할 결과 데이터를 조회해서 모델에 담는다
      <br><br>
- 모델
    - 뷰에 출력한 데이터를 담아둔다
    - 뷰가 필요한 데이터를 모두 모델에 담아서 전달해주는 덕분에 뷰는 비즈니스 로직이나 데이터 접근을 몰라도 된다
      <br><br>
- 뷰
    - 모델에 담겨있는 데이터를 사용해서 화면을 그리는 일에 집중한다
      <br><br>

#### MVC 패턴의 한계

1. 포워드 중복 : View로 이동하는 코드가 항상 중복 호출되어야 한다
2. ViewPath 중복
3. 공통처리가 어렵다

#### FrontController 패턴

- 프론트 컨트롤러 서블릿 하나로 클라이언트 요청을 받는다
- 프론트 컨트롤러가 요청에 맞는 컨트롤러를 찾아서 호출한다
- 입구를 하나로 통제해서 공통 처리를 용이하게 한다

#### 어댑터 패턴

- v4까지의 frontController를 보면 해당하는 controller 밖에 사용하지 못했다
    - 예를 들어 v4 안에서 v3의 controller를 사용하지 못하는 단점이 있었다
- 유연한 frontController로 모든 버전의 controller를 controll 해보자

#### 정리

- v1 : 프론트 컨트롤러 도입
    - 기존의 구조를 최대한 유지면서 프론트 컨트롤러를 도입
      <br><br>
- v2 : View 분리
    - 단순 반복되는 뷰 로직 분리
      <br><br>
- v3 : Model 추가
    - 서블릿 종속성 제거
    - 뷰 이름 중복 제거
      <br><br>
- v4: 단순하고 실용적인 컨트롤러
    - v3와 거의 비슷
    - 구현 입장에서 ModelView를 직접 생성해서 반환하지 않도록 편리한 인터페이스 제공
      <br><br>
- v5: 유연한 컨트롤러
    - 어댑터 도입
    - 어댑터를 추가해서 프레임워크를 유연하고 확장성 있게 설계

#### Spring MVC

- `@RequestMapping`
    - `@RequestMappingHandlerMapping` - `@RequestMapping`의 URI에 해당하는 handler 찾기
    - `@RequestMappingHandlerAdapter` - 찾은 handler를 처리할 수 있는 adapter를 찾기