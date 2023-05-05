# 정적 컨텐츠

정적 컨텐츠는 서버에서는 아무것도 안하고 파일을 그대로 웹브라우저로 내려주는 것

- 스프링 부트 정적 컨텐츠 기능
- https://docs.spring.io/spring-boot/docs/2.3.1.RELEASE/reference/html/spring-bootfeatures.html#boot-features-spring-mvc-static-content

</br>

`resources/static/hello-static.html`

``` html
<!DOCTYPE HTML>
<html>
    <head>
        <title>static content</title>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    </head>
    <body>
        정적 컨텐츠 입니다.
    </body>
</html>
```

</br>

원하는 파일을 `resources/static` 폴더에 넣으면 정적파일이 그대로 반환이 된다. 하지만 여기엔 어떠한 프로그래밍을 할 수가 없다.

</br>

### 실행

- http://localhost:8080/hello-static.html

</br>

### 정적 컨텐츠 이미지

</br>

[![MVC-DB-v2022-11-28.png](https://i.postimg.cc/yYxS8v2d/MVC-DB-v2022-11-28.png)](https://postimg.cc/svF2n9jd)