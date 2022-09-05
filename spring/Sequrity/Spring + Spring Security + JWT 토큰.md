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


