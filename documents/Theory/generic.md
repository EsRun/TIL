# Generic

## 개념

- 어떤 자료구조를 만들어 배포하려고 할 때 String도 쓰고싶고 Integer도 쓰고 싶은데 데이터 타입마다 클래스를 만든다면 너무 비효율적.
- 이런 문제를 해결하기 위해 Generic을 사용
- Generic은 클래스 내부에서 지정하는 것이 아닌 외부에서 사용자에 의해 지정되는 것을 의미
- 한마디로 특정 타입을 미리 지정해주는 것이 아닌 필요레 의해 지정할 수 있도록 하는 일반(Generic) 타입이다.

```html
List list = new ArrayList(); -> 도형 list = new 정사각형(); ArrayList list = new
ArrayList(); -> 정사각형 list = new 정사각형();
```
