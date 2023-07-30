## *`ViewResolver`*

`View`경로를 지정하는 방법은 다음과 같다.

1. `application.properties|yml`에 설정
2. `WebMvcConfigurer`를 구현한 `@Configuration`클래스에서 `Bean` 설정

application.yml

```yaml
spring:
  mvc:
    view:
      prefix: /WEB-INF/jsp/
      suffix: .jsp
```

```java

@Configuration
public class MvcConfig implements WebMvcConfigurer {
    @Override
    public void configureViewResolvers(final ViewResolverRegistry registry) {
        registry.jsp("/WEB-INF/jsp/", ".jsp");
    }
}
```

이와 같이 설정하면? 논리명으로 지정된 `View`를 찾아서 `View`를 렌더링한다.
권장하지는 않지만 절대경로로 지정할 수도 있다.

```java

@Controller
public class MvcController {
    @GetMapping("/mvc/view-resolver")
    public ModelAndView viewResolver(final Model model) {
        model.addAttribute("data", "hello");
        return new ModelAndView("/WEB-INF/jsp/viewResolver.jsp");
    }
}
```

`SpringBoot`에서 자동으로 등록하는 `ViewResolver`는 다음과 같다.

| 구분                             | 설명                                                                                |
|--------------------------------|-----------------------------------------------------------------------------------|
| `BeanNameViewResolver`         | `Bean`의 이름으로 `View`를 찾아서 반환한다. `Bean`의 이름은 `View`의 논리명과 동일하다. (Ex: `Excel` 파일 생성) |
| `InternalResourceViewResolver` | `prefix`와 `suffix`를 사용해서 `View`를 찾아서 반환한다. `JSP`를 처리할 때 주로 사용한다.                  |

`View` 반환 방식은 다음과 같다.

| 순서 | 기능                                | 설명                                                                                                                                                                                                    |
|----|-----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1  | `HandlerAdatper` 호출               | `HandlerAdapter`를 통해 `new-form`이라는 논리 뷰 이름을 획득.                                                                                                                                                       |
| 2  | `ViewResolver` 호출                 | `ViewResolver`를 통해 `new-form`이라는 논리 뷰 이름에 해당하는 `View`를 획득. <br/> `BeanNameViewResolver`는 `Bean`의 이름으로 `View`를 찾는다. 하지만 `Bean`의 이름과 논리 뷰 이름이 동일하지 않다. 따라서 `InternalResourceViewResolver`가 `View`를 찾는다. |
| 3  | `InternalResourceViewResolver` 호출 | `InternalResourceViewResolver`는 `prefix`와 `suffix`를 사용해서 `View`를 찾는다. `prefix`는 `/WEB-INF/views/`이고 `suffix`는 `.jsp`이다. 따라서 `InternalResourceView`를 찾을 수 있다.                                          |
| 4  | `View` 반환                         | `View`를 통해서 렌더링 결과를 생성한다. `InternalResourceView`는 `forward`를 사용해서 `JSP`를 실행한다.                                                                                                                        |

**참고** 다른 `View`와 달리 `JSP`는 `forward()`를 통해서 해당 `JSP`로 이동(실행)해야 렌더링이 된다. 나머지 `ViewTemplate`은 해당 부분을 생략한다. 
