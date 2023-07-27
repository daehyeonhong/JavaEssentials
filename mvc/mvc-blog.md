# Spring MVC Blog

## `WebServer`와 `WebApplicationServer`

### WebServer

웹서버는 HTTP 프로토콜에 기반하여 웹 브라우저의 요청을 서비스하는 기능을 담당하며, HTML 문서나 각종 리소스를 전달한다. 웹서버는 주로 정적인 요소에 대한 응답을 처리하는데 사용된다.
정적 리소스란? 서버에 저장되어 있는 파일을 그대로 전달하는 리소스를 말한다. 예를 들어 HTML, CSS, JS, 이미지 파일 등이 있다. 대표적인 웹서버로는 Apache, Nginx, IIS 등이 있다.

### WebApplicationServer

웹 어플리케이션 서버는 웹 서버와 웹 컨테이너의 기능을 모두 갖추고 있다. 웹 컨테이너는 웹 서버와 웹 어플리케이션 사이에서 동작하며, 동적인 데이터 생성을 담당한다. 웹 컨테이너는 서블릿(Servlet)과 같은
자바 기반의 웹 프로그래밍을 위한 기술을 지원한다. 대표적인 웹 어플리케이션 서버로는 Tomcat, JBoss, WebLogic, WebSphere, Netty 등이 있다.

## `Servlet`

### `Servlet`이란?

서블릿은 웹 어플리케이션 서버에서 동작하는 작은 자바 프로그램이다. 서블릿은 웹 서버와 웹 어플리케이션 사이에서 동작하며, 동적인 데이터 생성을 담당한다. 서블릿은 자바 기반의 웹 프로그래밍을 위한 기술을
지원한다. `@WebServlet` 어노테이션을 사용하여 서블릿을 등록할 수 있는데, 이때 서블릿의 URL 패턴을 지정할 수 있다. 서블릿은 `HttpServlet` 클래스를 상속받아야 하며 다양한 메소드를
오버라이딩하여 사용할 수 있다.

## 동시 요청 - 멀티 쓰레드

### 멀티 쓰레드

멀티 쓰레드는 하나의 프로세스 내에서 여러 개의 쓰레드가 동시에 작업을 수행하는 것을 말한다. 멀티 쓰레드는 하나의 프로세스를 공유하므로, 프로세스 간의 통신보다 쓰레드 간의 통신이 훨씬 간단하다. 멀티 쓰레드는
쓰레드 간의 작업량이 작고, 자원을 공유하는 작업을 수행할 때 유용하다. `WAS`는 멀티 쓰레드로 동작하며, 미리 지정한 쓰레드 풀을 통해 쓰레드를 관리한다.

### 쓰레드 풀

쓰레드 풀은 미리 생성해둔 쓰레드를 관리하는 객체이다. 쓰레드 풀은 쓰레드를 생성하고 소멸하는 비용을 줄이기 위해 사용한다. 쓰레드 풀은 미리 생성해둔 쓰레드를 풀에 저장해두었다가 필요할 때 쓰레드를 가져와 작업을
수행하고 반환한다.

## HTML, HTTP API, CSR, SSR

| 구분       | 동작                                                             |
|----------|----------------------------------------------------------------|
| HTML     | 서버에서 HTML을 생성하여 클라이언트에 전달                                      |
| HTTP API | JSON 데이터를 클라이언트에 전달, 주로 서버간 혹은 네이티브 앱 프로그램 간에 사용               |
| CSR      | 클라이언트에서 HTML을 생성하여 화면에 표시, 주로 React, Vue, Angular 등의 프레임워크를 사용 |
| SSR      | 서버에서 HTML을 생성하여 클라이언트에 전달                                      |

## `Servlet` 사용 방법

### `Servlet` 등록

`Servlet`을 등록하는 방법은 크게 2가지가 있다. `@WebServlet` 어노테이션을 사용하는 방법과 `web.xml` 파일을 사용하는 방법이다. `@WebServlet` 어노테이션을 사용하는
방법은 `Servlet` 클래스에 `@WebServlet` 어노테이션을 붙여주고 `urlPatterns` 속성을 통해 URL 패턴을 지정해주면 된다. 또한 `HttpServlet` 클래스를 상속받아야 한다.

```java

@WebServlet(urlPatterns = "/hello")
public class HelloServlet extends HttpServlet {
    ...
}
```

### `request`와 `response`

`Servlet`은 `HttpServletRequest`와 `HttpServletResponse`를 매개변수로 받아 사용한다. `HttpServletRequest`는 HTTP 요청에 대한 정보를 가지고
있으며, `HttpServletResponse`는 HTTP 응답에 대한 정보를 가지고 있다.

`HttpServletRequest` 객체에서 매개변수를 가져오는 방법은 `request.getParameter()` 메소드를 사용하면 된다. `HTTPBody에 담긴 JSON 데이터를 가져오는 방법은 `
request.getInputStream()` 메소드를 통해 가져온 input stream을 StreamUtils를 사용하여 String으로 변환하여 ObjectMapper를 사용하여 JSON 데이터를 가져올 수
있다.

```java
final String username=request.getParameter("username");
final ServletInputStream inputStream=request.getInputStream();
final String messageBody=StreamUtils.copyToString(inputStream,StandardCharsets.UTF_8);
final HelloData helloData=objectMapper.readValue(messageBody,HelloData.class);
```

`HttpServletResponse` 객체에서 응답을 보내는 방법은 `response.getWriter().write()` 메소드를 사용하면 된다. `response.getWriter().write()` 메소드는
문자열을 응답으로 보내는 메소드이다.

```java
response.getWriter().write("hello "+username);
```

HTML 파일을 응답으로 보내는 방법은 `response.getWriter().write()` 메소드를 사용하여 HTML 코드를 작성하여 응답으로 보내면 된다.

```java
final PrintWriter writer=response.getWriter();
        writer.println("<html>");
        writer.println("<body>");
        writer.println("<div>안녕?</div>");
        writer.println("</body>");
        writer.println("</html>");
```

response에 JSON 데이터를 전달하는 방법은 객체를 생성하여 `ObjectMapper`를 사용하여 JSON 데이터로 변환한 후 `response.getWriter().write()` 메소드를 사용하여 응답으로
보내면 된다.

```java
final HelloData helloData=new HelloData(username,age);
final String result=objectMapper.writeValueAsString(helloData);
        response.getWriter().write(result);
```

## JSP

JSP를 활용하면 HTML 코드에 자바 코드를 삽입하여 동적인 웹 페이지를 생성할 수 있다. JSP는 HTML 코드에 자바 코드를 삽입하여 동적인 웹 페이지를 생성할 수 있으며, JSP는 서블릿으로 변환되어
실행된다. JSP는 `<% %>` 태그를 사용하여 자바 코드를 삽입할 수 있으며, `<%= %>` 태그를 사용하여 자바 코드의 결과를 출력할 수 있다. JSP는 HTML 코드에 자바 코드를 삽입하여 동적인 웹
페이지를 생성할 수
있다.

## MVC 패턴

### MVC 패턴이란?

MVC 패턴은 Model, View, Controller의 약자이다. MVC 패턴은 하나의 애플리케이션을 세 가지 역할로 구분한 패턴이다. Model은 데이터를 처리하는 부분이며, View는 사용자에게 보여지는
부분이며, Controller는 사용자의 요청을 처리하는 부분이다. MVC 패턴은 Model과 View, Controller를 분리하여 각각의 역할에 집중할 수 있도록 한다. 또한 MVC 패턴은 유지보수가 쉽고,
코드의 재사용성이 높아진다. 다만 공통처리 로직이나 예외처리 로직 등이 중복되는 경우가 많다는 한계를 가지고 있다.
