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