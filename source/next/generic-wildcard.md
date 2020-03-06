제네릭함수와 와일드카드 정의와 사용법
제네릭함수 예시

여러 가지의 API를 호출하고 그 로그를 기록을 해야하는데 그 정보를 담는 객체들이 RequestBean을 상속받는다.
객체가 10개면 service단에 insert 메서드 10개 mapper에 10개 만들어서 쿼리랑 연결해줘야하는데
아래 메서드를 이용하면 서비스단에는 메서드 한개만 있으면 된다.
단 아래 메서드를 쓰기위해서는 조건이 필요하다.
mapper에 존재하는 메서드의 이름은 insert + 파라미터객체명 + Log 이여야 한다.

```java
public <T extends RequestBean> void insertRequest(T t) {
// T extends RequestBean 으로 인해 파라미터로는 RequestBean을 상속받은 객체만 가능
  try {
    // 객체의 이름을 가져와 문자열 생성
    String methodName = "insert" + t.getClass().getSimpleName() + "Log";
    
    //mapper에서 위에서 만든 문자열의 메서드를 찾아온다
	  Method method = mapper.getClass().getMethod(methodName, t.getClass());
    
    //메서드 실행 (insert 진행)
    method.invoke(mapper, t);
   } catch (IllegalAccessException | IllegalArgumentException | InvocationTargetException | NoSuchMethodException | SecurityException e){
		log.debug(e.getMessage());
  }
}
```

위 예시에서는 extends RequestBean의 의미가 크게 없지만 extends를 설정해줌으로 RequestBean에 있는 메서드도 사용이 가능하다.
만약 extends 없이 메서드를 사용한다면 RequestBean을 상속받은 객체만 파라미터로 온다해도 위 메서드 안에서 RequestBean에 있는
메서드를 사용한다면 에러가 날것이다.

```java
public <T extends Test> void insertRequest(T t) {
  try {
    
   } catch (IllegalAccessException | IllegalArgumentException | InvocationTargetException | NoSuchMethodException | SecurityException e){
		log.debug(e.getMessage());
  }
}
```
