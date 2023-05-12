# 회원 웹 기능 - 조회

</br>

### 회원 컨트롤러에서 조회 기능

</br>

``` java
@GetMapping("/members") // get방식 맵핑
public String list(Model model) {   // 조회페이지 모델을 받아서 실행
    List<Member> members = memberService.findMembers(); // List에 모든 멤버들의 정보를 담음
    model.addAttribute("members", members); // 조회페이지 모델에 List 전송
    return "members/memberList";    // 해당 url로 이동
}
```

</br>

### 회원 리스트 HTML

</br>

``` html
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<body>
<div class="container">
    <div>
        <table>
            <thead>
            <tr>
                <th>#</th>
                <th>이름</th>
            </tr>
            </thead>
            <tbody>
            <tr th:each="member : ${members}">
                <td th:text="${member.id}"></td>
                <td th:text="${member.name}"></td>
            </tr>
            </tbody>
        </table>
    </div>
</div> <!-- /container -->
</body>
</html>
```

</br>