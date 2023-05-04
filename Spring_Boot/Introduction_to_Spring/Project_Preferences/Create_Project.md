# 프로젝트 생성

</br>

### 사전 준비물

- Java 11 설치
- IDE : IntelliJ 또는 Eclipse 설치

</br>

**[스트링 부트 스타터 사이트](https://start.spring.io)로 이동해서 스프링 프로젝트 생성**

</br>

### 프로젝트 선택

- Project :Project: Gradle - Groovy Project
- Spring Boot: 2.7.x
- Language: Java
- Packaging: Jar
- Java: 11

> Maven, Gradle은 버전 설정 및 필요한 라이브러리를 가져오고, 빌드하는 라이프사이클까지 관리해주는 툴   
> 과거에는 Maven을 많이 사용했지만, 요즘에는 Gradle을 많이 사용

> Spring Boot 버전은 SNAPSHOT, M1 같은 미정식 버전을 제외하고 최신 버전을 사용하시면 된다.   
> 예) 2.7.1 (SNAPSHOT) 이것은 아직 정식 버전이 아니므로 선택하면 안된다.   
> 예) 2.7.0 이렇게 뒤에 영어가 붙어있지 않으면 정식 버전이므로 이 중에 최신 버전을 선택하면 된다.

### Project Metadata

- groupId: hello
- artifactId: hello-spring

> groupId는 보통 기업의 도메인명을 입력   
> artifactId는 빌드된 결과물(프로젝트명)

### Dependencies

- Spring Web
- Thymeleaf

> 사용할 라이브러리를 선택

> Thymeleaf는 html을 만들어주는 템플릿 엔진

</br>

생성한 스프링 부트 프로젝트를 압축 풀고, IDE로 해당 프로젝트 안에 build.gradle 열기

- src폴더 : main폴더, test폴더가 있다.
    - main폴더 : java폴더, resources폴더가 있다.
        - java폴더 : 패키지와 실제 java 소스파일들이 있다.
        - resources폴더 : 실제 java 소스파일을 제외한 html, xml이나 properties와 같은 설정파일이 있다.
    - test폴더 : test 코드와 관련된 소스들이 있다.

</br>

### Gradle 전체 설정

</br>

`build.gradle`

``` gradle
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
	testImplementation 'org.springframework.boot:spring-boot-starter-test'	// junit5 test 라이브러리
}

tasks.named('test') {
	useJUnitPlatform()
}
```

</br>

Spring boot가 나오면서 설정파일까지 제공한다. 

</br>

### .gitignore

git에는 필요한 소스코드 파일만 업로드하고 나머지 빌드된 결과물 같은 것들은 업로드되면 안된다. 그래서 이러한 것들을 기본적으로 Spring Boot가 해준다.

</br>

### 동작 확인

- 기본 메인 클래스 실행
- 스프링 부트 메인 실행 후 에러페이지로 간단하게 동작 확인(`http://localhost:8080`)

> 메인 메소드를 실행하면 SpringApplication.run()이 애너테이션이 있는 클래스를 인자로 SpringApplication이 실행된다.   
SpringApplication이 tomcat이라는 웹서버를 내장하고 있어 실행되면 tomcat 웹서버를 띄우면서 Spring Boot가 같이 올라온다.

</br>

### IntelliJ Gradle 대신에 자바 직접 실행

최근 IntelliJ 버전은 Gradle을 통해서 실행 하는 것이 기본 설정이다. 이렇게 하면 실행속도가 느리다.   
다음과 같이 변경하면 자바로 바로 실행해서 실행속도가 더 빠르다.

- Preferences → Build, Execution, Deployment → Build Tools → Gradle
    - Build and run using: Gradle → IntelliJ IDEA
    - Run tests using: Gradle →  IntelliJ IDEA

**윈도우 사용자** File → Setting