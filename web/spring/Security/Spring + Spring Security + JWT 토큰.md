# Gradle 의존성 추가
	
> security , jpa, jwt, validation 의존성 추가 (lombok, web , db 관련 의존성 생략)
>``` java
// jpa  
implementation 'org.springframework.boot:spring-boot-starter-data-jpa'  
// security  
implementation 'org.springframework.boot:spring-boot-starter-security'  
// 유효성 검증  
implementation 'org.springframework.boot:spring-boot-starter-validation'
// jwt  
implementation group: 'io.jsonwebtoken', name: 'jjwt-api', version: '0.11.5'  
runtimeOnly group: 'io.jsonwebtoken', name: 'jjwt-impl', version: '0.11.5'  
runtimeOnly group: 'io.jsonwebtoken', name: 'jjwt-jackson', version: '0.11.5'




# Security 설정
## Security config 파일 생성
security 설정을 위해 config 파일을 생성합니다.

config라는 패키지를 만들고 SecurityConfig라는 java파일을 만듭니다.

기존에는 `WebSecurityConfigurerAdapter` 를  상속받아 설정을 오버라이딩 하는 방식이었는데 스프링이 버전업 됨에 따라서  `WebSecurityConfigurerAdapter` 등 몇가지가 Deprecated 되었습니다.
바뀐 버전에서는 상속받아 오버라이딩하지 않고 Bean으로 등록해서 사용한다고한다.
 ~~(이부분 때문에 이전 강의들과 현재와 달라서 매우 헤맸다)~~

이전코드
``` java
@Override
public void configure(WebSecurity web) {
	web.ignoring().antMatchers("/assets/**", "/h2-console/**");
}	
```

바뀐코드
```java
@Bean  
public WebSecurityCustomizer webSecurityCustomizer() {  
    return (web) -> web.ignoring().antMatchers("/h2-console/**"  
            , "/favicon.ico"  
            , "/error", "/api/test");  
}
```


## Security config 설정하기

#### 설정들
- formLogin() : 폼 로그인으로 설정
- loginPage() : 로그인 페이지의 주소
- loginProcessingUrl() : 해당 url으로 로그인 요청이오면 시큐리티가 낚아채서 대신 로그인을 진행한다.
- defaultSuccessUrl() : 로그인이 성공하면 보여줄 페이지 
	- defaultSuccessUrl("/") 으로 설정하게 되면 특정페이지에서 로그인하게되면 그 페이지로 다시 보내준다.


### Security 로그인 진행 방식
- 시큐리티가 loginProcessingUrl에 요청이 오면 낚아 채서 로그인을 진행시킨다
- 로그인 진행이 완료되면 시큐리티 session을 만들어준다(Security ContextHolder)
- 오브젝트타입 =>  Authentication 타입 객체
- Authentication 안에 User 정보가 있어야 됨
- User 오브젝트 타입 => UserDetails

- Security Session => Authentication => UserDetails




## UserDetailsService 
loginProcessingUrl 요청이 오면 자동으로 UserDetailsService타입으로 IoC 되어있는 loadByUsername 함수가 자동으로 실행 됩니다.

###  loadByUsername 
- 파라미터로 의 파라미터로 username을 받는다 이 유저네임과 form에서 유저의 id의 name과 이름을 맞춰주어야 하는데 만약 이 값을 다르게 하고 싶다면 SpringConfig 파일에 userParameter()에 바뀐 이름을 넣어주면 된다.
- 여기에 UserDetils를 상속받은 User객체를 리턴하게 해주면된다.
- 성공하면 Authentication 객체에 UserDetails객체가 들어가게 된다.
-

## @Secured() 어노테이션
- 특정 메서드에 ()안의 권한을 가지고있는 유저만 접근 가능하도록하는 어노테이션 입니다.
- SecurityConfig의 @EnableGlobalMethodSecurity()어노테이션 안에 securedEnabled=true 추가해서 활성화 한다.


## @PreAuthorize() 어노테이션
- 두가지 이상의 권한에게 접근시킬때 사용하는 어노테이션입니다.
- SecurityConfig의 @EnableGlobalMethodSecurity()어노테이션 안에 prePostEnabled = true 추가해서 활성화 한다.
- @PreAuthorize("hasRole('ROLE_MANAGER') or hasRole('ROLE_ADMIN')")
