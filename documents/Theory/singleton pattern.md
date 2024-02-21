# 싱글톤 패턴(Singleton Pattern)
- 클래스에 하나의 인스턴스만을 생성해 사용하는, 유일한 객체를 만들기 위한 디자인 패턴
- 인스턴스 생성 이후에 해당 클래스의 생성자가 호출되더라도 최초 생성된 인스턴스만을 리턴한다.
- 전역 변수와 동일한 개념
- 데이터베이스 커넥션풀, 캐싱, 로그 등에 주로 사용된다.

## 장점
- 최초 하나의 메모리 영역을 할당 받고 인스턴스를 생성하기 때문에 메모리를 효율적으로 사용
- 여러개릐 인스턴스를 생성하지 않기 때문에 메모리 낭비 방지
- 공통된 값을 사용하는 상태 관리에 유리

## 단점
- 모듈간 의존성이 높아진다. 
- 이는 싱글톤 인스턴스의 내용이 변경된다면 이를 참조하는 모든 모듈들도 수정해야 된다는 의미이다.
- OOP SOLID 원칙에 위배되는 경우가 많다.
- 하나의 인스턴스만을 생성하고 때문에 단일 책임 원칙(SRP)에 위배
- 하나의 인스턴스를 많은 클래스가 참조하게되면 결합도가 높아져 개방 폐쇄 원칙(OCP)에 위배
- 싱글톤은 인터페이스나 추상클래스가 아닌 구체 클래스를 사용하기 때문에 의존 역전 원칙(DIP)에 위배
- TDD 단위 테스트가 어려움(전역으로 상태 공유를 하고 있기 때문에 테스트가 수행되려면 항상 인스턴스를 초기화 해야한다.)

## 예시
1. 지연 초기화(Thread-Safe Lazy Initialization)
```html
    public class SingleTon {

    private static SingleTon instance;
    
    private SingleTon() {}
    
    public static synchronized SingleTon getInstance() {
    	if(instance == null) {
            instance = new SingleTon();
    	}
    	return instance;
    }
```
위 코드는 Synchronized 키워드를 사용해 속도가 느리다.
Synchronized 키워드를 사용한 블록에는 다른 쓰레드에서 동시에 접근할 수 없다. 하나의 쓰레드만 접근 가능하다.

2. 지연 초기화 + 더블 체크(Thread-Safe Lazy Initialization + Double-Checked locking)
```html
    public class SingleTon {

    
    private static SingleTon instance;
    
    private SingleTon() {}
    
    public static SingleTon getInstance() {
    	if(instance == null) {
    		synchronized (SingleTon.class) {
				instance = new SingleTon();
			}
    	}
    	return instance;
    }
```
getInstance()에 synchronized를 사용하지 않고 instance가 null이 아닐 경우 synchronized를 사용하여 인스턴스를 생성
하지만 Synchronized를 사용했기 때문에 여전히 속도가 느리다.

3. holder에 의한 초기화(가장 많이 사용)
```html
    public class SingleTon {
        private SingleTon(){}

        private static class LazyHolder{
            public static final SingleTon INSTANCE = new SingleTon();
        }

        public static SingleTon getInstance(){
            return LazyHolder.INSTANCE;
        }
    }
```
2번과 같이 개발자가 직접 동기화 코드를 작성하면 신뢰성의 문제가 발생한다.

그래서 위와 같이 static inner class를 활용해 로딩 시점에 한번만 호출하고 final을 사용해 다시 인스턴스가 생성되지 않도록 한다.
Synchronized를 사용하지 않아 속도가 빠르다.