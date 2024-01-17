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

7. **다형성 활용**
  ```java
  public class Cat {

      public void sound() {
          System.out.println("냐옹");
      }
  }
  ```
  ```java
  public class Caw {

      public void sound() {
          System.out.println("음매");
      }
  }
  ```
  ```java
  public class Dog {

      public void sound() {
          System.out.println("멍멍");
      }
  }
  ```
  ```java
  public class AnimalSoundMain {

      public static void main(String[] args) {
          Dog dog = new Dog();
          Cat cat = new Cat();
          Caw caw = new Caw();

          dog.sound();
          cat.sound();
          caw.sound();
      }
  }
  ```
  - 여기서 새로운 동물이 추가된다고 가정하면, 새로운 클래스를 만들고 코드도 새로 추가해야 하며, 중복되는 코드가 증가하게 된다.
  - 중복을 제거하기 위해서는 메서드를 사용하거나 배열과 for문을 사용하면 된다. 하지만 Dog, Cat, Caw는 서로 완전히 다른 클래스이다.
  - 메서드를 통한 중복 제거 시도
    ```java
    private static void soundCaw(Caw caw) {
        System.out.println("동물 소리 테스트 시작");
        caw.sound();
        System.out.println("동물 소리 테스트 종료");
    }
    ```
    - 메서드를 사용하면 매개변수의 클래스가 서로 다르기 때문에 메서드를 함께 사용하는 것은 불가능하다.
  - 배열과 for문을 통한 중복 제거 시도
    ```java
    Caw[] cawArr = {cat, dog, caw};  //컴파일 오류 발생
    System.out.println("동물 소리 테스트 시작");
        for (Caw caw : cawArr) {
            cawArr.sound();
        }
    System.out.println("동물 소리 테스트 종료");
    ```
    - 배열과 for문을 사용하여 중복을 제거하려고 해도 배열의 타입을 하나로 지정해야 한다.
    - 타입이 서로 다른 Dog, Cat, Caw를 하나의 배열에 담는 것은 불가능하다.
  - 지금까지 중복 제거 시도가 안되는 이유의 핵심은 바로 타입이 다르다는 점이다. Dog, Cat, Caw가 모두 같은 타입을 사용할 수 있는 방법이 있다면 메서드와 배열을 활용하여 코드의 중복을 제거할 수 있다.
  - 다형성의 핵심은 다형적 참조와 메서드 오버라이딩이다. 이 둘을 활용하면 Dog, Cat, Caw가 모두 같은 타입을 사용하고 자신의 메서드도 호출할 수 있다.
  - 다형성을 사용하기 위해 상속 관계를 사용한다. Animal이라는 부모 클래스를 만들고 sound() 메서드를 정의한다. 이 메서드는 자식 클래스에서 오버라이딩할 목적으로 만들었다.
  - Dog, Cat, Caw는 Animal 클래스를 상속받았다. 그리고 각각 부모의 sound() 메서드를 오버라이딩한다.
  ```java
  public class Animal {
      public void sound() {
          System.out.println("동물 울음 소리");
      }
  }
  ```
  ```java
  public class Cat extends Animal {
      @Override
      public void sound() {
          System.out.println("냐옹");
      }
  }
  ```
  ```java
  public class AnimalPolyMain1 {

      public static void main(String[] args) {
          Dog dog = new Dog();
          Cat cat = new Cat();
          Caw caw = new Caw();

          soundAnimal(dog);
          soundAnimal(cat);
          soundAnimal(caw);
      }

      public static void soundAnimal(Animal animal) {
          animal.sound();
      }
  }
  ```
  - soundAnimal(dog)을 호출하면 soundAnimal(Animal animal)에 Dog 인스턴스가 전달된다. Animal은 Dog의 부모이다.
  - 메서드 안에서 animal.sound() 메서드를 호출한다.
  - animal 변수의 타입은 Animal이므로 Dog 인스턴스에 있는 Animal 클래스 부분을 찾아서 sound() 메서드를 실행한다. 그런데 하위 클래스인 Dog에서 sound() 메서드를 오버라이딩했다. 따라서 오버라이딩한 메서드가 우선권을 가진다.
  - Dog 클래스에 있는 sound() 메서드가 호출된다.
  - 이 코드의 핵심은 Animal animal 부분이다.
    - 다형적 참조 덕분에 animal 변수는 자식인 Dog, Cat, Caw의 인스턴스를 참조할 수 있다.(부모는 자식을 담을 수 있다.)
    - 메서드 오버라이딩 덕분에 animal.sound()를 호출해도 각 인스턴스의 메서드를 호출할 수 있다. 만약 자바에 메서드 오버라이딩이 없었다면 모두 Animal의 sound()가 호출되었을 것이다.
  ```java
  public class AnimalPolyMain2 {

      public static void main(String[] args) {
          Dog dog = new Dog();
          Cat cat = new Cat();
          Caw caw = new Caw();
          Animal[] animalArr = {dog, cat, caw};

          // 변하지 않는 부분
          for (Animal animal : animalArr) {
              animal.sound();
          }

      }
  }
  ```
  - 배열은 같은 타입의 데이터를 나열할 수 있다.
  - Animal 타입의 배열을 만들고 다형적 참조를 사용하면 된다.
  ```java
  public class AnimalPolyMain2 {

      public static void main(String[] args) {
          Animal[] animalArr = {new Dog(), new Cat(), new Caw()};
          for (Animal animal : animalArr) {
              soundAnimal(animal);
          }
      }

      private static void soundAnimal(Animal animal) {
          animal.sound();
      }
  }
  ```
  - 새로운 동물이 추가되어도 soundAnimal() 메서드는 코드 변경 없이 유지할 수 있다. 이렇게 할 수 있는 이유는 이 메서드는 Dog 같은 구체적인 클래스를 참조하는 것이 아니라 Animal이라는 추상적인 부모를 참조하기 때문이다. 따라서 Animal을 상속 받은 새로운 동물이 추가되어도 이 메서드의 코드는 변경 없이 유지할 수 있다.
  - main()은 코드가 변하는 부분이지만, soundAnimal()은 코드가 변하지 않는 부분이다.
  - 새로운 기능이 추가되었을 때 변하는 부분을 최소화하는 것이 잘 작성된 코드이다. 이렇게 코드에서 변하는 부분과 변하지 않는 부분을 명확하게 구분하는 것이 좋다.
  - 이 코드에는 2가지 문제가 존재한다.
    - Animal 클래스를 생성할 수 있는 문제
      - Animal 클래스는 동물이라는 클래스로, 다형성을 위해서 필요한 것이지 직접 인스턴스를 생성해서 사용할 일은 없다.
      - 하지만 Animal도 클래스이기 때문에 인스턴스를 생성하고 사용하는 데 아무런 제약이 없다.
      - 이렇게 생성된 인스턴스는 작동은 하지만 제대로 된 기능을 수행하지 않는다.
    - Animal 클래스를 상속받는 곳에서 sound() 메서드를 오버라이딩하지 않을 가능성
      - Animal 클래스를 상속받는 새 클래스를 만든다고 가정했을 때, 개발자가 실수로 메서드를 오버라이딩하는 것을 깜빡하게 되면 부모의 기능을 상속받는다.
    - 추상 클래스와 추상 메서드를 사용하면 이런 문제를 한 번에 해결할 수 있다.

8. **추상 클래스**
  - 추상 클래스
    - 부모 클래스는 제공하지만, 실세 생성되면 안되는 클래스를 추상 클래스라 한다.
    - 추상 클래스는 이름 그대로 추상적인 개념을 제공하는 클래스이다. 따라서 실체인 인스턴스가 존재하지 않는다.
    - 대신 상속을 목적으로 사용하고 부모 클래스의 역할을 담당한다.
    ```java
    abstract class AbstractAnimal {...}
    ```
    - 추상 클래스는 클래스를 선언할 때 앞에 추상이라는 의미의 abstract 키워드를 붙여주면 된다.
    - 추상 클래스는 기존 클래스와 완전히 같다. 다만 new AbstractAnimal()와 같이 직접 인스턴스를 생성하지 못하는 제약이 추가된 것이다.
  - 추상 메서드
    - 부모 클래스를 상속받는 자식 클래스가 반드시 오버라이딩해야 하는 메서드를 부모 클래스에 정의할 수 있다. 이것을 추상 메서드라 한다.
    - 추상 메서드는 이름 그대로 추상적인 개념을 제공하는 메서드이다. 따라서 실체가 존재하지 않고, 메서드 바디가 없다.
    ```java
    public abstract void sound();
    ```
    - 추상 메서드는 선언할 때 메서드 앞에 추상이라는 의미의 abstract 키워드를 붙여주면 된다.
    - 추상 메서드가 하나라도 있는 클래스는 추상 클래스로 선언해야 한다.
      - 그렇지 않으면 컴파일 오류가 발생한다.
      - 추상 메서드는 메서드 바디가 없다. 따라서 작동하지 않는 메서드를 가진 불완전한 클래스로 볼 수 있다. 따라서 직접 생성하지 못하도록 추상 클래스로 선언해야 한다.
    - 추상 메서드는 상속받는 자식 클래스가 반드시 오버라이딩해서 사용해야 한다.
      - 그렇지 않으면 컴파일 오류가 발생한다.
      - 추상 메서드는 자식 클래스가 반드시 오버라이딩해야 하기 때문에 메서드 바디 부분이 없다. 따라서 바디 부분을 만들면 컴파일 오류가 발생한다.
      - 오버라이딩하지 않으면 자식도 추상 클래스가 되어야한다.
    - 추상 메서드는 기존 메서드와 완전히 같다. 다만, 메서드 바디가 없고, 자식 클래스가 해당 메서드를 반드시 오버라이딩해야 한다는 제약이 추가된 것이다.
  - 예시
    ```java
    public abstract class AbstractAnimal {

        public abstract void sound();
        
        public void move() {
            System.out.println("동물이 움직입니다.");
        }
    }
    ```
    - AbstractAnimal은 abstract가 붙은 추상 클래스이다. 이 클래스는 직접 인스턴스를 생성할 수 없다.
    - sound()는 abstract가 붙은 추상 메서드이다. 이 메서드는 자식이 반드시 오버라이딩해야 한다.
    - 이 클래스는 move()라는 메서드를 가지고 있는데, 이 메서드는 추상 메서드가 아니다. 따라서 자식 클래스가 오버라이딩하지 않아도 된다.
    - 참고로 추상 클래스라고 AbstractAnimal처럼 클래스 이름 앞에 꼭 Abstract를 써야하는 것은 아니다. 그냥 Animal이라는 클래스 이름으로도 충분하다.
    ```java
    public class AbstractMain {

        public static void main(String[] args) {
            // 추상클래스 생성 불가
            // AbstractAnimal animal = new AbstractAnimal();

            Dog dog = new Dog();
            Cat cat = new Cat();
            Caw caw = new Caw();

            cat.sound();
            cat.move();

            soundAnimal(dog);
            soundAnimal(cat);
            soundAnimal(caw);
        }

        private static void soundAnimal(AbstractAnimal animal) {
            animal.sound();
        }
    }
    ```
    - 추상 클래스는 생성이 불가능하다.
    - 추상 메서드는 반드시 오버라이딩해야 한다. 만약 자식에서 오버라이딩 메서드를 만들지 않으면 컴파일 오류가 발생한다.
  - 순수 추상 클래스 : 모든 메서드가 추상 메서드인 추상 클래스
    ```java
    public abstract class AbstractAnimal {
        public abstract void sound();
        public abstract void move();
    }
    ```
    ```java
    public class Cat extends AbstractAnimal {

        @Override
        public void sound() {
            System.out.println("냐옹");
        }

        @Override
        public void move() {
            System.out.println("고양이 이동");
        }
    }
    ```
    ```java
    public class AbstractMain {

        public static void main(String[] args) {
            // 추상클래스 생성 불가
            // AbstractAnimal animal = new AbstractAnimal();

            Dog dog = new Dog();
            Cat cat = new Cat();
            Caw caw = new Caw();

            soundAnimal(dog);
            soundAnimal(cat);
            soundAnimal(caw);

            moveAnimal(dog);
            moveAnimal(cat);
            moveAnimal(caw);
        }

        private static void soundAnimal(AbstractAnimal animal) {
            animal.sound();
        }

        private static void moveAnimal(AbstractAnimal animal) {
            animal.move();
        }
    }
    ```
    - 순수 추상 클래스
      - 모든 메서드가 추상 메서드인 순수 추상 클래스는 코드를 실행할 바디 부분이 전혀 없다.
      - 이러한 순수 추상 클래스는 실행 로직을 전혀 가지고 있지 않다. 단지 다형성을 위한 부모 타입으로써 껍데기 역할만 제공할 뿐이다.
    - 순수 추상 클래스 특징
      - 인스턴스를 생성할 수 없다.
      - 상속 시 자식은 모든 메서드를 오버라이딩해야 한다.
      - 주로 다형성을 위해 사용된다.
    - 상속하는 클래스는 모든 메서드를 구현해야 한다.
      - 상속 시 자식은 모든 메서드를 오버라이딩해야 한다라는 특징은 상속 받는 클래스 입장에서 보면 부모의 모든 메서드를 구현해야 하는 것이다.
      - 이런 특징을 생각해보면 순수 추상 클래스는 마치 어떤 규격을 지켜서 구현해야 하는 것처럼 느껴진다.
      - AbstractAnimal의 경우 sound(), move()라는 규격에 맞추어 구현을 해야한다.
      - 이것은 우리가 일반적으로 이야기하는 인터페이스와 같이 느껴진다.
      - 이런 순수 추상 클래스의 개념은 프로그래밍에서 매우 자주 사용된다. 자바는 순수 추상 클래스를 더 편리하게 사용할 수 있도록 인터페이스라는 개념을 제공한다.

9. **인터페이스**
  - 자바는 순수 추상 클래스를 더 편리하게 사용할 수 있는 인터페이스라는 기능을 제공한다.
  - 인터페이스는 class가 아니라 interface 키워드를 사용하면 된다.
  - 인터페이스의 메서드는 모두 public, abstract이다.
  - 메서드에 public abstract를 생략할 수 있다. 참고로 생략이 권장된다.
  - 인터페이스는 다중 구현(다중 상속)을 지원한다.
  ```java
  public interface InterfaceAnimal {
      void sound();
      void move();
  }
  ```
  - 인터페이스와 멤버 변수
    ```java
    public interface InterfaceAnimal {
        public static final int MY_PI = 3.14;
    }
    ```
    - 인터페이스에서 멤버 변수는 public, static, final이 모두 포함되었다고 간주된다.
    - 자바에서 static final을 사용해 정적이면서 고칠 수 없는 변수를 상수라 하고, 관례상 상수는 대문자에 언더스코어로 구분한다.
    ```java
    public interface InterfaceAnimal {
        int MY_PI = 3.14;
    }
    ```
    - 다음과 같이 키워드를 생략할 수 있다.
  - 예시
    ```java
    public interface InterfaceAnimal {
        void sound();
        void move();
    }
    ```
    ```java
    public class Cat implements InterfaceAnimal {
        @Override
        public void sound() {
            System.out.println("냐옹");
        }

        @Override
        public void move() {
            System.out.println("고양이 이동");
        }
    }
    ```
    ```java
    public class InterfaceMain {

        public static void main(String[] args) {
            // 인터페이스 생성 불가
            // InterfaceAnimal interfaceAnimal = new InterfaceAnimal();

            Cat cat = new Cat();
            Dog dog = new Dog();
            Caw caw = new Caw();

            soundAnimal(cat);
            soundAnimal(dog);
            soundAnimal(caw);
        }

        private static void soundAnimal(InterfaceAnimal animal) {
            animal.sound();
        }
    }
    ```
    - 클래스, 추상 클래스, 인터페이스는 모두 똑같다.
      - 클래스, 추상 클래스, 인터페이스는 프로그램 코드, 메모리 구조 상 모두 똑같다.
      - 인터페이스는 순수 추상 클래스와 비슷하다고 생각하면 된다.
  - 상속 vs 구현
    - 부모 클래스의 기능을 자식 클래스가 상속받을 때, 클래스는 상속받는다고 표현하지만, 부모 인터페이스의 기능을 자식이 상속받을 때는 인터페이스를 구현한다고 표현한다.
    - 상속은 이름 그대로 부모의 기능을 물려받는 것이 목적이다.
    - 하지만, 인터페이스는 모든 메서드가 추상 메서드이므로 물려받을 수 있는 기능이 없고, 오히려 인터페이스에 정의한 모든 메서드를 자식이 오버라이딩해서 기능을 구현해야 하므로, 구현한다고 표현한다.
    - 인터페이스는 메서드 이름만 있는 설계도이고, 이 설계도가 실제 어떻게 작동하는 지는 하위 클래스에서 모두 구현해야 한다.
    - 따라서 인터페이스의 경우 상속이 아니라 해당 인터페이스를 구현한다고 표현한다.
  - 인터페이스를 사용해야 하는 이유
    - 제약
      - 인터페이스를 만드는 이유는 인터페이스를 구현하는 곳에서 인터페이스의 메서드를 반드시 구현하라는 규약(제약)을 주는 것이다.
      - 순수 추상 클래스의 경우 미래에 실행 가능한 메서드를 추가할 수 있는데, 추가된 기능을 자식 클래스에서 구현하지 않을 수도 있고, 또 더는 순수 추상 클래스가 아니게 된다.
      - 인터페이스는 모든 메서드가 추상 메서드이므로 이런 문제를 원천 차단할 수 있다.
    - 다중 구현
      - 자바에서 클래스 상속은 부모를 하나만 지정할 수 있다. 반면 인터페이스는 부모를 여러 명 두는 다중 구현(다중 상속)이 가능하다.

10. **인터페이스 - 다중 구현**
  - 자바는 다중 상속을 지원하지 않는다. 그래서 extends 대상은 하나만 선택할 수 있다. 즉, 부모를 하나만 선택할 수 있다는 뜻이다.
  - 대신 인터페이스의 다중 구현을 허용하여 이러한 문제를 해결한다. 인터페이스는 모두 추상 메서드로 이루어져 있기 때문이다.
  - 인터페이스 자신은 구현을 가지지 않는 대신 인터페이스를 구현하는 곳에서 해당 기능을 모두 구현해야 한다. 이런 이유로 인터페이스는 다이아몬드 문제가 발생하지 않는다.
  - 예시
    ```java
    public interface InterfaceA {
        void methodA();
        void methodCommon();
    }
    ```
    ```java
    public interface InterfaceB {
        void methodB();
        void methodCommon();
    }
    ```
    ```java
    public class Child implements InterfaceA, InterfaceB {
        @Override
        public void methodA() {
            System.out.println("Child.methodA");
        }

        @Override
        public void methodB() {
            System.out.println("Child.methodB");
        }

        @Override
        public void methodCommon() {
            System.out.println("Child.methodCommon");
        }
    }
    ```
    - implements InterfaceA, InterfaceB와 같이 다중 구현을 할 수 있다.
    - methodCommon()의 경우 양 쪽 인터페이스에 다 있지만 같은 메서드이므로 구현은 하나만 하면 된다.
    ```java
    public class DiamondMain {

        public static void main(String[] args) {
            InterfaceA a = new Child();
            a.methodA();
            a.methodCommon();
            
            InterfaceB b = new Child();
            b.methodB();
            b.methodCommon();
        }
    }
    ```
    - a.methodCommon()을 호출하면 변수 a가 InterfaceA 타입이므로 해당 타입에서 methodCommon()을 찾는다.
    - methodCommon()은 하위 타입인 Child에서 오버라이딩되어 있다. 따라서 Child의 methodCommon()이 호출된다.
    - 변수 b도 마찬가지이다.

11. **클래스와 인터페이스 활용**
  ```java
  public abstract class AbstractAnimal {
      public abstract void sound();
      public void move() {
          System.out.println("동물이 이동합니다.");
      }
  }
  ```
  ```java
  public interface Fly {
      void fly();
  }
  ```
  ```java
  public class Dog extends AbstractAnimal {
      @Override
      public void sound() {
          System.out.println("멍멍");
      }
  }
  ```
  ```java
  public class Bird extends AbstractAnimal implements Fly {
      @Override
      public void sound() {
          System.out.println("짹짹");
      }

      @Override
      public void fly() {
          System.out.println("새 날기");
      }
  }
  ```
  - Bird는 AbstractAnimal 클래스를 상속하고 Fly 인터페이스를 구현한다.
  - extends를 통한 상속은 하나만 할 수 있고, implements를 통한 인터페이스는 다중 구현할 수 있기 때문에 둘이 함께 나온 경우 extends가 먼저 나와야한다.
  ```java
  public class Chicken extends AbstractAnimal implements Fly {
      @Override
      public void sound() {
          System.out.println("꼬끼오");
      }

      @Override
      public void fly() {
          System.out.println("닭 날기");
      }
  }
  ```
  ```java
  public class SoundFlyMain {

      public static void main(String[] args) {
          Dog dog = new Dog();
          Bird bird = new Bird();
          Chicken chicken = new Chicken();

          soundAnimal(dog);
          soundAnimal(bird);
          soundAnimal(chicken);

          flyAnimal(bird);
          flyAnimal(chicken);
      }

      private static void soundAnimal(AbstractAnimal animal) {
          animal.sound();
      }
      // Fly 인터페이스가 있으면 사용 가능
      private static void flyAnimal(Fly fly) {
          fly.fly();
      }
  }
  ```
  - soundAnimal(AbstractAnimal animal) : AbstractAnimal을 상속한 Dog, Bird, Chicken을 전달해서 실행할 수 있다.
  - flyAnimal(Fly fly) : Fly 인터페이스를 구현한 Bird, Chicken을 전달해서 실행할 수 있다.
