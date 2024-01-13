# let, const 재할당 개념

```html
let myArray = [];
const myArray = [];
```
두개의 선언 키워드 모두 Memory Heap에 주소가 저장된다.
하지만 위와 같은 배열 변수를 선언했을 경우 const를 사용하는 것을 추천한다.

- const로 선언된 배열에 요소 추가
```html
const arr = ['a', 'b', 'c'];
arr.push('d');
console.log(arr); // ['a', 'b', 'c', 'd']
```

- const로 선언된 객채에 속성 추가 / 변경
```html
const obj = { a: 1, b: 2 };
obj.c = 3;
obj.a = 5;
console.log(obj); // { a: 5, b: 2, c: 3 }
```

하지만 const로 선언된 배열이나 객체를 참조하려고 하면 에러가 발생한다.
```html
const arr = ['a', 'b', 'c'];
const arr2 = [];
arr = arr2; // Error : Assignment to constant variable.

const obj = { a: 1, b: 2 };
const obj2 = { c: 3, d: 4 };
obj = obj2; // Error : Assignment to constant variable.
```

const는 변수 자체를 불변으로 만드는 것이 아니라 변수가 참조하는 값의 변경을 막는다.

위 const 선언 시 발생하는 에러가 let을 사용하게 되면 모두 정상적으로 작동한다.
하지만 const사용을 추천하는 이유가 있다.

첫째. 실수로 인한 재할당을 방지
둘째. 코드의 명확성 향상
셋째. 불변성 확보로 인한 에러 방지

