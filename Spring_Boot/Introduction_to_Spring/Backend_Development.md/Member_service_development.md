# 회원 서비스 개발

회원 서비스는 회원 레포지토리와 도메인을 활용해서 비즈니스 로직을 작성하는 것

</br>

``` java
package hello.hellospring.service;

import hello.hellospring.domain.Member;
import hello.hellospring.repository.MemberRepository;
import hello.hellospring.repository.MemoryMemberRepository;

import java.util.List;
import java.util.Optional;

public class MemberService {

    private final MemberRepository memberRepository = new MemoryMemberRepository(); // 회원 레포지토리 객체 생성

    /**
     * 회원 가입
     */
    public Long join(Member member) {   // 회원 가입 메소드
        // 같은 이름이 있는 중복 회원X
        validateDuplicateMember(member);    // 중복 회원 검증
        memberRepository.save(member);  // 인자로 받은 member 객체를 메모리에 저장
        return member.getId();  // member 객체 id 반환
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
        return memberRepository.findAll();
    }

    public Optional<Member> findOne(Long memberId) {    // 해당 id를 가진 회원 조회
        return memberRepository.findById(memberId);
    }
}
```