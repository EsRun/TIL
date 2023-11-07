# typescript

## 타입 선언 시 대소문자 구분

- **string, number 와 String, Number 차이점**

  ```html
  const caseTest = (select: Number) => { console.log(select); };
  ```

  위 구문 실행 시
  Type 'Number' cannot be used as an index type.ts(2538)
  에러 발생

  number는 primitive type으로 문자열 타입이고 Number는 object type으로 생성자 함수를 통해 생성하는 객체 타입이다.
  Number 타입에는 number 타입을 할당할 수 있지만 number 타입에는 Number 타입을 할당할 수 없다.(number는 원시 타입이고 Number는 객체 타입이기 때문에)
