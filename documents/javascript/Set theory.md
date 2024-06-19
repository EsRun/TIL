# Set 개념
- 고유만 값들의 Collection
- 고유한 값만 저장 : Set 객체는 중복 값을 허용하지 않는다. 동일한 값은 하나만 저장된다.
- 객체 중복 처리 : 같은 내용의 객체라도 다른 객체로 인식, 동일한 객체 참조만 중복으로 인정한다.
- 대소문자 구분 : 대소문자를 구분하여 같은 문자열의 대소문자가 다를 경우 다른 값으로 인정한다.

## 예시

- 고유한 값만 저장
```javascript
const emptySet = new Set();
console.log(emptySet); // Set(0) {}

const letters = new Set(['A', 'B', 'C', 'D', 'E', 'C']);
console.log(letters); // Set(5) { 'A', 'B', 'C', 'D', 'E' }

const charSet = new Set('HELLO');
console.log(charSet); // Set(4) { 'H', 'E', 'L', 'O' }
```

- 대소문자 구분
```javascript
const word = new Set(['hello']);
console.log(word.has('hello')); // true
console.log(word.has('HELLO')); // false
console.log(word.has('Hello')); // false
```

- 객체 중복 처리
```javascript
const obj = new Set();
const obj1 = { oo: 1};
const obj2 = { oo: 1};
obj.add(obj1);
obj.add(obj2);
console.log(obj); // Set(2) { {oo: 1}, {oo: 1}}

const objectSet = new Set([
  { name: 'Alice', company: 'Google' },
  { name: 'Bob', company: 'Apple' },
  { name: 'Charlie', company: 'Microsoft' },
  { name: 'Alice', company: 'Google' },
  { name: 'Eve', company: 'Amazon' }
]);
console.log(objectSet);
/* Set(5) {
  { name: 'Alice', company: 'Google' },
  { name: 'Bob', company: 'Apple' },
  { name: 'Charlie', company: 'Microsoft' },
  { name: 'Alice', company: 'Google' },
  { name: 'Eve', company: 'Amazon' }
} */
```

## 속성
```javascript
const companies = new Set(['Google', 'Apple', 'Microsoft', 'Amazon', 'Facebook']);
```

- 추가 : Set.add(value)
```javascript
companies.add('Tesla');
console.log(companies); // Set(6) { 'Google', 'Apple', 'Microsoft', 'Amazon', 'Facebook', 'Tesla' }
```

- 삭제 : Set.delete(value)
```javascript
companies.delete('Apple');
console.log(companies); // Set(5) { 'Google', 'Microsoft', 'Amazon', 'Facebook', 'Tesla' }
```

- 존재 여부 확인 : Set.has(value)
```javascript
const isChecked = companies.has('Tesla');
console.log(isChecked); // true
```

- 갯수 확인 : Set.size
```javascript
const checkSize = companies.size;
console.log(checkSize); // 5
```

- 전체 삭제 : Set.clear()
```javascript
companies.clear();
console.log(companies); // Set(0) {}
```