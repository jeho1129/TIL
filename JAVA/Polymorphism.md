# <center>TIL<center>

# 다형성 :memo:

1. **다형성**
  - 다형성(Polymorphism)은 이름 그대로 다양한 형태, 여러 형태를 뜻한다.
  - 프로그래밍에서 다형성은 한 객체가 여러 타입의 객체로 취급될 수 있는 능력을 뜻한다. 보통 하나의 객체는 하나의 타입으로 고정되어있다. 그런데 다형성을 사용하면 하나의 객체가 다른 타입으로 사용될 수 있다.
  - 다형적 참조
    ```java
    public class Parent {

        public void parentMethod() {
            System.out.println("Parent.parentMethod");
        }
    }
    ```
    ```java
    public class Child extends Parent {

        public void childMethod() {
            System.out.println("Child.childMethod");
        }
    }
    ```
    ```java
    public class PolyMain {

        public static void main(String[] args) {
            // 부모 변수가 부모 인스턴스 참조
            Parent parent = new Parent();
            parent.parentMethod();

            // 자식 변수가 자식 인스턴스 참조
            Child child = new Child();
            child.parentMethod();
            child.childMethod();

            // 부모 변수가 자식 인스턴스 참조(다형적 참조)
            Parent poly = new Child();
            poly.parentMethod();
            // 자식의 기능은 호출할 수 없다.(컴파일 오류 발생)
            // poly.childMethod();
            
            // 자식은 부모를 담을 수 없다.
            // Child child1 = new Parent();
        }
    }
    ```
    - 부모 타입의 변수가 부모 인스턴스 참조
      - Parent parent = new Parent();
      - Parent 인스턴스를 만들었다. 이 경우 부모 타입인 Parent를 생성했기 때문에 메모리 상에 Parent만 생성되고 자식은 생성되지 않는다.
      - 생성된 참조값을 Parent 타입의 변수인 parent에 담아둔다.
      - parent.parentMethod()를 호출하면 인스턴스의 Parent 클래스에 있는 parentMethod()가 호출된다.
    - 자식 타입의 변수가 자식 인스턴스 참조
      - Child child = new Child();
      - Child 인스턴스를 만들었다. 이 경우 자식 타입인 Child를 생성했기 때문에 메모리 상에 Child와 Parent가 모두 생성된다.
      - 생성된 참조값을 Child 타입의 변수인 child에 담아둔다.
      - child.childMethod()를 호출하면 인스턴스의 Child 클래스에 있는 childMethod()가 호출된다.
    - 다형적 참조 : 부모 타입의 변수가 자식 인스턴스 참조
      - Parent poly = new Child();
      - Child 인스턴스를 만들었다. 이 경우 자식 타입인 Child를 생성했기 때문에 메모리 상에 Child와 Parent가 모두 생성된다.
      - 생성된 참조값을 Parent 타입의 변수인 poly에 담아둔다.
      - 부모 타입은 자식 타입을 담을 수 있다.
      - Parent poly는 부모 타입이다. new Child()를 통해 생성된 결과는 Child 타입이다.
      - 반대로 자식 타입은 부모 타입을 담을 수 없다.
    - 자바에서 부모 타입은 자신은 물론이고, 자신을 기준으로 모든 자식 타입을 참조할 수 있다. 이것이 바로 다양한 형태를 참조할 수 있다고 해서 다형적 참조라 한다.
    - 다형적 참조와 인스턴스 실행
      - poly.parentMethod()를 호출하면 먼저 참조값을 사용하여 인스턴스를 찾는다. 그리고 다음으로 인스턴스 안에서 실행할 타입도 찾아야한다. poly는 Parent 타입이다. 따라서 Parent 클래스부터 시작해서 필요한 기능을 찾는다. 인스턴스의 Parent 클래스에 parentMethod()가 있기 때문에 해당 메서드가 호출된다.
    - 다형적 참조의 한계
      - poly.childMethod()를 호출하면 먼저 참조값을 사용하여 인스턴스를 찾는다. 그리고 다음으로 인스턴스 안에서 실행할 타입을 찾아야한다. poly는 Parent 타입이다. 따라서 Parent 클래스부터 시작해서 필요한 기능을 찾는다. 그런데 상속 관계는 부모 방향으로 찾아 올라갈 수는 있지만 자식 방향으로 찾아 내려갈 수는 없다. Parent는 부모 타입이고 상위에 부모가 없기 때문에 childMethod()를 찾을 수 없으므로 컴파일 오류가 발생한다.
      - 이런 경우 childMethod()를 호출하고 싶다면 캐스팅이 필요하다.

2. **다형성과 캐스팅**
  ```java
  public class CastingMain1 {

      public static void main(String[] args) {
          // 부모 변수가 자식 인스턴스 참조(다형적 참조)
          Parent poly = new Child();  // x001

          // 단, 자식의 기능은 호출할 수 없다.
          // poly.childMethod();

          // 다운캐스팅(부모 타입 -> 자식 타입)
          Child child = (Child) poly;  // x001
          child.childMethod();
      }
  }
  ```
  - 부모 타입을 사용하는 변수를 자식 타입에 대입하려고 하면 컴파일 오류가 발생한다.
  - 이 때는 다운캐스팅이라는 기능을 사용하여 부모 타입을 자식 타입으로 변경할 수 있다.
  - (타입)처럼 괄호와 그 사이에 타입을 지정하면 참조 대상을 특정 타입으로 변경할 수 있다. 이렇게 특정 타입으로 변경하는 것을 캐스팅이라고 한다.
  - 캐스팅을 한다고 해서 Parent poly의 타입이 변하는 것은 아니다. 해당 참조값을 꺼내고 꺼낸 참조값이 Child 타입이 되는 것이다. 따라서 poly의 타입은 Parent로 기존과 같이 유지된다.
  - 업캐스팅(Upcasting) : 부모 타입으로 변경
  - 다운캐스팅(Downcasting) : 자식 타입으로 변경