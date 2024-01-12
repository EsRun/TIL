# 자바스크립트 엔진(v8)의 콜스택, 힙 개념

## Call Stack
- 원시 타입(primitive type, string / number / boolean / null 등)과 실행 컨텍스트(실행할 코드에 제공할 정보들을 담은 객체)가 저장된다.

## Memory Heap
- 참조 타입(reference type, object / array / function / date 등)이 저장된다.
- 동적으로 데이터를 할당할 수 있는 메모리 영역

## 예시
### Call Stack
|변수명|주소|값(Heap 주소)|
|------|---|---|
|aaa|10FF0000|55|
|bbb|10FF0001|1F0F00F1|
|ccc|10FF0010|1F0F0010|
|ddd|10FF0000|1F0F00F0|

### Memory Heap
|주소|값|
|---|---|
|1F0F00F0|10|
|1F0F00F1|['a', 'b', 'c']|
|1F0F0010|function(..){}|

위 예시를 보면 변수 aaa(원시 타입)의 값 Call Stack에 저장 되지만, 나머지 변수 3개의 값 Memory Heap에 저장된다.

두가지 타입 모두 변수(aaa, bbb, ccc, ddd) 자체는 Call Stack의 실행 컨텍스트의 렉시컬 환경에 저장된다.

하지만 원시 타입의 값은 Call Stack의 실행 컨텍스트에 저장되고,
참조 타입의 값은 Call Stack 에 Memory Heap 주소가 저장되고, 실제 값은 Memory Heap의 값에 존재한다.

