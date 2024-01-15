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

3. **캐스팅의 종류**
  - 일시적 다운캐스팅
    - 자식 타입의 기능을 사용하기 위해서는 다운캐스팅 결과를 변수에 담아두고 이후에 기능을 사용한다.
    - 하지만 다운캐스팅 결과를 변수에 담아두는 과정 없이 일시적으로 다운캐스팅을 해서 인스턴스에 있는 하위 클래스의 기능을 바로 호출할 수 있다.
    - 예시
      ```java
      public class CastingMain2 {

          public static void main(String[] args) {
              Parent poly = new Child();
              // 일시적 다운캐스팅 - 해당 메서드를 호출하는 순간만 다운캐스팅
              ((Child) poly).childMethod();
          }
      }
      ```
      - poly는 Parent 타입이다. 그런데 이 코드를 실행하면 Parent 타입을 임시로 Child로 변경한다. 그리고 메서드를 호출할 때 Child 타입에서 찾아서 실행한다.
      - 정확히는 poly가 Child 타입으로 바뀌는 것은 아니다.
      - 참고로 캐스팅을 한다고 해서 Parent poly의 타입이 변하는 것은 아니다. 해당 참조값을 꺼내고 꺼낸 참조값이 Child 타입이 되는 것이다. 따라서 poly의 타입은 Parent로 그대로 유지된다.
      - 이렇게 일시적 다운캐스팅을 사용하면 별도의 변수 없이 인스턴스의 자식 타입의 기능을 사용할 수 있다.
  - 업캐스팅
    - 다운캐스팅과 반대로 현재 타입을 부모 타입으로 변경하는 것을 업캐스팅이라 한다.
    - 예시
      ```java
      public class CastingMain3 {
          public static void main(String[] args) {
              Child child = new Child();
              Parent parent1 = (Parent) child;  // 업캐스팅은 생략 가능, 생략 권장
              Parent parent2 = child;  // 업캐스팅 생략

              parent1.parentMethod();
              parent2.parentMethod();
          }
      }
      ```
      - Child 타입을 Parent 타입에 대입해야 한다. 따라서 타입을 변환하는 캐스팅이 필요하다.
      - 부모 타입으로 변환하는 경우에는 캐스팅 코드인 (타입)을 생략할 수 있다.
      - 업캐스팅은 생략할 수 있다. 다운캐스팅은 생략할 수 없다. 참고로 업캐스팅은 매우 자주 사용하기 때문에 생략을 권장한다.

4. **다운캐스팅과 주의점**
  - 다운캐스팅은 잘못하면 심각한 런타임 오류가 발생할 수 있다.
  - 예시
    ```java
    public class CastingMain4 {
        public static void main(String[] args) {
            Parent parent1 = new Child();
            Child child1 = (Child) parent1;
            child1.childMethod();  // 문제 없음

            Parent parent2 = new Parent();
            Child child2 = (Child) parent2;  // 런타임 오류
            child2.childMethod();
        }
    }
    ```
    - new Parent()로 부모 타입으로 객체를 생성한다. 따라서 메모리 상에 자식 타입은 전혀 존재하지 않는다.
    - 이후 생성 결과를 parent2에 담아둔다. 이 경우 같은 타입이므로 여기서는 문제가 발생하지 않는다.
    - 다음 parent2를 Child 타입으로 다운캐스팅한다. 그런데 parent2는 Parent로 생성이 되었기 때문에 메모리 상에 Child 자체가 존재하지 않는다.
    - 자바에서는 이렇게 사용할 수 없는 타입으로 다운캐스팅하는 경우 ClassCastException이라는 예외를 발생시킨다. 예외가 발생하면 다음 동작이 실행되지 않고, 프로그램이 종료된다.
  - 업캐스팅이 안전하고 다운캐스팅이 위험한 이유
    - 업캐스팅의 경우 이런 문제가 절대 발생하지 않는다. 객체를 생성하면 해당 타입의 상위 부모 타입은 모두 함께 생성되기 때문이다. 따라서 위로만 타입을 변경하는 업캐스팅은 메모리 상에 인스턴스가 모두 존재하기 때문에 항상 안전하기 때문에 캐스팅을 생략할 수 있다.
    - 반면 다운캐스팅의 경우 인스턴스에 존재하지 않는 하위 타입으로 캐스팅하는 문제가 발생할 수 있다. 객체를 생성하면 부모 타입은 함께 생성되지만 자식 타입은 생성되지 않는다. 따라서 개발자가 이런 문제를 인지하고 사용해야 한다는 의미로 명시적으로 캐스팅을 해주어야 한다.

5. **instanceof**
  - 다형성에서 참조형 변수는 이름 그대로 다양한 자식을 대상으로 참조할 수 있다.
  - 변수가 참조하는 인스턴스의 타입을 확인하고 싶다면 instanceof 키워드를 사용하면 된다.
  - 예시
    ```java
    public class CastingMain5 {

        public static void main(String[] args) {
            Parent parent1 = new Parent();
            call(parent1);
            Parent parent2 = new Child();
            call(parent2);
        }

        private static void call(Parent parent) {
            parent.parentMethod();

            if (parent instanceof Child) {
                System.out.println("Child 인스턴스");
                Child child = (Child) parent;
                child.childMethod();
            }
        }
    }
    ```
    - call(Parent parent) 메서드는 매개변수로 넘어온 parent가 참조하는 타입에 따라서 다른 명령을 수행한다.
    - 다운캐스팅을 수행하기 전에는 먼저 instanceof를 사용해서 원하는 타입으로 변경이 가능한 지 확인한 다음 다운캐스팅을 수행하는 것이 안전하다.
    - instanceof 키워드는 오른쪽 대상의 자식 타입을 왼쪽에서 참조하는 경우에도 true를 반환한다.
    - instanceof를 사용하면서 동시에 변수를 선언할 수도 있다.
    ```java
    public class CastingMain6 {
        public static void main(String[] args) {
            Parent parent1 = new Parent();
            call(parent1);
            Parent parent2 = new Child();
            call(parent2);
        }

        private static void call(Parent parent) {
            parent.parentMethod();
            // Child 인스턴스인 경우 childMethod() 실행
            if (parent instanceof Child child) {
                System.out.println("Child 인스턴스");
                child.childMethod();
            }
        }
    }
    ```
    - 덕분에 인스턴스가 맞는 경우 직접 다운캐스팅하는 코드를 생략할 수 있다.

6. **다형성과 메서드 오버라이딩**
  - 메서드 오버라이딩에서 기억해야 할 점은 오버라이딩된 메서드가 항상 우선권을 가진다는 점이다.
  - 멤버 변수는 오버라이딩이 되지 않고, 메서드는 오버라이딩이 된다.
  - 예시
    ```java
    public class OverridingMain {

        public static void main(String[] args) {
            // 자식 변수가 자식 인스턴스 참조
            Child child = new Child();
            System.out.println(child.value);
            child.method();

            // 부모 변수가 부모 인스턴스 참조
            Parent parent = new Parent();
            System.out.println(parent.value);
            parent.method();

            // 부모 변수가 자식 인스턴스 참조
            Parent poly = new Child();
            System.out.println(poly.value);  // 변수는 오버라이딩 X
            poly.method();  // 메서드 오버라이딩
        }
    }
    ```
    - poly 변수는 Parent 타입이다. 따라서 poly.value, poly.method()를 호출하면 인스턴스의 Parent 타입에서 기능을 찾아서 실행한다.
      - poly.value : Parent에 있는 value 값을 읽는다.
      - poly.method() : Parent 타입에 있는 method()를 실행하려고 한다. 그런데 하위 타입인 Child.method()가 오버라이딩 되어 있다. 오버라이딩된 메서드는 항상 우선권을 가지기 때문에 Parent.method()가 아닌 Child.method()가 실행된다.
  - 오버라이딩은 부모 타입에서 정의한 기능을 자식 타입에서 재정의하는 것이다. 만약 자식에서도 오버라이딩하고 손자에서도 같은 메서드를 오버라이딩을 하면 손자의 오버라이딩 메서드가 우선권을 가진다.