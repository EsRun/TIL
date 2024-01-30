# OOP 5원칙(The 5 SOLID principles)

## 종류
- 단일 책임 원칙(SRP, Single Responsibility principle)
- 개방/폐쇄 원칙(OCP, Open Closed Principle)
- 리스코프 대체 원칙(LSP, Liscov Substitution Principle)
- 인터페이스 분리 원칙(ISP, Interface Sergregation Principle)
- 종속성 역전 원칙(DIP, Dependency Inversion Principle)

### 단일 책임 원칙(SRP)
- 클래스에는 변경 이유가 하나만 있어야 한다.
- 클래스에는 하나의 책임이나 작업만 있어야 한다.
- 이유 : 유지 관리성 향상, 코드 수정 시 의도하지 않은 버그 발생률 감소

### 개방/폐쇄 원칙(OCP)
- 객체의 확장(기능 추가, 변경)은 개방적으로, 수정(원본 코드 수정)은 폐쇄적으로 한다.
- 객체의 기능이 변경되거나 추가되는 것은 가능하지만, 기존 코드는 수정되지 않아야 한다.

### 리스코프 대체 원칙(LSP)
- 부모를 상속하는 객체는 부모를 완전히 대체할 수 있어야 한다.

```html
- 직사각형을 만드는 객체를 정사각형을 만드는 객체에 상속받아 사용할 경우 X(직사각형과 정사각형은 바람직한 상속 관계가 성립되지 않는다.)
- 사각형 객체를 만들고, 이를 상속받는 직사각형, 정사각형 객체를 사용하는 경우 O
```

### 인터페이스 분리 원칙(ISP)
- 객체는 자신이 사용하는 메소드에만 의존해야 한다.
- 객체는 자신에게 필요한 기능만을 가지도록 제한한다.

```html
abstract public class Phone{
    
    public void Galaxy(){
        System.out.println("갤럭시");
    }
    public void GalaxyOs(){
        System.out.println("갤럭시 OS");
    }

    public void Iphone(){
        System.out.println("아이폰");
    }
    public void IphoneOs(){
        System.out.println("아이폰 OS");
    }
}
```
- 위 객체를 상속받아 사용하는 경우
```html
    public class Samsung extends Phone{

        @Override
        public void Galaxy(){
            Todo...
        }
        @Override
        public void GalaxyOs(){
            Todo...
        }

        @Override
        public void Iphone(){ // 불필요
            Todo...
        }
        @Override
        public void IphoneOs(){ // 불필요
            Todo...
        }
    }
```
- ISP 적용한 코드
```html
    public interface galaxy(){
        public void galaxy();
    }
    public interface galaxyOs(){
        public void galaxyOs();
    }
    public interface iphone(){
        public void iphone();
    }
    public interface iphoneOs(){
        public void iphoneOs();
    }
```

### 의존성 역전 원칙(DIP)
- 상위 모듈(비즈니스 로직)은 하위 모듈(데이터베이스 액세스)의 구현에 의존해서는 안된다.
- 둘다 추상화에 의존해야 한다.
- 상위 모듈 : interface, abstract class
- 하위 모듈 : mainClass, class
- 상위 모듈 -> 하위 모듈 X
- 하위 모듈 -> 추상화 계층 <- 하위 모듈

```html
    public class User{
        private Fps game;

        public void setGame(Fps game){
            this.game = game;
        }

        publid void start(){
            System.out.println(game.toString());
        }
    }
```
- 위 클래스를 사용하는 경우
```html
    public class Main{
        public static void main(String[] args){
            Fps fps = new Fps();
            User user = new user();
            user.setGame(fps);
            user.start();
        }
    }
```
위 코드에서 Game 클래스는 Fps라는 객체에 의존하고 있다. 이런 경우 Game의 종류가 변경됐을 때 Game 클래스를 수정해야 한다.
의존 상태 : Game -> Fps, Game -> Rpg
```html
    public class User{
        private Fps game;
        private Rpg game2;

        // 게임의 종류 만큼 Game 클래스 내에 메소드가 있어야 된다.
        public void setGame(Fps game){
            this.game = game;
        }
        publid void setGame2(Rpg game2){
            this.game2 = game2;
        }

        publid void start(){
            System.out.println(game.toString());
        }
    }
```
- DIP 적용한 코드
```html
    public class User{
        private Game game;

        public void setGame(Game game){
            this.game = game;
        }

        publid void start(){
            System.out.println(game.toString());
        }
    }
```
- User 내에서 게임 객체를 생성하지 않고, Game이라는 추상 클래스를 상속받아 구현하여 사용한다.

