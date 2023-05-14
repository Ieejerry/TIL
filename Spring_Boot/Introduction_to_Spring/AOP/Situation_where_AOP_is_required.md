# AOP가 필요한 상황

- 모든 메소드의 호출 시간을 측정하고 싶다면?
- 공통 관심 사항(cross-cutting concern) vs 핵심 관심 사항(core concern)
- 회원 가입 시간, 회원 조회 시간을 측정하고 싶다면?

</br>

[![MVC-DB-v2022-11-28.png](https://i.postimg.cc/pr4rtmTg/MVC-DB-v2022-11-28.png)](https://postimg.cc/m13BY27w)

</br>

### MemberService 회원 조회 시간 측정 추가

</br>

``` java
package hello.hellospring.service;

import hello.hellospring.domain.Member;
import hello.hellospring.repository.MemberRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import java.util.List;
import java.util.Optional;

@Transactional
public class MemberService {

    private final MemberRepository memberRepository; // 회원 레포지토리 변수 생성

    public MemberService(MemberRepository memberRepository) {   // 회원 레포지토리를 생성자를 통해 객체 생성
        this.memberRepository = memberRepository;
    }


    /**
     * 회원 가입
     */
    public Long join(Member member) {   // 회원 가입 메소드

        long start = System.currentTimeMillis();    // 메소드 시작 시간

        try {
            // 같은 이름이 있는 중복 회원X
            validateDuplicateMember(member);    // 중복 회원 검증
            memberRepository.save(member);  // 인자로 받은 member 객체를 메모리에 저장
            return member.getId();  // member 객체 id 반환
        } finally {
            long finish = System.currentTimeMillis();   // 메소드 끝나는 시간
            long timeMs = finish - start;
            System.out.println("join = " + timeMs + "ms");
        }
    }

    private void validateDuplicateMember(Member member) {
        memberRepository.findByName(member.getName())    // 메모리에 인자로 받은 member 객체와 같은 이름을 가진 객체가 있는지 확인
            .ifPresent(m -> {
                throw new IllegalStateException("이미 존재하는 회원입니다.");
            }); // 반환된 객체가 null이 아니고 값이 있으면 해당 exception 발생
    }

    /**
     * 전체 회원 조회
     */
    public List<Member> findMembers() { // 전체 회원 조회
        long start = System.currentTimeMillis();    // 메소드 시작 시간

        try {
            return memberRepository.findAll();
        } finally {
            long finish = System.currentTimeMillis();   // 메소드 끝나는 시간
            long timeMs = finish - start;
            System.out.println("findMembers = " + timeMs + "ms");
        }
    }

    public Optional<Member> findOne(Long memberId) {    // 해당 id를 가진 회원 조회
        return memberRepository.findById(memberId);
    }
}
```

</br>

### 문제

- 회원가입, 회원 조회에 시간을 측정하는 기능은 핵심 관심 사항이 아니다.
- 시간을 측정하는 로직은 공통 관심 사항이다
- 시간을 측정하는 로직과 핵심 비즈니스의 로직이 섞여서 유지보수가 어렵다.
- 시간을 측정하는 로직을 별도의 공통 로직으로 만들기 매우 어렵다.
- 시간을 측정하는 로직을 변경할 때 모든 로직을 찾아가면서 변경해야 한다.