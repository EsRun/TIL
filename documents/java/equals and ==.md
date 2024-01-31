# equals와 ==의 차이점

## 종류
- equals는 Object 클래스에서 제공하는 메소드이다.
- == 는 연산자이다.

## equals
- 기본적으로 참조 타입(Object 클래스의 메소드이기 때문)을 사용하기 때문에 메모리 값을 비교한다.
- 하지만 String 클래스는 equals()를 실제값과 비교하도록 재정의하였다.

## ==
- 원시 타입(int, Stinrg 등)에 사용할 경우 실제 값을 비교한다.
- 참조 타입(Object, Array 등)에 사용할 경우 메모리 주소 값을 비교한다.

## 예시(String 클래스의 equals() 메소드 사용 시)
```html
    String a = new String("hi");
    String b = new String("hi");
    System.out.println(a.equals(b)); // true
    System.out.println(a == b); // false
    
    String c = "hi";
    String d = "hi";
    System.out.println(c.equals(d)); // true
    System.out.println(c == d); // true

    System.out.println(a.equals(c)); // true, 실제 값을 비교하기 때문에 true(String 클래스에서 재정의한 equals()를 사용하기 때문에 실제 값을 비교)
    System.out.println(a == c); // false, 메모리 주소 값을 비교하기 때문에 false
```

## 예시(Object 클래스의 equals() 메소드 사용 시)
```html
    Dto e = new Dto("hi");
    Dto f = new Dto("hi");
    System.out.println(e.equals(f)); // false
    System.out.println(e == f); // false

    String dto = "hi";
    System.out.println(e.equals(dto)); // false, 메모리 주소 값을 비교하기 때문에 false(Object 클래스에서 정의한 기본 equals()를 사용하기 떄문에 메모리 주소 값 비교)
    System.out.println(e == dto); // false, 메모리 주소 값을 비교하기 때문에 false

```

## 차이점
```html
    String a = new String("hi");
    String b = new String("hi");
    String c = "hi";
    String d = "hi";
    Dto e = new Dto("hi");
    dto f = new Dto("hi");
```
- 위 코드에서 a와 b는 각각 heap 영역의 다른 메모리 주소를 가진 값을 생성한다.
- c와 d는 heap 영역의 String Constant Pool 영역에 "hi"라는 하나의 값을 가르키게 된다.
- e와 f는 heap 영역의 다른 메무리 주소를 가진 값을 생성한다.

## 결론
- String 클래스와 Object 클래스의 equals() 메소드는 다르다.
- String 클래스는 Object 클래스의 equals()를 오버라이딩 하여 실제 값을 비교하도록 재정의하였다.
- String 클래스는 실제 값을 비교하도록 구현되어 있고, Object 클래스는 메모리 주소 값을 비교하도록 구현되어 있다.
- 임의로 구현한 객체에서 Object 클래스의 equasl()를 재정의하여 사용하면 메모리 주소 값을 비교하는 것이 아닌 실제 값을 비교하도록 구현할 수 있다.