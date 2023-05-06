# 회원 서비스 테스트

</br>

### 기존에는 회원 서비스가 메모리 회원 리포지토리를 직접 생성하게 했다.

</br>

``` java
public class MemberService {

    private final MemberRepository memberRepository = new MemoryMemberRepository();

}
```

</br>

### 회원 리포지토리의 코드가 회원 서비스 코드를 DI 가능하게 변경한다.

</br>

``` java
public class MemberService {

    private final MemberRepository memberRepository; // 회원 레포지토리 변수 생성

    public MemberService(MemberRepository memberRepository) {   // 회원 레포지토리를 생성자를 통해 객체 생성
        this.memberRepository = memberRepository;
    }

    ...

}
```

</br>

### 회원 리포지토리의 코드가 회원 서비스 코드를 DI 가능하게 변경한다.

</br>

``` java
package hello.hellospring.service;

import hello.hellospring.domain.Member;
import hello.hellospring.repository.MemoryMemberRepository;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

import static org.assertj.core.api.Assertions.*;
import static org.junit.jupiter.api.Assertions.*;

class MemberServiceTest {

    MemberService memberService;  // MemberService 변수 선언
    MemoryMemberRepository memberRepository; // MemoryMemberRepository 변수 선언

    @BeforeEach
    public void beforeEach() {  // 같은 memberRepository 객체를 사용하도록 DI
        memberRepository = new MemoryMemberRepository();
        memberService = new MemberService(memberRepository);
    }

    @AfterEach
    public void afterEach() {
        memberRepository.clearStore();    // 각 테스트가 종료될 때마다 메모리 비우기
    }

    @Test
    void 회원가입() {   // 회원가입 테스트
        // given
        Member member = new Member();   // member 객체 생성
        member.setName("hello");    // member 객체 이름 설정

        // when
        Long saveId = memberService.join(member);   // member 회원가입

        // then
        Member findMember = memberService.findOne(saveId).get();    // 회원을 id로 찾아서 꺼내기
        assertThat(member.getName()).isEqualTo(findMember.getName());   // 꺼낸 회원과 가입한 회원을 비교
    }

    @Test
    public void 중복_회원_예외() {
        // given
        Member member1 = new Member();  // member1 객체 생성
        member1.setName("spring");  // member1 객체 이름 설정

        Member member2 = new Member();  // member2 객체 생성
        member2.setName("spring");  // member2 객체 이름 설정

        // when
        memberService.join(member1);    // member1 객체 회원 가입
        IllegalStateException e = assertThrows(IllegalStateException.class, () -> memberService.join(member2));// 예외가 발생하는지 테스트

        assertThat(e.getMessage()).isEqualTo("이미 존재하는 회원입니다."); // 예외 메세지 비교
//        try {
//            memberService.join(member2);
//            fail();
//        } catch (IllegalStateException e) {
//            assertThat(e.getMessage()).isEqualTo("이미 존재하는 회원입니다.");
//        }

        // then
    }

}
```

</br>

- `@BeforeEach` : 각 테스트 실행 전에 호출된다. 테스트가 서로 영향이 없도록 항상 새로운 객체를 생성하고, 의존관계도 새로 맺어준다.