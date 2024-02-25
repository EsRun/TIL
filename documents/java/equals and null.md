# equals 사용 시 예외처리

## 예시
```html
    String text = null;

    1. !text.equals(""); // java.lang.NullPointerException 발생
    2. !"".equals(text); // true
    3. StringUtils.isEmpty(text); // true

    2,3을 주로 사용한다.
```

## !"".equals() / StringUtils.imEmpty() 사용 이유
- 문자열 비교를 위해 equals 사용할 경우 non-null String 기준으로 비교하는 것이 좋다.
- 비교의 주체로 문자열을 사용하는 것이 null로 인한 에러 방지에 효과적이다.