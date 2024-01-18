# 스프링 의존성 주입 방법

## 종류
- 생성자 주입(Contructor Injection)
- 필드 주입(Field Injection)
- 수정자 주입(Setter Injection)

## 생성자 주입(Contructor Injection)
```html
    @Controller
    public class consController{
        
        private final consService service;

        @Autowired
        public consController(consService service){
            this.service = service;
        }
    }
```

## 필드 주입(Field Injection)
```html
    @Controller
    public class fieldController{

        @Autowired
        private fieldService service;
    }
```

## 수정자 주입(Setter Injection)
```html
    @Controller
    public class setContorller{
        
        private setService service;

        @Autowired
        public void setSetService(setService service){
            this.service = service;
        }
    }
```

## 요약
- 생성자 주입을 추천하는 이유

```html
    
    @Service
    public class aService {

        @Autowired
        private bService b;
        
        public void aa() {
            b.bb();
        }
    }
```

```html
    @Service
    public class bService {

        @Autowired
        private aService a;
        
        public void bb() {
            a.bb();
        }
    }
```
- 위와 같이 필드, 수정자 주입 사용 시 컴파일 시 오류가 발생하지 않으나, 런타임 시 오류 발생
- 하지만 생성자 주입은 의존 관계 주입이 일어나기 때문에 객체의 생성자가 실행될 때 의존 객체의 null 여부를 검사해 컴파일 시 오류를 발생, 에러 방지에 효과적