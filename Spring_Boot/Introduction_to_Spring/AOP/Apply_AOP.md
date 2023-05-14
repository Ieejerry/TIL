# AOP 적용

- AOP: Aspect Oriented Programming
- 공통 관심 사항(cross-cutting concern) vs 핵심 관심 사항(core concern) 분리

</br>

[![MVC-DB-v2022-11-28.png](https://i.postimg.cc/dtYFXMJW/MVC-DB-v2022-11-28.png)](https://postimg.cc/7bmjGWG7)

</br>

### 시간 측정 AOP 등록

</br>

``` java
package hello.hellospring.AOP;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.springframework.stereotype.Component;

@Aspect
@Component
public class TimeTraceAop {

    @Around("execution(* hello.hellospring..*(..))")
    public Object execute(ProceedingJoinPoint joinPoint) throws Throwable {
        long start = System.currentTimeMillis();
        System.out.println("START: " + joinPoint.toString());
        try {
            return joinPoint.proceed();
        } finally {
            long finish = System.currentTimeMillis();
            long timeMs = finish - start;
            System.out.println("END: " + joinPoint.toString() + " " + timeMs + "ms");
        }
    }
}

```

</br>

### 해결

- 회원가입, 회원 조회등 핵심 관심사항과 시간을 측정하는 공통 관심 사항을 분리한다.
- 시간을 측정하는 로직을 별도의 공통 로직으로 만들었다.
- 핵심 관심 사항을 깔끔하게 유지할 수 있다
- 변경이 필요하면 이 로직만 변경하면 된다.
- 원하는 적용 대상을 선택할 수 있다.

</br>

## 스프링의 AOP 동작 방식 설명

</br>

### AOP 적용 전 의존관계

</br>

[![MVC-DB-v2022-11-28.png](https://i.postimg.cc/rsHz5MdC/MVC-DB-v2022-11-28.png)](https://postimg.cc/MfyWSkmv)

</br>

### AOP 적용 후 의존관계

</br>

[![MVC-DB-v2022-11-28.png](https://i.postimg.cc/s2JXwpQ2/MVC-DB-v2022-11-28.png)](https://postimg.cc/3ydYw0ZM)

</br>

### AOP 적용 전 전체 그림

</br>

[![MVC-DB-v2022-11-28.png](https://i.postimg.cc/vBkcVGx7/MVC-DB-v2022-11-28.png)](https://postimg.cc/Q9g8LGbV)

</br>

### AOP 적용 후 전체 그림

</br>

[![MVC-DB-v2022-11-28.png](https://i.postimg.cc/T3t2bTZy/MVC-DB-v2022-11-28.png)](https://postimg.cc/WdJPLcpj)

</br>

- 실제 Proxy가 주입되는지 콘솔에 출력해서 확인하기