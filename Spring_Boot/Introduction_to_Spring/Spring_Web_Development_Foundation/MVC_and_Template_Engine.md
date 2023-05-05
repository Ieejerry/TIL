# MVC와 템플릿 엔진

- MVC: Model, View, Controller

</br>

### Contoller

</br>

``` java
@Controller
public class HelloController {

    @GetMapping("hello-mvc")
    public String helloMvc(@RequestParam("name") String name, Model model) {
        model.addAttribute("name", name);
        return "hello-templete.html";
    }
    
}
```

</br>

### View

</br>

`resources/templates/hello-template.html`

``` html
<html xmlns:th="http://www.thymeleaf.org">
    <body>
        <p th:text="'hello ' + ${name}">hello! empty</p>
    </body>
</html>
```

</br>

html파일이 템플릿 엔진과 연결되어 있다면 기존 html정보를 서버에서 넘어온 정보로 치환이 가능하고, 연결이 되어있지 않은 경우 html파일 그대로 볼 수 있다는 장점이 있다.

</br>

### 실행

- http://localhost:8080/hello-mvc?name=spring

위의 처럼 주소값을 주면 `name=spring`이 인자로 컨트롤러로 넘어간다. 컨트롤러에서 매개변수 `name`은 `spring`이라는 값으로 대입되고, 이 변수가 `model`에 담겨서 `spring-templete`으로 넘어가면 `${name}`이 모델에서 키값이 name인 것의 value값을 꺼내오는 것이기 때문에 `spring`이 출력된다.

</br>

### MVC, 템플릿 엔진 이미지

</br>

[![MVC-DB-v2022-11-28.png](https://i.postimg.cc/0QyjtCgF/MVC-DB-v2022-11-28.png)](https://postimg.cc/LqGm5L83)