# *`SpringMVC`*

`Controller`에서 `@RequestMapping`된 메서드에서 `String:ViewName`을 반환하면 `ViewResolver`를 사용해서 뷰를 찾고 렌더링한다.

또한 메서드의 매개변수로 `HttpServletRequest`, `HttpServletResponse` 뿐만 아니라 해당 요청의 정보를 담고 있는
`@RequestParam` 등을 사용할 수 있으며 `Model`을 매개변수로 받아서 `Model`에 데이터를 담아서 뷰에 전달할 수 있다.

추가로 `@Controller` 방식을 도입하면 메서드의 `HTTP Method`에 따라서 다른 메서드를 호출할 수 있다. 허가된 메서드만 호출할 수 있도록
`@RequestMapping`에 `method` 속성을 사용하거나, `@GetMapping`, `@PostMapping` 등을 사용할 수 있다.
