" Entity는 Controller, Client단에서 쓰이면 직접 쓰이면 좋은 설계가 아니다.

Entity를 DTO로 바꿔 사용해야한다.  " 라고 블로그에 적혀있었다.

왜 일까 궁금해서 정리한 내용을 적어보려한다.

## Entity 
> DB에 저장하기 위해 유저가 정의한 클래스 (Domain)
> 실제 RDBS 테이블과 매칭되는 클래스

@Id 
PrimaryKey를 가지는 변수를 선언한다.
@GeneratedValue을 사용하여 어떻게 id값을 자동으로 생성할지 설정 할 수있다.

  
@Column어노테이션을 사용하지 않는다면 DB컬럼 명과 변수명이 일치하는 것끼리 기본적으로 매핑되지만 서로 다르게 설정하고 싶다면 @Column(name="컬럼명")을 사용하여 설정을 한다.

## DTO
데이터 전송 객체
DB에서 데이터를 얻어 Service나  Controller등으로 보낼때 사용하는 객체

Request, Response등

DTO class에 toEntity 함수를 정의해서 entity로 바꿀수 있다.  (DB에 등록할때 쓰인다)

Dto class에 생성자를 만들때 파라미터를 entity로 넣으면서 매핑된 Dto를 만들수 있다. (DB를 조회할때 쓰임)

*Entity는 Setter를 만들면 안된다고한다.

Setter를 무분별하게 사용하다보면 여기저기서 entity값을 변경할수 있기 때문에 일관성을 보장할수 없다.

의미있는 변경 메소드이름을 사용한다.