## 
Google Api Console에서 새로운 프로젝트 생성
OAuth 동의화면
만들기
애플리케이션이름 적고 저장
사용자 인증정보
OAuth 클라이언트 ID만들기
	애플리케이션 유형 : 웹 어플리케이션
	이름
	승인된 리디렉션url : 구글 로그인이 완료가 되면 코드를 돌려줍니다. 그 코드를 받아서 엑세스 토큰을 받아서 사용자의 정보에 요청
	OAuth클라이언트를 사용하면 주소가 고정
	/login/oauth2/code 부분이 고정코드
	URI : http://localhost8080/login/oauth2/code/google
	이 주소에 대한 컨트롤러를 만들 필요가 없다. 라이브러리가 처리해주기 때문
	
생성되면 클라이언트 ID와 클라이언트 보안 비밀번호가 나오고 이 정보는 다른사람이 모르게 관리해야한다.

OAuth2라이브러리가 있다.
Mvnrepository.com -> OAuth2 Client

aplication properties -> security.oauth2.clinet.registraion.google.client-id = 
security.oauth2.clinet.registraion.google.client-secret =
security.oauth2.clinet.registraion.google.scope-email
security.oauth2.clinet.registraion.google.scope-profile

로그인폼에 버튼달기
링크 -> 고정
``` html
<a href ="/oauth2/authorization/google">구글 로그인</a>
```

securityConfig 에
``` java
.and()
.oauth2Login()
.loginPage();
```

추가 한다.


 이후 구글 로그인이 완료된 뒤의 후처리가 필요하다.
 - 코드받기(인증)
 - 엑세스 토큰(권한)
 - 사용자프로필 정보를 가져오고
	 - 그 정보를 토대로 회원가입을 자동으로 진행시키기도 함
 - 이메일, 전화번호, 이름, 아이디 (쇼핑몰) -> 집주소 백화점 -> vip, 일반회원 등 이외 정보가 필요하면 추가 정보를 입력시켜서 회원가입시킨다.
- 구글 로그인이 완료되면 코드를 받는게 아니라 엑세스토큰_+ 사용자 프로필 정보를 받는다


.userInfoEndPoint()
.userService() <-
DefaultOAuth2UserService 를 상속받는 객체가 들어가야함


## DefaultOAuth2UserService
loadUser

자바 스프링으로 스프링 시큐리티와 oauth를 사용한 웹 api 서비스를 만들려고하는데 고민이 있어. 
회원 테이블 설계를 하는중인데 
회원가입을 일반 회원가입(email), oauth회원 가입 두가지 경로로 만들고 싶고
문제가 되는 case는 두가지가 있어
		1. 이메일 회원가입 후 oauth 로그인 요청시 - oauth 인증 후 oauth 로그인 가능하도록
		2. oauth 회원가입시 이메일 회원가입시 - password 입력, 이메일 인증 후 이메일 로그인 가능
위 내용 처럼 구현하고 싶은데 db를 어떻게 짜면 효율적일지 고민하고있어

네가 정확히 아는 내용으로만 어떤식으로 짜면 효율직일지 설명해줘