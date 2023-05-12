# 회원 웹 기능 - 등록

</br>

## 회원 등록 폼 개발

</br>

### 회원 등록 폼 컨트롤러

</br>

``` java
@Controller // 컨트롤러 애너테이션을 달아주면 spring에서 관리를 한다.
public class MemberController {

    private  final MemberService memberService;

    @Autowired  // MemberController가 생성이 될 때, 스프링 빈에 등록되어있는 MemberService 객체를 가져와서 넣어준다.
    public MemberController(MemberService memberService) {  // 생성자를 통해 memberService 객체 생성
        this.memberService = memberService;
    }

    @GetMapping("/members/new") // get방식 맵핑
    public String createForm() {
        return "members/createMemberForm";  // 해당 템플릿 html 호출
    }
}
```

</br>

### 회원 등록 폼 HTML

</br>

`resources/templates/members/createMemberForm`

``` html
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<body>
<div class="container">
    <form action="/members/new" method="post">
        <div class="form-group">
            <label for="name">이름</label>
            <input type="text" id="name" name="name" placeholder="이름을
입력하세요">
        </div>
        <button type="submit">등록</button>
    </form>
</div> <!-- /container -->
</body>
</html>
```

</br>

## 회원 등록 컨트롤러

</br>

### 웹 등록 화면에서 데이터를 전달 받을 폼 객체

</br>

``` java
package hello.hellospring.controller;

public class MemberForm {
    private String name;    // 이름 변수 선언

    public String getName() {   // 이름 출력
        return name;
    }

    public void setName(String name) {  // 이름 저장
        this.name = name;
    }
}

```

</br>

### 회원 컨트롤러에서 회원을 실제 등록하는 기능

</br>

``` java
@PostMapping("/members/new")    // post 방식 맵핑
public String create(MemberForm form) { // post로 넘어온 객체를 받아서 실행
    Member member = new Member();   // 멤버 객체 생성
    member.setName(form.getName()); // 멤버 이름을 매개변수로 받은 객체의 이름으로 저장

    memberService.join(member); // 멤버 객체를 회원가입

    return "redirect:/";    // 초기 화면으로 이동
}
```