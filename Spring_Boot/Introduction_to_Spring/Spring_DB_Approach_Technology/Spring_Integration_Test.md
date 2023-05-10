# 스프링 통합 테스트

스프링 컨테이너와 DB까지 연결한 통합 테스트를 진행

</br>

### 회원 서비스 스프링 통합 테스트

</br>

``` java
package hello.hellospring.service;

import hello.hellospring.domain.Member;
import hello.hellospring.repository.MemberRepository;
import hello.hellospring.repository.MemoryMemberRepository;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.transaction.annotation.Transactional;

import static org.assertj.core.api.Assertions.assertThat;
import static org.junit.jupiter.api.Assertions.assertThrows;

@SpringBootTest // SpirngBoot 테스트 애너테이션
@Transactional
class MemberServiceintegrationTest {

    @Autowired
    MemberService memberService;  // MemberService 변수 선언
    @Autowired
    MemberRepository memberRepository; // MemberRepository 변수 선언

    @Test
    void 회원가입() {   // 회원가입 테스트
        // given
        Member member = new Member();   // member 객체 생성
        member.setName("spring");    // member 객체 이름 설정

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

- `@SpringBootTest` : 스프링 컨테이너와 테스트를 함께 실행한다
- `@Transactional` : 테스트 케이스에 이 애노테이션이 있으면, 테스트 시작 전에 트랜잭션을 시작하고, 테스트 완료 후에 항상 롤백한다. 이렇게 하면 DB에 데이터가 남지 않으므로 다음 테스트에 영향을 주지 않는다.