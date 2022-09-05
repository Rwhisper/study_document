
# StringBuilder
- 자바에서 String객체끼리 더하는 것은 메모리 할당과 해제를 발생시키는데  덧셈연산이 많아진다면 성능적으로 좋지 않다.  
- 이를 해결하기 위해서 StringBuilder를 사용한다.


Integer.toString 함수를 Integer.toString(int i, int radix) 형태로 사용하게 되면 i를 radix에 해당하는 진법으로 변환할 수 있다
```java
str.append(Integer.toString(i, n));
```

### append
문자열 더하기
```java
StringBuilder str = new StringBuilder();
str.append("test");
```

Inte