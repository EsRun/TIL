# 클로저 개념

## MDN에서의 정의
```html
    “A closure is the combination of a function and the lexical environment within which that function was declared.”
    클로저는 함수와 그 함수가 선언됐을 때의 렉시컬 환경(Lexical environment)과의 조합이다.
```

## 예시
```html
    function increaseCount() {
        let count = 0;

        return function() {
            return count++;
        };
    }

    let countA = increaseCount();
    let countB = increaseCount();

    console.log(countA()); // 0
    console.log(countA()); // 1
    console.log(countA()); // 2
    console.log(countB()); // 0
    console.log(countB()); // 1

    결과를 보면 변수 countA와 countB는 각각 독립적인 함수를 갖는다.
    일반적으로 increaseCount() 함수가 실행되고 난 후 변수 count는 increaseCount() 함수와 함께 소면된다.
    하지만 변수 countA 에는 return function()의 return count++가 저장된다.
    자신이 선언 돼었을 때의 범위(function increaseCount())를 기억해 호출 후에도 범위(function increaseCount(){let count = 0}) 안의 변수(let count)에 접근할 수 있는 개념
```

## 간단 정리
- 자신이 선언됐을 때의 범위(scope) 밖에서 호출 되어도 그 범위(scope)에 접근할 수 있는 함수
- 클로저는 내부 함수가 외부 함수의 맥락(context)에 접근할 수 있는 것을 가르키는 개념
