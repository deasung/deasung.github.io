---
title: 처음배우는 스프링부트2 책을 읽고 요점정리
published: true
---


스프링부트 프로젝트 의존성 

https://github.com/spring-projects/spring-boot

application-{profile}.yml {profile}에 원하는 프로파일값으로 YAML 파일을 추가하면 

애플리케이션 실행시 지정한 프로파일값을 바탕으로 실행

서버에서 실행시

    $ java -jar ... -D spring.profiles.active=dev

## YAML 파일 매핑

- 유연한 바인딩: 프로퍼티값을 객체에 바인딩할 경우 필드를 낙타 표기법(Camel Case)으로 선언 프로퍼티의 키는 다양한 형식(낙타 표기법,케밥 표기법(Kebab Case),언더바 표기법(Underscore) 선언 바인딩

- 메타데이터 지원: 프로터피 키에 대한 정보를 메타데이터 파일(Json) 로 제공
- SpEL(Spring Expression Language,스프링 표현 언어) 평가: SpEL은 런타임에 객체 참조에 대해 질의하고 조작하는 기능을 지원하는 언어, 특히 메서드 호출 및 기본 문자열 템플릿기능을 제공. @Value만 사용 가능

# 스프링 부트 테스트

## @DataJpaTest

JPA 관련 테스트 설정만 로드 

기본적으로 인메모리 임베디드 데이터베이스를 사용 

데이터 소스주입
```java
import org.junit.runner.RunWith;
import org.springframework.test.context.junit4.SpringRunner;
import org.springframework.boot.test.autoconfigure.jdbc.AutoConfigureTestDatabase;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;
import org.springframework.test.context.ActiveProfiles;
    
@RunWith(SpringRunner.class)
@DataJpaTest
@ActiveProfiles("...")
@AutoConfigureTestDatabase(replace = AutoConfigureTestDatabase.Replace.NONE)
public class JpaTest {
...
}
```

- @AutoConfigureTestDatabase 어노테이션의 기본 설정값인 Replace.Any를 사용하면 기본적으로 내장된 데이터소스를 사용함 , Replace.NONE으로 설정하면 @ActiveProfiles에 설정한 프로파일 환경값에 따라 데이터소스가 적용됨
- JPA 테스트가 끝날때마다 자동으로 테스트에 사용한 데이터를 롤백

# @RestClientTest

REST 관련 테스트를 도와주는 어노테이션 
```java
@RunWith(SpringRunner.class)
@RestClientTest(BookRestService.class)
public class BookRestTest {
    
  @Rule
  public ExpectedException thrown = ExpectedException.none();
    
  @Autowired
  private BookRestService bookRestService;
    
  @Autowired
  private MockRestServiceServer server;
    
  @Test
  public void rest_테스트() {
    	
    this.server.expect(requestTo("/rest/test"))
      .andRespond(withSuccess(new ClassPathResource("/test.json",
    	getClass()), MediaType.APPLICATION_JSON));
    
    Book book = this.bookRestService.getRestBook();
    assertThat(book.getTitle()).isEqualTo("테스트");
  }
    
  @Test
  public void rest_error_테스트() {
    		
    this.server.expect(requestTo("/rest/test"))
      .andRespond(withServerError());
    this.thrown.expect(HttpServerErrorException.class);
    this.bookRestService.getRestBook();
  }
    
}

```
    
- @RestClientTest 는 테스트 대상이 되는 빈을 주입받음
- @Rule로 지정한 필드값은 @Before나 @After 어노테이션에 상관없이 하나의 테스트 메서드가 끝날때 마다 정의한 값으로 초기화 시켜줌

## @JsonTest

@JsonTest 어노테이션은 JSON의 직렬화(serialization)와 역직렬화(deserialization)을 수행하는 라이브러리인 Gson과 Jackson API의 테스트를 제공함

## 4장 스프링 부트 웹

스프링이 관리하는 컴포넌트에서 퍼시스턴스 계층에 대해 더 명확하게 특수한 제네릭 스테레오타입을 말함

퍼시스턴스 계층이란 물리적 저장공간을 뜻함.영속성을 가진 파일이나 DB에 로직을 구현하는 것을 뜻하기도함.

JPA fetch eager와 lazy 두종류가 있음 eager는 도메인을 조회할때 즉시 관련된 객체도 같이 조회

lazy는 객체가 실제로 사용될때 조회됨

## CommandLineRunner를 사용하여 DB에 데이터 넣기

CommandLineRunner는 애플리케이션 구동 후 특정 코드를 실행시키고 싶을 때 직접 구현하는 인터페이스 

애플리케이션 구동시 테스트 데이터를 함께 생성하여 데모 프로젝트를 실행/테스트하고 싶을때 편리함 

스프링 DI(Dependency Injection) 스프링의 주요 특성 중 하나로 주로 의존 관계 주입 

의존 관계를 주입하는게 아니라 단지 객체의 레퍼런스를 전달하여 참조시킨다는 의미로 의존 관계 설정이라고 함 

## 5장 스프링 부트 시큐리티 + OAuth2

스프링 부트 시큐리티에서 가장 중요한 개념은 '인증(authentication)' 과 '권한부여(authorization)'

@NestedConfigurationProperty

@EnableWebSecurity 어노테이션은 웹에서 시큐리티 기능 사용하겠다는 어노테이션 

스프링부트는 @EnableWebSecurity 자동 설정이 적용됨 
```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    
  @Override
  protected void configure(HttpSecurity http) throws Exception {
    CharacterEncodingFilter filter = new CharacterEncodingFilter();
    	
    http
      .authorizeRequests()  //인증 메커니즘 요청 HttpServletRequest 기반으로 설정
    	  .antMatchers("/", "/login/**", "/css/**", "/images/**", "/js/**", // 요청 패턴을 리스트 형식으로 설정 
    	    "/console/**").permitAll() //설정한 리퀘스트 패턴 누구나 접근 허용 
    	  .anyRequest() // 설정한 요청 이외의 리퀘스트 요청을 표현 
    	  .authenticated() // 해당 요청은 인증된 사용자만 할수 있음 
    	.and()
    	  .headers() // 응답에 해당하는 header 설정 
    		.frameOptions().disable() // XFrameOptionsHeaderWriter 최적화 설정을 허용안함 
    	.and()
    	  .exceptionHandling()
    		.authenticationEntryPoint(new LoginUrlAuthenticationEntryPoint(
    		  "/login")) //인증의 진입 지점 인증되지 않은 사용자가 허용되지 않은 경로로 리퀘스트 요청하면 /login으로 이동 
    	.and()
    	  .formLogin()
    		.successForwardUrl("/board/list") // 로그인에 성공하면 설정된 경로로 포워딩 
    	.and()
    	  .logout()
    		.logoutUrl("/logout") 
    		.logoutSuccessUrl("/")
    		.deleteCookies("JSESSIONID") // 로그아웃시에 쿠키 값 삭제 
    		.invalidateHttpSession(true) // 세션무효화 
    	.and()
    	  .addFilterBefore(filter, CsrfFilter.class) //첫번째 인자보다 먼저 시작될 필터를 등록 
    		  .csrf().disable(); 
  }
}
```
    
    
    
    

그레이들에서 의존성 관리 제어를 위한 플러그인

    apply plugin: 'io.spring.dependency-management'