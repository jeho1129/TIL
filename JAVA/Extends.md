# <center>TIL<center>

# 상속 :memo:

1. **상속 관계**
  - 상속은 객체 지향 프로그래밍의 핵심 요소 중 하나로, 기존 클래스의 필드와 메서드를 새로운 클래스에서 재사용할 수 있게 해준다.
  - 상속을 사용하기 위해서는 extends 키워드를 사용하면 된다. 또한 extends 대상은 하나만 선택할 수 있다.
  - 부모 클래스(슈퍼 클래스) : 상속을 통해 자신의 필드와 메서드를 다른 클래스에 제공하는 클래스
  - 자식 클래스(서브 클래스) : 부모 클래스로부터 필드와 메서드를 속성받는 클래스
  - 예시
    ```java
    public class Car {

        public void move() {
            System.out.println("차를 이동합니다.");
        }
    }
    ```
    - Car는 부모 클래스가 된다.
    ```java
    public class ElectricCar extends Car {

        public void charge() {
            System.out.println("충전합니다.");
        }
    }
    ```
    ```java
    public class GasCar extends Car {

        public void fillUp() {
            System.out.println("기름을 주유합니다.");
        }
    }
    ```
    - extends Car를 사용해서 부모 클래스인 Car를 상속받는다. 상속 덕분에 move()를 사용할 수 있다.
    ```java
    public class CarMain {

        public static void main(String[] args) {
            ElectricCar electricCar = new ElectricCar();
            electricCar.move();
            electricCar.charge();

            GasCar gasCar = new GasCar();
            gasCar.move();
            gasCar.fillUp();
        }
    }
    ```
    - 상속은 부모의 기능을 자식이 물려받는 것이다. 따라서 자식이 부모의 기능을 물려받아 사용할 수 있다. 반대로 부모 클래스는 자식 클래스에 접근할 수 없다. 자식 클래스는 부모 클래스의 기능을 물려 받기 때문에 접근할 수 있지만, 그 반대는 아니다.
  - 단일 상속
    - 자바는 다중 상속을 지원하지 않는다.
    - extends 대상은 하나만 선택할 수 있다. 즉, 부모를 하나만 선택할 수 있다는 뜻이다. 부모가 또 다른 부모를 하나 가지는 것은 괜찮다.
    - 다중 상속을 사용하게 되면 부모 클래스들에 똑같은 이름의 메서드가 존재할 경우, 어떤 부모의 메서드를 사용해야 할 지 애매한 문제가 발생한다. 이를 다이아몬드 문제라 한다.
    - 또한, 다중 상속을 사용하면 클래스 계층 구조가 매우 복잡해질 수 있다.
    - 이러한 문제점 때문에 자바는 클래스의 다중 상속을 허용하지 않는 대신 인터페이스의 다중 구현을 허용해 이런 문제를 피한다.

2. **상속과 메모리 구조**
  - 자식 클래스 객체를 호출하면 자식뿐만 아니라 상속 관계에 있는 부모 클래스까지 함께 포함해서 인스턴스를 생성한다. 참조값은 하나이지만 실제로 그 안에서는 여러 클래스 정보가 공존하는 것이다.
  - 상속이라고 해서 단순하게 부모의 필드와 메서드만 물려받는 것이 아니다. 상속 관계를 사용하면 부모 클래스도 함께 포함해서 생성된다.
  - 외부에서 볼 때는 하나의 인스턴스를 생성하는 것 같지만 내부에서는 부모와 자식이 모두 생성되고 공간도 구분된다.
  - 자식 클래스의 객체를 호출하면 참조값을 확인하여 메서드를 호출한다. 하지만 상속 관계의 경우에는 내부에 부모와 자식이 모두 존재한다. 이 때 부모를 통해서 메서드를 찾을 지, 자식을 통해서 메서드를 찾을 지 선택해야 한다. 
  - 이 때는 호출하는 변수의 타입(클래스)을 기준으로 선택한다.
  - 상속 관계에서 자식 타입에 해당 기능이 없으면 부모 타입으로 올라가서 선택한다. 부모에서도 해당 기능을 찾지 못하면 더 상위인 부모에서 필요한 기능을 찾아본다. 계속 찾아도 없을 경우에는 컴파일 오류가 발생한다.

3. **상속과 메서드 오버라이딩**
  - 부모 타입의 기능을 자식에서는 다르게 재정의하고 싶은 경우가 존재한다.
  - 부모에게서 상속받은 기능을 자식이 재정의하는 것을 메서드 오버라이딩(Overriding)이라 한다.
  - 예시
    ```java
    public class Car {

        public void move() {
            System.out.println("차를 이동합니다.");
        }
    }
    ```
    ```java
    public class ElectricCar extends Car {

        @Override
        public void move() {
            System.out.println("전기차를 빠르게 이동합니다.");
        }

        public void charge() {
            System.out.println("충전합니다.");
        }
    }
    ```
    ```java
    public class CarMain {

        public static void main(String[] args) {
            ElectricCar electricCar = new ElectricCar();
            electricCar.move();

            GasCar gasCar = new GasCar();
            gasCar.move();
        }
    }
    ```
    - ElectricCar의 move() 메서드를 새로 만들었기 때문에 ElectricCar의 move()를 호출하면 Car의 move()가 아닌 ElectricCar의 move()가 호출된다.
    - @이 붙은 부분을 Annotation이라 한다. Annotation은 주석과 비슷한데, 프로그램이 읽을 수 있는 특별한 주석과 같은 역할이다.
    - @Override는 상위 클래스의 메서드를 오버라이드하는 것임을 나타낸다. 이름 그대로 오버라이딩한 메서드 위에 이 Annotation을 붙여야한다.
    - 컴파일러는 이 Annotation을 보고 메서드가 정확히 오버라이드가 되었는지 확인한다. 오버라이딩 조건을 만족시키지 않으면 컴파일 에러가 발생시킨다. 따라서 실수로 오버라이딩을 못하는 경우를 방지해준다. 예를 들어 이 경우, 만약 부모에 move() 메서드가 없다면 컴파일 오류가 발생한다.
    - 이 기능은 필수는 아니지만 코드의 명확성을 위해 붙여주는 것이 좋다.
  - 오버로딩(Overloading)과 오버라이딩(Overriding)
    - 메서드 오버로딩 : 메서드 이름이 같고 매개변수(파라미터)가 다른 메서드를 여러 개 정의하는 것을 메서드 오버로딩이라 한다.
    - 메서드 오버라이딩 : 하위 클래스에서 상위 클래스의 메서드를 재정의하는 과정을 의미한다. 따라서 상속 관계에서 사용한다. 오버라이딩을 번역하면 재정의라는 뜻을 가지고 있다.
  - 메서드 오버라이딩 조건
    - 메서드 이름 : 메서드 이름이 같아야 한다.
    - 메서드 매개변수(파라미터) : 매개변수(파라미터) 타입, 순서, 개수가 같아야 한다.
    - 반환 타입 : 반환 타입이 같아야 한다. 단, 반환 타입이 하위 클래스 타입일 수 있다.
    - 접근 제어자 : 오버라이딩 메서드의 접근 제어자는 상위 클래스의 메서드보다 더 제한적이어서는 안된다. 예를 들어, 상위 클래스의 메서드가 protected로 선언되어 있다면 하위 클래스에서 private 또는 default로는 오버라이드할 수 없다.
    - 예외 : 오버라이딩 메서드는 상위 클래스의 메서드보다 더 많은 체크 예외를 throw로 선언할 수 없다. 하지만 더 적거나 같은 수의 예외, 또는 하위 타입의 예외는 선언할 수 있다.
    - static, final, private 키워드가 붙은 메서드는 오버라이딩될 수 없다.
      - static은 클래스 레벨에서 작동하므로 인스턴스 레벨에서 사용하는 오버라이딩이 의미가 없다. 클래스 이름을 통해 필요한 곳에 직접 접근하면 된다.
      - final 메서드는 재정의를 금지한다.
      - private 메서드는 해당 클래스에서만 접근 가능하기 때문에 하위 클래스에서 보이지 않는다. 따라서 오버라이딩할 수 없다.
    - 생성자 오버라이딩 : 생성자는 오버라이딩할 수 없다.

4. **상속과 접근 제어**
  ```java
  package extends1.access.parent;

  public class Parent {

      public int publicValue;
      protected int protectedValue;
      int defaultValue;
      private int privateValue;

      public void publicMethod() {
          System.out.println("Parent.publicMethod");
      }

      protected void protectedMethod() {
          System.out.println("Parent.protectedMethod");
      }

      void defaultMethod() {
          System.out.println("Parent.defaultMethod");
      }

      private void privateMethod() {
          System.out.println("Parent.privateMethod");
      }

      public void printParent() {
          System.out.println("==Parent 메서드 안==");
          System.out.println(publicValue);
          System.out.println(protectedValue);
          System.out.println(defaultValue);
          System.out.println(privateValue);

          // 부모 메서드 안에서 모두 접근 가능
          defaultMethod();
          privateMethod();
      }
  }
  ```
  ```java
  package extends1.access.child;

  import extends1.access.parent.Parent;

  public class Child extends Parent {

      public void call() {
          publicValue = 1;
          protectedValue = 1;  // 상속 관계 or 같은 패키지
          // defaultValue = 1;  // 다른 패키지 접근 불가, 컴파일 오류
          // privateValue = 1;  // 접근 불가, 컴파일 오류

          publicMethod();
          protectedMethod();
          // defaultMethod();
          // privateMethod();

          printParent();
      }
  }
  ```
  - publicValue : 부모의 public 필드에 접근한다. public이므로 접근할 수 있다.
  - protectedValue : 부모의 protected 필드에 접근한다. 자식과 부모는 다른 패키지이지만, 상속 관계이므로 접근할 수 있다.
  - defaultValue : 자식과 부모가 다른 패키지이므로 접근할 수 없다.
  - privateValue : private는 모든 외부 접근을 막으므로 호출할 수 없다.
  - 접근 제어와 메모리 구조
    - 본인 타입에 없으면 부모 타입에서 기능을 찾는데, 이 때 접근 제어자가 영향을 준다. 객체 내부에서는 자식과 부모가 구분되어있기 때문이다. 결국 자식 타입에서 부모 타입의 기능을 호출할 때, 부모 입장에서 보면 외부에서 호출한 것과 같다.

5. **super - 부모 참조**
  - 부모와 자식의 필드명이 같거나 메서드가 오버라이딩 되어있으면, 자식에서 부모의 필드나 메서드를 호출할 수 없다.
  - 이 때 super 키워드를 사용하면 부모를 참조할 수 있다. super는 이름 그대로 부모 클래스에 대한 참조를 나타낸다.
  - 예시
    ```java
    package extends1.super1;

    public class Parent {

        public String value = "parent";

        public void hello() {
            System.out.println("Parent.hello");
        }
    }
    ```
    ```java
    public class Child extends Parent {

        public String value = "child";

        @Override
        public void hello() {
            System.out.println("Child.hello");
        }

        public void call() {
            System.out.println(this.value);  // child
            System.out.println(super.value);  // parent

            this.hello();  // Child.hello
            super.hello();  // Parent.hello
        }
    }
    ```
    ```java
    public class Super1Main {

        public static void main(String[] args) {
            Child child = new Child();
            child.call();
        }
    }
    ```
    - 필드 이름과 메서드 이름이 같지만 super를 사용하여 부모 클래스에 있는 기능을 사용할 수 있다.

6. **super - 생성자**
  - 상속 관계의 인스턴스를 생성하면 결국 메모리 내부에는 자식과 부모 클래스가 각각 다 만들어진다. 따라서 각각의 생성자도 모두 호출되어야 한다.
  - 상속 관계를 사용하면 자식 클래스의 생성자에서 부모 클래스의 생성자를 반드시 호출해야 한다.
  - 상속 관계에서 부모의 생성자를 호출할 때는 super를 사용하면 된다.
  - 예시
    ```java
    public class ClassA {

        public ClassA() {
            System.out.println("ClassA 생성자");
        }
    }
    ```
    - ClassA는 최상위 부모 클래스이다.
    ```java
    public class ClassB extends ClassA {

        public ClassB(int a) {
            super();  // 기본 생성자 생략 가능
            System.out.println("ClassB 생성자 = " + a);
        }

        public ClassB(int a, int b) {
            super();  // 기본 생성자 생략 가능
            System.out.println("ClassB 생성자 = " + a + "+" + b);
        }
    }
    ```
    - ClassB는 ClassA를 상속받았다. 상속을 받으면 생성자의 첫 줄에 super를 사용하여 부모 클래스의 생성자를 호출해야한다.
    - 예외로 생성자 첫 줄에 this를 사용할 수는 있다. 하지만 super는 자식의 생성자 안에서 언젠가는 반드시 호출해야 한다.
    - 부모 클래스의 생성자가 기본 생성자(파라미터가 없는 생성자)인 경우에는 super()를 생략할 수 있다.
    - 상속 관계에서 첫 줄에 super를 생략하면 자바는 부모의 기본 생성자를 호출하는 super()를 자동으로 만들어준다.
    ```java
    public class ClassC extends ClassB {

        public ClassC() {
            super(10, 20);
            System.out.println("ClassC 생성자");
        }
    }
    ```
    - ClassC는 ClassB를 상속받았다.
    - 생성자는 하나만 호출할 수 있으므로 ClassB의 두 생성자 중 하나만 선택하면 된다.
    - ClassC의 부모인 ClassB에는 기본 생성자가 없다. 따라서 부모의 기본 생성자를 호출하는 super()를 사용하거나 생략할 수 없다.
    ```java
    public class Super2Main {

        public static void main(String[] args) {
            ClassC classC = new ClassC();
        }
    }
    ```
    - ClassA - ClassB - ClassC 순서로 실행된다. 생성자의 실행 순서가 결과적으로 최상위 부모부터 실행되어 하나씩 아래로 내려오는 것이다. 따라서 초기화는 최상위 부모부터 이루어진다. 왜냐하면 자식 생성자의 첫 줄에서 부모의 생성자를 호출해야하기 때문이다.
  - 상속 관계의 생성자 호출은 결과적으로 부모에서 자식 순서로 실행된다. 따라서 부모의 데이터를 먼저 초기화하고 그 다음 자식의 데이터를 초기화한다.
  - 상속 관계에서 자식 클래스의 생성자 첫 줄에 반드시 super를 호출해야한다. 단 기본 생성자인 경우 생략할 수 있다.