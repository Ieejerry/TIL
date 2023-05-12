# 회원 웹 기능 - 홈 화면 추가

</br>

### 홈 컨트롤러 추가

</br>

``` java
package hello.hellospring.controller;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class HomeController {

    @GetMapping("/")
    public String home() {  // 기본 도메인 home.html로 매핑
        return "home";
    }
}
```

</br>

### 회원 관리용 홈

</br>

``` html
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<body>
<div class="container">
    <div>
        <h1>Hello Spring</h1>
        <p>회원 기능</p>
        <p>
            <a href="/members/new">회원 가입</a>
            <a href="/members">회원 목록</a>
        </p>
    </div>
</div> <!-- /container -->
</body>
</html>
```

</br>

> 참고: 컨트롤러가 정적 파일보다 우선순위가 높다.