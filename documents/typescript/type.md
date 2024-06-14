# Typescript Interface & Type

## Interface
- 기본 사용법
    ```html
        interface User {
            name: string;
            age: number;
        }

        const user: User = {
            name: "John",
            age: 30
        };
    ```
- 확장 방법
    ```html
        interface Person {
            name: string;
        }

        interface Employee extends Person {
            employeeId: number;
        }

        const employee: Employee = {
            name: "John",
            employeeId: 123
        };
    ```
## Type
- 기본 사용법
    ```html
        type User = {
            name: string;
            age: number;
        };

        const user: User = {
            name: "John",
            age: 30
        };
    ```
- 확장 방법
    ```html
        type Person = {
            name: string;
        };

        type Employee = Person & {
            employeeId: number;
        };

        const employee: Employee = {
            name: "John",
            employeeId: 123
        };
    ```
## 공통점