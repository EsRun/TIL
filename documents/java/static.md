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