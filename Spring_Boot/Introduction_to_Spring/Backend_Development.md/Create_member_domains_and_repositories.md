# 회원 도메인과 리포지토리 만들기

</br>

### 회원 객체

</br>

``` java
package hello.hellospring.domain;

public class Member {

    private Long id;    // 회원 id 식별자, 시스템이 정하는 id값
    private String name;    // 회원 이름

    public Long getId() {   // 회원 id 가져오기
        return id;
    }

    public void setId(Long id) {    // 회원 id 저장하기
        this.id = id;
    }

    public String getName() {   // 회원 이름 가져오기
        return name;
    }

    public void setName(String name) {  // 회원 이름 저장하기
        this.name = name;
    }
}
```

</br>

### 회원 리포지토리 인터페이스

</br>

``` java
package hello.hellospring.repository;

import hello.hellospring.domain.Member;

import java.util.List;
import java.util.Optional;

public interface MemberRepository {
    Member save(Member member); // 회원 정보 저장
    Optional<Member> findById(Long id); // 회원 id로 회원 찾기
    Optional<Member> findByName(String name);   // 회원 이름으로 회원 찾기
    List<Member> findAll(); // 모든 회원 찾기
}
```

</br>

### 회원 리포지토리 메모리 구현체

</br>

``` java
package hello.hellospring.repository;

import hello.hellospring.domain.Member;

import java.util.*;

/**
 * 동시성 문제가 고려되어 있지 않음, 실무에서는 ConcurrentHashMap, AtomicLong 사용 고려
 */
public class MemoryMemberRepository implements MemberRepository {

    private static Map<Long, Member> store = new HashMap<>();   // 메모리에 회원 정보를 저장할 HashMap 선언
    private static long sequence = 0L;  // id값 생성 해주는 변수

    @Override
    public Member save(Member member) { // 회원 정보 저장
        member.setId(++sequence);   // 회원 id값 저장
        store.put(member.getId(), member);  // 메모리에 회원 정보 저장
        return member;  // 회원 정보 반환
    }

    @Override
    public Optional<Member> findById(Long id) { // id로 회원 찾기
        return Optional.ofNullable(store.get(id));  // 메모리에 id값을 키값으로 갖는 객체 반환, null이 반환될 경우가 있어 Optional 사용
    }

    @Override
    public Optional<Member> findByName(String name) {   // 이름으로 회원 찾기
        return store.values().stream()
                .filter(member -> member.getName().equals(name))
                .findAny(); // store를 돌면서 매개변수로 받은 값과 같은 값을 가지는 객체 반환
    }

    @Override
    public List<Member> findAll() { // 모든 회원 정보 찾기
        return new ArrayList<>(store.values()); // store에 저장된 모든 객체를 배열에 담아 반환
    }

    public void clearStore() {  // 메모리 비우기
        store.clear();
    }
}
```