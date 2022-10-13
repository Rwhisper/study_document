## Security 의존성 주입
시큐리티 사용을 위해  Security 의존성 주입을 해준다.
> implementation 'org.springframework.boot:spring-boot-starter-security:2.7.3'



## 1. SecurityConfig
- 시큐리티를 사용하기 위해서는 security 필터를 등록해 주어야 한다.
- SecurityConfig 설정 파일에 HttpSecurity를 받아 SecurityFilterChain를 반환하는 빈 객체를 등록해준다.

####  SecurityFilterChain
``` java
protected SecurityFilterChain filterChain(HttpSecurity http) throws Exception {

	http.csrf().disable(); 
	
	http.authorizeRequests()
	
	.antMatchers("/user/**").authenticated()
	
	//.antMatchers("/admin/**").access("hasRole('ROLE_ADMIN') or hasRole('ROLE_USER')")
	
	//.antMatchers("/admin/**").access("hasRole('ROLE_ADMIN') and hasRole('ROLE_USER')")
	
	.antMatchers("/admin/**").access("hasRole('ROLE_ADMIN')")
	
	.anyRequest().permitAll()
	
	.and()
	
	.formLogin()
	
	.loginPage("/login")
	
	.loginProcessingUrl("/loginProc")
	
	.defaultSuccessUrl("/")
	
	.and()
	
		.oauth2Login()
		
		.loginPage("/login")
		
		.userInfoEndpoint()
		
		.userService(principalOauth2UserService);

}
```

### BCryptPasswordEncoder 빈 객체 생성 
- 패스워드 암호화를 위한 BCryptPasswordEncoder 객체 생성
``` java
@Bean

public BCryptPasswordEncoder encodePwd() {

return new BCryptPasswordEncoder();

}
```


