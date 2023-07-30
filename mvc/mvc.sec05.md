# Spring MVC

## `HandlerMapping`과 `HandlerAdapter`

기존의 컨트롤러 호출 방식은 `org.springframework.web.servlet.mvc.Controller`를 구현하는 방식이였다.

현재는 `SpringMVC`에서 `FrontController`의 역할을 하는 것은 `DispatcherServlet`으로, 다양한 기능을 제공하지만 핵심은 `HandlerMapping`
과 `HandlerAdapter`이다.

- `HandlerMapping` : 요청 `URL`을 어떤 컨트롤러가 처리할지 결정한다.
    - `HandlerMapping`에서 `Controller`를 찾을 수 있어야 하고, 찾지 못한다면 기본적으로 `404: Not Found`를 반환한다.
- `HandlerAdapter` : `HandlerMapping`에서 찾은 `Controller`를 실행한다.
    - `HandlerAdapter`는 `Controller`의 실행 결과를 `ModelAndView`로 변환해서 반환한다.

## *HandlerMapping*

| 구분                             | 설명                                                           |
|--------------------------------|--------------------------------------------------------------|
| `RequestMappingHandlerMapping` | `@RequestMapping`을 처리하는 `HandlerMapping`이다. `@Annotation` 기반 |
| `BeanNameUrlHandlerMapping`    | `Bean`의 이름으로 핸들러를 찾는 `HandlerMapping`이다.                     |

## *HandlerAdapter*

| 구분                               | 설명                                                           |
|----------------------------------|--------------------------------------------------------------|
| `RequestMappingHandlerAdapter`   | `@RequestMapping`을 처리하는 `HandlerAdapter`이다. `@Annotation` 기반 |
| `HttpRequestHandlerAdapter`      | `HttpRequestHandler`를 처리하는 `HandlerAdapter`이다.               |
| `SimpleControllerHandlerAdapter` | `interface:Controller`를 처리하는 `HandlerAdapter`이다.             |

### *`OldController`*의 `HandlerMapping`과 `HandlerAdapter`

| 동작               | 구분                               | 설명                                               |
|------------------|----------------------------------|--------------------------------------------------|
| `HandlerMapping` | `BeanNameUrlHandlerMapping`      | `Bean`의 이름으로 핸들러를 찾는 `HandlerMapping`이다.         |
| `HandlerAdapter` | `SimpleControllerHandlerAdapter` | `interface:Controller`를 처리하는 `HandlerAdapter`이다. |

## *`HttpRequestHandler`*의 `HandlerMapping`과 `HandlerAdapter`

`HttpRequestHandler`를 구현한 `MyHttpRequestHandler`

```java

@Component(value = "/springmvc/request-handler")
public class MyHttpRequestHandler implements HttpRequestHandler {
    @Override
    public void handleRequest(final HttpServletRequest request, final HttpServletResponse response) throws ServletException, IOException {
        System.out.println("MyHttpRequestHandler.handleRequest");
    }
}
```

| 동작                  | 구분                          | 설명                                                                                                           |
|---------------------|-----------------------------|--------------------------------------------------------------------------------------------------------------|
| `HandlerMapping` 조회 | `BeanNameUrlHandlerMapping` | `Bean`의 이름으로 핸들러를 찾는다.                                                                                       |
| `HandlerAdapter` 조회 | `HttpRequestHandlerAdapter` | `HandlerAdapter`의 `supports()`를 순회, `SimpleControllerHandlerAdapter`가 `interface:Controller`를 지원하기 때문에 대상이 됨 |
| `HandlerAdapter` 실행 | `HttpRequestHandlerAdapter` | `HttpRequestHandler`를 실행한다.                                                                                  |

## *`@RequestMapping`*의 `HandlerMapping`과 `HandlerAdapter`

`@RequestMapping`을 처리하는 `HandlerMapping`과 `HandlerAdapter`는 `@Annotation` 기반으로 동작한다. 이 `HandlerMapping`
과 `HandlerAdapter`이 가장 우선순위가 높다. `@RequestMapping`을 처리하는 `HandlerMapping`과 `HandlerAdapter`
는 `RequestMappingHandlerMapping`과 `RequestMappingHandlerAdapter`이다.
