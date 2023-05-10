# JPA

- JPA는 기존의 반복 코드는 물론이고, 기본적인 SQL도 JPA가 직접 만들어서 실행해준다.
- JPA를 사용하면, SQL과 데이터 중심의 설계에서 객체 중심의 설계로 패러다임을 전환을 할 수 있다.
- JPA를 사용하면 개발 생산성을 크게 높일 수 있다.

</br>

### build.gradle 파일에 JPA, h2 데이터베이스 관련 라이브러리 추가

</br>

``` java
plugins {	// 플러그인
	id 'java'	// 선택 언어
	id 'org.springframework.boot' version '2.7.11'	// Spring Boot 버전
	id 'io.spring.dependency-management' version '1.0.15.RELEASE'
}

group = 'hello'	// 그룹명
version = '0.0.1-SNAPSHOT'	// 그룹 버전
sourceCompatibility = '11'	// 자바 버전

repositories {
	mavenCentral()	// mavenCentral이라는 공개사이트에서 라이브러리 다운로드 설정
}

dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'	// thymeleaf 라이브러리
	implementation 'org.springframework.boot:spring-boot-starter-web'	// web 라이브러리
//	implementation 'org.springframework.boot:spring-boot-starter-jdbc'	// jdbc 라이브러리
	implementation 'org.springframework.boot:spring-boot-starter-data-jpa'	// jpa 라이브러리
	runtimeOnly 'com.h2database:h2'	// h2 database 클라이언트
	testImplementation 'org.springframework.boot:spring-boot-starter-test'	// junit5 test 라이브러리
}

tasks.named('test') {
	useJUnitPlatform()
}
```

</br>

`spring-boot-starter-data-jpa`는 내부에 jdbc 관련 라이브러리를 포함한다. 따라서 jdbc는 제거해도 된다.

</br>

### 스프링 부트에 JPA 설정 추가

</br>

`resources/application.properties`

```
spring.datasource.url=jdbc:h2:tcp://localhost/~/test
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
spring.jpa.show-sql=true
spring.jpa.hibernate.ddl-auto=none
```

</br>

> 주의!: 스프링부트 2.4부터는 `spring.datasource.username=sa`를 꼭 추가해주어야 한다. 그렇지 않으면 오류가 발생한다.

- `show-sql` : JPA가 생성하는 SQL을 출력한다.
- `ddl-auto` : JPA는 테이블을 자동으로 생성하는 기능을 제공하는데 none 를 사용하면 해당 기능을 끈다
    - `create`를 사용하면 엔티티 정보를 바탕으로 테이블도 직접 생성해준다.

</br>

### JPA 엔티티 매핑

</br>

``` java
package hello.hellospring.domain;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class Member {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY) // 엔티티 맵핑
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

### JPA 회원 리포지토리

</br>

``` java
package hello.hellospring.repository;

import hello.hellospring.domain.Member;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.jdbc.core.RowMapper;
import org.springframework.jdbc.core.namedparam.MapSqlParameterSource;
import org.springframework.jdbc.core.simple.SimpleJdbcInsert;

import javax.sql.DataSource;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.*;

public class JdbcTemplateMemberRepository implements MemberRepository {

    private final JdbcTemplate jdbcTemplate;    // 객체 선언

    @Autowired
    public JdbcTemplateMemberRepository(DataSource dataSource) {    // 생성자를 통해 Jdbc 객체 생성
        jdbcTemplate = new JdbcTemplate(dataSource);
    }


    @Override
    public Member save(Member member) {
        SimpleJdbcInsert jdbcInsert = new SimpleJdbcInsert(jdbcTemplate);   // insert 쿼리를 짜주는 객체
        jdbcInsert.withTableName("member").usingGeneratedKeyColumns("id");

        Map<String, Object> parameters = new HashMap<>();
        parameters.put("name", member.getName());

        Number key = jdbcInsert.executeAndReturnKey(new MapSqlParameterSource(parameters));
        member.setId(key.longValue());
        return member;
    }

    @Override
    public Optional<Member> findById(Long id) { // id로 회원 조회 메소드
        List<Member> result = jdbcTemplate.query("select * from member where id = ?", memberRowMapper(), id);
        return result.stream().findAny();   // Optional로 반환
    }

    @Override
    public Optional<Member> findByName(String name) {   // Name으로 회원 조회 메소드
        List<Member> result = jdbcTemplate.query("select * from member where name = ?", memberRowMapper(), name);
        return result.stream().findAny();   // Optional로 반환
    }

    @Override
    public List<Member> findAll() { // 전체 회원 조회
        return jdbcTemplate.query("select * from member", memberRowMapper());
    }

    private RowMapper<Member> memberRowMapper() {
        return (rs, rowNum) -> {
            Member member = new Member();
            member.setId(rs.getLong("id")); // member 객체에 아아디 저장
            member.setName(rs.getString("name"));   // member 객체에 이름 저장
            return member;  // 객체 반환
        };
    }
}
```

</br>

### 서비스 계층에 트랜잭션 추가

</br>

``` java
import org.springframework.transaction.annotation.Transactional
@Transactional

public class MemberService {}
```

</br>

- `org.springframework.transaction.annotation.Transactional`를 사용하자.
- 스프링은 해당 클래스의 메서드를 실행할 때 트랜잭션을 시작하고, 메서드가 정상 종료되면 트랜잭션을 커밋한다. 만약 런타임 예외가 발생하면 롤백한다
- **JPA를 통한 모든 데이터 변경은 트랜잭션 안에서 실행해야 한다.**

</br>

### JPA를 사용하도록 스프링 설정 변경

</br>

``` java
package hello.hellospring;

import hello.hellospring.repository.*;
import hello.hellospring.service.MemberService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import javax.persistence.EntityManager;
import javax.sql.DataSource;

@Configuration
public class SpringConfig {

//    private DataSource dataSource;  // 스프링이 제공하는 DataSource 호출
//
//    @Autowired
//    public SpringConfig(DataSource dataSource) {
//        this.dataSource = dataSource;
//    }

    private EntityManager em;

    @Autowired
    public SpringConfig(EntityManager em) {
        this.em = em;
    }

    @Bean
    public MemberService memberService() {
        return  new MemberService(memberRepository());
    }

    @Bean
    public MemberRepository memberRepository() {
//        return new MemoryMemberRepository();
//        return new JdbcMemberRepository(dataSource);
//        return new JdbcTemplateMemberRepository(dataSource);
        return new JpaMemberRepository(em);
    }
}
```