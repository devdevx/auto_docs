# Spring Boot

## Links

- [Spring Boot Academy](https://spring.academy/courses)
- [SpringDeveloper YT channel](https://www.youtube.com/@SpringSourceDev/videos)
- [Clean architecture](https://github.com/spember/spring-shoestore)

## Recipes

### Show build info in log and actuator info endpoint

**NOTE**: Some values are not available until is executed from jar

1. In `application.properties` configure

```
spring.config.import=optional:classpath:/git.properties

spring.application.name=@project.name@
spring.application.version=@project.version@

info.app.name=@project.name@
info.app.description=@project.description@
info.app.version=@project.version@

management.info.java.enabled=true
management.info.build.enabled=true
management.info.env.enabled=true
management.info.defaults.enabled=true
management.info.git.enabled=true
management.info.os.enabled=true

management.endpoint.info.enabled=true

management.endpoint.health.probes.enabled=true
management.endpoint.health.show-details=always

management.endpoints.web.exposure.include=health,info
```

2. In `banner.txt` define

```
Spring Boot: ${spring-boot.version}
Application: ${spring.application.name} ${spring.application.version}
Git: ${git.branch} ${git.commit.id.abbrev} ${git.tags} ${git.commit.time}
```

3. In `pom.xml` declare

```
...
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
...
<plugin>
    <groupId>io.github.git-commit-id</groupId>
    <artifactId>git-commit-id-maven-plugin</artifactId>
</plugin>
...
```

**Note:** In Spring Boot 2 use this for the git plugin.

```
...
<plugin>
    <groupId>pl.project13.maven</groupId>
    <artifactId>git-commit-id-plugin</artifactId>
</plugin>
...
```
### Integrate Sentry

1. In `pom.xml` declare

```
<dependency>
    <groupId>io.sentry</groupId>
    <artifactId>sentry-spring-boot-starter-jakarta</artifactId>
    <version>7.3.0</version>
</dependency>
```

**Note:** In Spring Boot 2 use this for the git plugin.

```
<dependency>
    <groupId>io.sentry</groupId>
    <artifactId>sentry-spring-boot-starter</artifactId>
    <version>7.3.0</version>
</dependency>
```

2. Configure the `SENTRY_AUTH_TOKEN` and `SENTRY_DSN` env vars.

3. Optionally user context data (In web filters, event pre processors, etc).

```
import io.sentry.Sentry;
import io.sentry.protocol.User;

...

User user = new User();
user.setEmail(email);
user.setName(name);
user.setUsername(username);
user.setData(Map.of("prop", prop));
Sentry.setUser(user);
```

4. Configure the `@ControllerAdvice` to send unexpected web originated exceptions.

```
@ExceptionHandler(Exception.class)
public ResponseEntity<...> unexpectedException(Exception e) {
    Sentry.captureException(e);
    return ResponseEntity.internalServerError().body(...);
}
```

5. Capture the exceptions originated from scheduled tasks.

```
@Component
public class SentryThreadPoolTaskSchedulerCustomizer implements ThreadPoolTaskSchedulerCustomizer {
    @Override
    public void customize(ThreadPoolTaskScheduler taskScheduler) {
        taskScheduler.setErrorHandler(Sentry::captureException);
    }
}
```

**Note:**: In Spring Boot 2 use this instead.

```
@Component
public class SentryTaskSchedulerCustomizer implements TaskSchedulerCustomizer {
    @Override
    public void customize(ThreadPoolTaskScheduler taskScheduler) {
        taskScheduler.setErrorHandler(Sentry::captureException);
    }
}
```

6. Configure the async executor to handle sentry data between threads and the exception handler to manage exceptions from `@Async`.

```
public class AsyncHandler implements AsyncUncaughtExceptionHandler {

    @Override
    public void handleUncaughtException(Throwable ex, Method method, Object... params) {
        Sentry.captureException(ex);
    }
}
```

```
@Configuration
public class SentryAsyncConfigurer implements AsyncConfigurer {

    @Override
    public Executor getAsyncExecutor() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setTaskDecorator(new SentryTaskDecorator());
        executor.initialize();
        return executor;
    }

    @Override
    public AsyncUncaughtExceptionHandler getAsyncUncaughtExceptionHandler() {
        return new AsyncHandler();
    }
}
```

**Note:**: In Spring Boot 2 use this instead.

```
@Configuration
public class SentryAsyncConfigurerSupport extends AsyncConfigurerSupport {

    @Override
    public Executor getAsyncExecutor() {
        ThreadPoolTaskExecutor executor = new ThreadPoolTaskExecutor();
        executor.setTaskDecorator(new SentryTaskDecorator());
        executor.initialize();
        return executor;
    }

    @Override
    public AsyncUncaughtExceptionHandler getAsyncUncaughtExceptionHandler() {
        return new AsyncHandler();
    }
}
```

## Controller annotation interceptor

## Learn

https://tuhrig.de/self-made-event-dispatcher/

https://github.com/ityouknow/spring-boot-examples

https://github.com/xkcoding/spring-boot-demo

## Learn security

https://kevcodez.de/posts/2020-03-26-secure-spring-boot-app-with-oauth2-aws-cognito/

https://www.baeldung.com/spring-security-method-security

https://www.baeldung.com/spring-security-create-new-custom-security-expression

https://www.baeldung.com/spring-security-role-filter-json

https://dreamix.eu/blog/java/implementing-custom-authorization-function-for-springs-pre-and-post-annotations

http://code-addict.pl/permission-evaluator-boot2/

https://insource.io/blog/articles/custom-authorization-with-spring-boot.html

https://dzone.com/articles/simple-attribute-based-access-control-with-spring

## Learn distributed transactions

https://piotrminkowski.com/2020/06/19/distributed-transactions-in-microservices-with-spring-boot/

## Learn health check

https://github.com/spring-projects/spring-boot/blob/main/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/system/DiskSpaceHealthIndicator.java

## Learn SAGA

https://progressivecoder.com/wp-content/cache/all/saga-pattern-implementation-with-axon-and-spring-boot-part-1/index.html

https://tuhrig.de/saga-pattern-with-spring-boot-and-activemq/

## Learn websockets

https://dzone.com/articles/build-a-secure-app-using-spring-boot-and-websocket

## Learn Admin Server

https://codecentric.github.io/spring-boot-admin/

