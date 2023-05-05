# API

</br>

## @ResponseBody 문자 반환

</br>

``` java
@Controller
public class HelloController {
    
    @GetMapping("hello-string")
    @ResponseBody   // http body부에 이 데이터를 직접 넣음
    public String helloString(@RequestParam("name") String name) {
        return "hello " + name;  // "hello spring"
    }

}
```

</br>

- `@ResponseBody`를 사용하면 뷰 리졸버(`viewResolver`)를 사용하지 않음
- 대신에 HTTP의 BODY에 문자 내용을 직접 반환(HTML BODY TAG를 말하는 것이 아님)

</br>

### 실행

- http://localhost:8080/hello-string?name=spring

</br>

## @ResponseBody 객체 반환

</br>

``` java
@Controller
public class HelloController {

    @GetMapping("hello-api")
    @ResponseBody
    public Hello helloApi(@RequestParam("name") String name) {
        Hello hello = new Hello();
        hello.setName(name);
        return hello;
    }

    static class Hello {
        private  String name;

        public String getName() {
            return  name;
        }

        public void setName(String name) {
            this.name = name;
        }
    }

}
```

</br>

- `@ResponseBody`를 사용하고, 객체를 반환하면 객체가 JSON으로 변환됨

</br>

### 실행

- http://localhost:8080/hello-api?name=spring

</br>

## @ResponseBody 사용 원리

</br>

[![MVC-DB-v2022-11-28.png](https://i.postimg.cc/QCn6zD65/MVC-DB-v2022-11-28.png)](https://postimg.cc/30mCysQJ)

</br>

- `@ResponseBody`를 사용
    - HTTP의 BODY에 문자 내용을 직접 반환
    - `viewResolver` 대신에 `HttpMessageConverter`가 동작
    - 기본 문자처리: `StringHttpMessageConverter`
    - 기본 객체처리: `MappingJackson2HttpMessageConverter`
    - byte 처리 등등 기타 여러 HttpMessageConverter가 기본으로 등록되어 있음

> 참고: 클라이언트의 HTTP Accept 해더와 서버의 컨트롤러 반환 타입 정보 둘을 조합해서 `HttpMessageConverter`가 선택된다.