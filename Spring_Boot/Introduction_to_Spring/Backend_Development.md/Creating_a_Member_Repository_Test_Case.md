# 회원 리포지토리 테스트 케이스 작성

개발한 기능을 실행해서 테스트 할 때 자바의 main 메서드를 통해서 실행하거나, 웹 애플리케이션의 컨트롤러를 통해서 해당 기능을 실행한다. 이러한 방법은 준비하고 실행하는데 오래 걸리고, 반복 실행하기 어렵고 여러 테스트를 한번에 실행하기 어렵다는 단점이 있다. 자바는 JUnit이라는 프레임워크로 테스트를 실행해서 이러한 문제를 해결한다.

</br>

### 회원 리포지토리 메모리 구현체 테스트

</br>

`src/test/java` 하위 폴더에 생성한다.

``` java
package hello.hellospring.repository;

import hello.hellospring.domain.Member;
import org.assertj.core.api.Assertions;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.Test;
import java.util.List;

import java.util.Optional;

import static org.assertj.core.api.Assertions.*;

class MemoryMemberRepositoryTest {  // 테스트할 클래스와 동일한 이름 뒤에 Test 추가하여 클래스 생성

    MemoryMemberRepository repository = new MemoryMemberRepository();   // 메모리 객체 생성

    @AfterEach
    public void afterEach() {
        repository.clearStore();    // 각 테스트가 종료될 때마다 메모리 비우기
    }

    @Test
    public void save() {    // save() 메소드 테스트 메소드
        Member member = new Member();   // Member 객체 생성
        member.setName("spring");   // Member 이름 설정

        repository.save(member);    // Member 객체 메모리에 저장

        Member result = repository.findById(member.getId()).get();  // 메모리에 저장된 Member 객체 id로 찾아서 꺼내기
        assertThat(member).isEqualTo(result);   // 메모리에 저장된 객체와 만든 객체 비교
    }

    @Test
    public void findbyName() {  // findbyName() 메소드 테스트
        Member member1 = new Member();  // Member1 객체 생성
        member1.setName("spring1"); // Member 객체 이름 설정
        repository.save(member1);   // Member 객체 메모리에 저장

        Member member2 = new Member();  // Member1 객체 생성
        member2.setName("spring2"); // Member 객체 이름 설정
        repository.save(member2);   // Member 객체 메모리에 저장

        Member result = repository.findByName("spring1").get(); // Member1 객체의 이름으로 객체 잦아서 꺼내기

        assertThat(result).isEqualTo(member1);  // 꺼낸 객체와 만든 객체 비교
    }

    @Test
    public void findAll() {
        Member member1 = new Member();  // member1 객체 생성
        member1.setName("spring1"); // member1 객체 이름 설정
        repository.save(member1);   // member1 객체 메모리에 저장

        Member member2 = new Member();  // member2 객체 생성
        member2.setName("spring2"); // member1 객체 이름 설정
        repository.save(member2);   // member1 객체 메모리에 저장

        List<Member> result = repository.findAll(); // 메모리에 객체를 리스트에 넣기

        assertThat(result.size()).isEqualTo(2); // 객체를 담은 리스트의 사이즈가 2개인지 테스트
    }

}
```

</br>

- `@AfterEach` : 한번에 여러 테스트를 실행하면 메모리 DB에 직전 테스트의 결과가 남을 수 있다. 이렇게 되면 다음 이전 테스트 때문에 다음 테스트가 실패할 가능성이 있다. `@AfterEach`를 사용하면 각 테스트가 종료될 때 마다 이 기능을 실행한다. 여기서는 메모리 DB에 저장된 데이터를 삭제한다.
- 테스트는 각각 독립적으로 실행되어야 한다. 테스트 순서에 의존관계가 있는 것은 좋은 테스트가 아니다.