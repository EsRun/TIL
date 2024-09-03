# object copy

## 얕은 복사(Shallow Copy)
- 참조 객체가 원본 객체의 메모리 주소값을 저장한다.
- 원본 객체의 첫 번째 레벨만 복사하며, 그 속성들은 원본 객체와 동일한 참조를 한다.
- 깊은 복사에 비해 훨씬 속도가 빠르다.
- 상태 공유에 사용하기 적절하다.

```html
    // 원본 객체
    const originalObj = {
        name: "Alice",
        age: 25,
        address: {
            city: "Wonderland",
            zip: "12345"
        }
    };

    // 얕은 복사
    const shallowCopy = { ...originalObj };

    // 객체 수정
    shallowCopy.address.city = "New Wonderland";

    // 결과
    console.log(originalObj.address.city);  // "New Wonderland" - 원본 객체도 수정됨
    console.log(shallowCopy.address.city);  // "New Wonderland"
```

## 깊은 복사(Deep Copy)
- 참조 객체가 원본 객체의 모든 속성을 완전히 복사한다.
- 복사된 객체는 원본 객체와 동일한 값을 갖지만, 얕은 복사와는 다르게 완전히 다른 메모리 주소를 할당 받는다.
- 데이터의 독립성 보장 및 무결성 유지

```html
    // 원본 객체
    const originalObj = {
        name: "Alice",
        age: 25,
        address: {
            city: "Wonderland",
            zip: "12345"
        }
    };

    // 깊은 복사
    const deepCopy = JSON.parse(JSON.stringify(originalObj)); // 방법1
    const deepCopy = structuredClone(originalObj); // 방법 2

    // 객체 수정
    deepCopy.address.city = "New Wonderland";

    // 결과
    console.log(originalObj.address.city);  // "Wonderland" - 원본 객체는 그대로 유지됨
    console.log(deepCopy.address.city);     // "New Wonderland"
```

### 얕은 복사, 깉은 복사 차이점
- 얕은 복사는 성능이 좋지만 객체를 참조하기 때문에 예상치 못한 버그가 발생할 수 있다.
- 깊은 복사는 복사로 인한 버그 발생확률이 없으나, 메모리와 시간이 더 소요된다.
- 결론적으로 얕은 복사는 객체의 일부만 변경할 경우, 깊은 복사는 객체의 독립성을 유지하고 싶을 경우 사용한다.