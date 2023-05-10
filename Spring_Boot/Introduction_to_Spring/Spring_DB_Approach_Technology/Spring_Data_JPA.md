# 스프링 데이터 JPA

스프링 부트와 JPA만 사용해도 개발 생산성이 정말 많이 증가하고, 개발해야할 코드도 확연히 줄어든다. 여기에 스프링 데이터 JPA를 사용하면, 기존의 한계를 넘어 마치 마법처럼, 리포지토리에 구현 클래스 없이 인터페이스 만으로 개발을 완료할 수 있다. 그리고 반복 개발해온 기본 CRUD 기능도 스프링 데이터 JPA가 모두 제공한다.
스프링 부트와 JPA라는 기반 위에, 스프링 데이터 JPA라는 환상적인 프레임워크를 더하면 개발이 정말 즐거워진다. 지금까지 조금이라도 단순하고 반복이라 생각했던 개발 코드들이 확연하게 줄어든다. 따라서 개발자는 핵심 비즈니스 로직을 개발하는데, 집중할 수 있다.
실무에서 관계형 데이터베이스를 사용한다면 스프링 데이터 JPA는 이제 선택이 아니라 필수 이다.

> 주의: 스프링 데이터 JPA는 JPA를 편리하게 사용하도록 도와주는 기술이다. 따라서 JPA를 먼저 학습한 후에 스프링 데이터 JPA를 학습해야 한다.

- 앞의 JPA 설정을 그대로 사용한다.

</br>

### 스프링 데이터 JPA 회원 리포지토리

</br>

``` java
package hello.hellospring.repository;

import hello.hellospring.domain.Member;
import org.springframework.data.jpa.repository.JpaRepository;

import java.util.Optional;

public interface SpringDataJpaMemberRepository extends JpaRepository<Member, Long>, MemberRepository {  // JpaRepository, MemberRepository 인터페이스를 구현

    @Override
    Optional<Member> findByName(String name);
}
```

</br>

### 스프링 데이터 JPA 회원 리포지토리를 사용하도록 스프링 설정 변경

</br>

``` java
package hello.hellospring;

import hello.hellospring.repository.*;
import hello.hellospring.service.MemberService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import javax.persistence.EntityManager;

@Configuration
public class SpringConfig {

//    private DataSource dataSource;  // 스프링이 제공하는 DataSource 호출
//
//    @Autowired
//    public SpringConfig(DataSource dataSource) {
//        this.dataSource = dataSource;
//    }

    private final MemberRepository memberRepository;

    @Autowired
    public SpringConfig(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }

    @Bean
    public MemberService memberService() {
        return  new MemberService(memberRepository);
    }

//    @Bean
//    public MemberRepository memberRepository() {
//        return new MemoryMemberRepository();
//        return new JdbcMemberRepository(dataSource);
//        return new JdbcTemplateMemberRepository(dataSource);
//        return new JpaMemberRepository(em);
//    }
}
```

</br>

- 스프링 데이터 JPA가 `SpringDataJpaMemberRepository`를 스프링 빈으로 자동 등록해준다.

</br>

## 스프링 데이터 JPA 제공 클래스

</br>

[![MVC-DB-v2022-11-28.png](https://i.postimg.cc/tTkh3NTp/MVC-DB-v2022-11-28.png)](https://postimg.cc/YG4GkgYs)

</br>

### 스프링 데이터 JPA 제공 기능

- 인터페이스를 통한 기본적인 CRUD
- `findByName()` , `findByEmail()`처럼 메서드 이름 만으로 조회 기능 제공
- 페이징 기능 자동 제공