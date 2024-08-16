# Typescript Interface & Type

## Interface

- 기본 사용법

  ```html
  interface User { name: string; age: number; } const user: User = { name:
  "John", age: 30 };
  ```

- 확장 방법

  ```html
  interface Person { name: string; } interface Employee extends Person {
  employeeId: number; } const employee: Employee = { name: "John", employeeId:
  123 };
  ```

## Type

- 기본 사용법

  ```html
  type User = { name: string; age: number; }; const user: User = { name: "John",
  age: 30 };
  ```

- 확장 방법

  ```html
  type Person = { name: string; }; type Employee = Person & { employeeId:
  number; }; const employee: Employee = { name: "John", employeeId: 123 };
  ```

## 공통점

- 상속 가능

## 다른점

### type alias(타입 별칭)

- 유니언( | ) 사용 가능
- 모든 타입에 대해서 alias를 지어줌

### interface

- 객체에만 alias를 지어줌
- 동일한 인터페이스를 여러 번 선언(확장)할 수 있음
- 동일한 선언이 가능하기 때문에 라이브러리의 인터페이스를 수정할 수 있음

```html
  interface gpt{ 
    id: number; 
  } 
  interface gpt{ 
    name: string;
  }
  위 같이 동일한 인터페이스를 여러 번 선언할 수 있고, 선언 시 아래와 같은 효과를 가짐
  interface gpt{
    id: number; name: string;
  }
```
