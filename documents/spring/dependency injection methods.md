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
### 생성자 주입을 추천하는 이유

1. 순환 참조를 방지할 수 있다.
- 아래와 같이 필드, 수정자 주입 사용 시 컴파일 시 오류가 발생하지 않으나, 런타임 시 오류 발생
- 하지만 생성자 주입은 의존 관계 주입이 일어나기 때문에 객체의 생성자가 실행될 때 의존 객체의 null 여부를 검사해 컴파일 시 오류를 발생, 에러 방지에 효과적

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

2. 불변성을 보장한다.
- 아래와 같이 생성자 주입은 final 선언이 가능하여, 런타임 시 의존성을 주입받는 객체가 변하는 일이 없어진다. 즉 불변성을 보장하는 것이다.
- 하지만 수정자/필드 주입을 하게되면 수정을 가능성이 생기고, 이는 OOP 5가지 원칙 중 OCP(Open-Closed Principal, 개방-폐쇄의 원칙)을 위반한다.
- 또한 final 선언 시 선언 자체(예. private final declare de = null)나 생성자에서 초기화를 진행해야 한다.
- 그러나 수정자/필드는 final 선언을 할 수 없다. 정확히 말하면 초기값을 부여하여 사용할 수는 있지만 이는 final 사용의 목적, 불변성에 위배된다.

```html
    
    public class consController{
        
        private final consService service; // 정상 작동

        @Autowired
        public consController(consService service){
            this.service = service;
        }
    }

    public class consController{
        
        @Autowired
        private final consService service; // The blank final field service may not have been initialized 에러 발생

    }

    public class consController{
        
        private final consService service;

        @Autowired
        public setConsService(consService service){
            this.service = service; // The final field consController.service cannot be assigned 에러 발생
        }
    }

```