# Staitc

## 개념
- 프로그램 종료 시까지 메모리에 할당되어 사라지지 않는 전역 변수와 비슷한 개념

## static 변수
```html
    class Main {
        public static void main(String[] args) {
            staticField st1 = new staticField();
            staticField st2 = new staticField();
        }
    }

    class staticField {
        int count = 0; // 메소드 생성을 할 때마다 "새로운 메모리" 주소를 생성
        static int count2 = 0; // 메소드 생성을 할 때마다 "동일한 메모리" 주소를 사용
        staticField(){
            count++;
            count2++;
            System.out.println(count); // 1, 1 출력
            System.out.println(count2); // 1, 2 출력
        }
    }
```
- static이 붙은 count2는 동일한 메모리 주소에 저장된 값을 사용하기 때문에 1, 2 가 출력되는 것이고
- static이 없는 count는 서로 다른 메모리 주소에 저장된 값을 사용하기 때문에 1, 1이 출력되는 것이다.
- 메모리 효율 또는 공유의 목적으로 많이 사용한다.

## static 메소드
```html
    class Main {
        public static void main(String[] args) {
            staticField st1 = new staticField();
            staticField st2 = new staticField();
            
            System.out.println(staticField.getCount()); // static 메소드는 객체 생성 없이 메소드 호출을 할 수 있다.
        }
    }

    class staticField {
        int count = 0;
        static int count2 = 0;
        staticField(){
            count++;
            count2++;
            System.out.println(count);
            System.out.println(count2);
        }

        public static int getCount(){
            return count; // non-static variable count cannot be referenced from a static context return count; 에러 발생
            return count2; // static 메소드 안에서는 static 변수만 접근이 가능하다.
        } 
    }
```
- static 메소드에는 static 변수만 사용할 수 있다.
- 특정 클래스/인스턴스에 종속되지 않고 공통 기능에 주로 사용된다.

## 싱글톤과 스태틱 차이점
- JVM에 100개의 멀티 쓰레드가 있을 경우 싱글톤은 쓰레드 갯수 만큼 생성되지만
- 스태틱 오브젝트는 JVM에 단 한개만 생성되고 100개의 쓰레드가 공유한다.