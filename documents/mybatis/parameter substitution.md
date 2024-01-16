# mybatis 매개변수 치환 처리

## 종류
- #{} : 문자열 치환(String Substitution)
- ${} : 매개변수 치환(Parameter Substitution)

### 문자열 치환(String Substitution)
```html
    1. xml Mapper
    SELECT * FROM Spring WHERE ID = #{ID}

    2. Mysql
    SELECT * FROM Spring WHERE ID = ?

    3. 실행 시 
    SELECT * FROM Spring WHERE ID = 'spring'
```

### 매개변수 치환(Parameter Substitution)
```html
    1. xml Mapper
    SELECT * FROM Spring WHERE ID = ${ID}

    2. Mysql
    SELECT * FROM Spring WHERE ID = ?

    3. 실행 시 
    SELECT * FROM Spring WHERE ID = spring
```

### 차이점
1. #{}
- 값에 ''가 자동으로 붙음(문자 타입으로 처리)
- PreparedStatement(자바의 Statement를 상속받은 인터페이스)를 통해 SQL Injection 예방
- 주로 사용자의 입력값을 전달할 때 사용(WHERE이나 AND 같은 조건 구문)


2. ${}
- 값에 ''가 붙지 않음(원본 데이터 그대로 출력)
- Statement를 사용해 SQL Injection 취약
- 주로 동적 테이블 명이나 컬럼명에 사용(파라미터를 테이블이나 컬럼명으로 사용하는 경우)