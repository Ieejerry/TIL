# 순수 JDBC

</br>

## 환경 설정

</br>

### build.gradle 파일에 jdbc, h2 데이터베이스 관련 라이브러리 추가

</br>

``` java
implementation 'org.springframework.boot:spring-boot-starter-jdbc'
runtimeOnly 'com.h2database:h2'
```

</br>

### 스프링 부트 데이터베이스 연결 설정 추가

</br>

`resources/application.properties`

``` java
spring.datasource.url=jdbc:h2:tcp://localhost/~/test
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
```

</br>

> 주의!: 스프링부트 2.4부터는 `spring.datasource.username=sa`를 꼭 추가해주어야 한다. 그렇지 않으면 `Wrong user name or password` 오류가 발생한다. 참고로 다음과 같이 마지막에 공백이 들어가면 같은 오류가 발생한다. `spring.datasource.username=sa` ← 공백 주의, 공백은 모두 제거해야 한다.

> 참고: 인텔리J 커뮤니티(무료) 버전의 경우 `application.properties` 파일의 왼쪽이 다음 그림과 같이 회색으로 나온다. 엔터프라이즈(유료) 버전에서 제공하는 스프링의 소스 코드를 연결해주는 편의 기능이 빠진 것인데, 실제 동작하는데는 아무런 문제가 없다.

</br>

[![image.png](https://i.postimg.cc/CKQYNPP4/image.png)](https://postimg.cc/KKBdcNyK)

</br>

## Jdbc 리포지토리 구현

</br>

### Jdbc 회원 리포지토리

</br>

``` java
package hello.hellospring.repository;

import hello.hellospring.domain.Member;
import org.springframework.jdbc.datasource.DataSourceUtils;

import javax.sql.DataSource;
import java.sql.*;
import java.util.ArrayList;
import java.util.List;
import java.util.Optional;

public class JdbcMemberRepository implements MemberRepository {

    private final DataSource dataSource;    // DataSource 생성

    public JdbcMemberRepository(DataSource dataSource) {    // spring boot가 만든 데이터 소스 주입 받음
        this.dataSource = dataSource;
    }

    @Override
    public Member save(Member member) {
        String sql = "insert into member(name) values(?)";

        Connection conn = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;    // 결과를 받음

        try {
            conn = getConnection(); // connection 가져오기
            pstmt = conn.prepareStatement(sql, Statement.RETURN_GENERATED_KEYS);    // insert sql을 보내고, pk값을 얻음

            pstmt.setString(1, member.getName());   // 파라미터 1번=(?)에 member.getName() 대입

            pstmt.executeUpdate();  // db에 쿼리 날림
            rs = pstmt.getGeneratedKeys();  // db가 생성한 키를 반환

            if (rs.next()) {    // 값이 있으면
                member.setId(rs.getLong(1));    // 성공하면 값을 꺼냄
            } else {
                throw new SQLException("id 조회 실패"); // 실패하면 exception 발생
            }
            return member;  // 객체 반환
        } catch (Exception e) {
            throw new IllegalStateException(e); // exception 처리
        } finally {
            close(conn, pstmt, rs); // 자원 풀어주기
        }
    }
    @Override
    public Optional<Member> findById(Long id) {
        String sql = "select * from member where id = ?";   // 조회 쿼리문

        Connection conn = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;

        try {
            conn = getConnection(); // connection 가져오기
            pstmt = conn.prepareStatement(sql); // sql 날리기
            pstmt.setLong(1, id);   // pstmt 세팅

            rs = pstmt.executeQuery();  // db에서 조회

            if(rs.next()) { // 값이 있으면
                Member member = new Member();
                member.setId(rs.getLong("id"));
                member.setName(rs.getString("name"));   // 멤버 객체 생성
                return Optional.of(member); // 반환
            } else {
                return Optional.empty();
            }
        } catch (Exception e) {
            throw new IllegalStateException(e);
        } finally {
            close(conn, pstmt, rs);
        }
    }
    @Override
    public List<Member> findAll() {
        String sql = "select * from member";

        Connection conn = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;

        try {
            conn = getConnection();
            pstmt = conn.prepareStatement(sql);

            rs = pstmt.executeQuery();

            List<Member> members = new ArrayList<>();   // 리스트 생성
            while(rs.next()) {
                Member member = new Member();
                member.setId(rs.getLong("id"));
                member.setName(rs.getString("name"));
                members.add(member);    // 리스트에 객체 저장
            }

            return members;
        } catch (Exception e) {
            throw new IllegalStateException(e);
        } finally {
            close(conn, pstmt, rs);
        }
    }
    @Override
    public Optional<Member> findByName(String name) {
        String sql = "select * from member where name = ?";

        Connection conn = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;

        try {
            conn = getConnection();
            pstmt = conn.prepareStatement(sql);
            pstmt.setString(1, name);

            rs = pstmt.executeQuery();

            if(rs.next()) {
                Member member = new Member();
                member.setId(rs.getLong("id"));
                member.setName(rs.getString("name"));
                return Optional.of(member);
            } return Optional.empty();
        } catch (Exception e) {
            throw new IllegalStateException(e);
        } finally {
            close(conn, pstmt, rs);
        }
    }
    private Connection getConnection() {
        return DataSourceUtils.getConnection(dataSource);
    }
    private void close(Connection conn, PreparedStatement pstmt, ResultSet rs)
    {
        try {
            if (rs != null) {
                rs.close();
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        try {
            if (pstmt != null) {
                pstmt.close();
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
        try {
            if (conn != null) {
                close(conn);
            }
        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
    private void close(Connection conn) throws SQLException {
        DataSourceUtils.releaseConnection(conn, dataSource); }
}
```

</br>

### 스프링 설정 변경

</br>

``` java
package hello.hellospring;

import hello.hellospring.repository.JdbcMemberRepository;
import hello.hellospring.repository.MemberRepository;
import hello.hellospring.repository.MemoryMemberRepository;
import hello.hellospring.service.MemberService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import javax.sql.DataSource;

@Configuration
public class SpringConfig {

    private DataSource dataSource;  // 스프링이 제공하는 DataSource 호출

    @Autowired
    public SpringConfig(DataSource dataSource) {
        this.dataSource = dataSource;
    }

    @Bean
    public MemberService memberService() {
        return  new MemberService(memberRepository());
    }

    @Bean
    public MemberRepository memberRepository() {
//        return new MemoryMemberRepository();
        return new JdbcMemberRepository(dataSource);
    }
}
```

</br>

- DataSource는 데이터베이스 커넥션을 획득할 때 사용하는 객체다. 스프링 부트는 데이터베이스 커넥션 정보를 바탕으로 DataSource를 생성하고 스프링 빈으로 만들어둔다. 그래서 DI를 받을 수 있다.

</br>

### 구현 클래스 추가 이미지

</br>

[![MVC-DB-v2022-11-28.png](https://i.postimg.cc/T2q289pT/MVC-DB-v2022-11-28.png)](https://postimg.cc/14X1wDGd)

</br>

### 스프링 설정 이미지

</br>

[![MVC-DB-v2022-11-28.png](https://i.postimg.cc/qRHrShrt/MVC-DB-v2022-11-28.png)](https://postimg.cc/kVsLt5B9)

</br>

- 개방-폐쇄 원칙(OCP, Open-Closed Principle)
    - 확장에는 열려있고, 수정, 변경에는 닫혀있다.
- 스프링의 DI (Dependencies Injection)을 사용하면 기존 코드를 전혀 손대지 않고, 설정만으로 구현 클래스를 변경할 수 있다.
- 회원을 등록하고 DB에 결과가 잘 입력되는지 확인하자.
- 데이터를 DB에 저장하므로 스프링 서버를 다시 실행해도 데이터가 안전하게 저장된다.