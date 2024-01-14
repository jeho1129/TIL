# <center>TIL<center>

# final :memo:

1. **final 변수**
  - final 키워드는 이름 그대로 끝이라는 뜻이다.
  - 변수에 final 키워드가 붙으면 더는 값을 변경할 수 없다.
  - 참고로 final은 class, method를 포함한 여러 곳에 붙을 수 있다.
  ```java
  public class FinalLocalMain {

      public static void main(String[] args) {
          // final 지역 변수
          final int data1;
          data1 = 10; // 최초 한 번만 할당 가능
      }

      // final 매개변수    
      static void method(final int parameter) {
          // parameter = 20; 컴파일 오류
      }
  }
  ```
  - final을 지역 변수에 설정할 경우 최초 한 번만 할당할 수 있다. 이후 변수의 값을 변경하려면 컴파일 오류가 발생한다.
  - final을 지역 변수 선언 시 바로 초기화한 경우 이미 값이 할당되었기 때문에 값을 할당할 수 없다.
  - 매개변수에 final이 붙으면 메서드 내부에서 매개변수의 값을 변경할 수 없다. 따라서 메서드 호출 시점에 사용된 값이 끝까지 사용된다.
  ```java
  public class ConstructInit {

      final int value;

      public ConstructInit(int value) {
          this.value = value;
      }
  }
  ```
  - final을 필드에 사용할 경우 해당 필드는 생성자를 통해서 한 번만 초기화될 수 있다.
  ```java
  public class FieldInit {
    
      static final int CONST_VALUE = 10;
      final int value = 10;
  }
  ```
  - final 필드를 필드에서 초기화하면 이미 값이 설정되었기 때문에 생성자를 통해서도 초기화할 수 없다.
  - static 변수에도 final을 선언할 수 있다.
  - 생성자를 사용해서 final 필드를 초기화하는 경우, 각 인스턴스마다 final 필드에 다른 값을 할당할 수 있다.
  - final 필드를 필드에서 초기화하는 경우, 모든 인스턴스가 같은 값을 사용하기 때문에 static 영역을 이용하여 메모리를 효율적으로 관리할 수 있다.
  - 따라서 필드에 final + 필드 초기화를 사용하는 경우 static을 붙여서 사용하는 것이 효과적이다.

2. **final 상수**
  - 상수는 변하지 않고, 항상 일정한 값을 가지는 수를 말한다. 자바에서는 보통 단 하나만 존재하는 변하지 않는 고정된 값을 상수라 한다. 이러한 이유로 상수는 static final 키워드를 사용한다.
  - 자바 상수 특징
    - static final 키워드를 사용한다.
    - 대문자를 사용하고 구분은 _로 한다.(일반적인 변수와 상수를 구분하기 위해 이렇게 한다.)
    - 필드를 직접 접근해서 사용한다
      - 상수는 기능이 아니라 고정된 값 자체를 사용하는 것이 목적이다.
      - 상수는 값을 변경할 수 없다. 따라서 필드에 직접 접근해도 데이터가 변하는 문제가 발생하지 않는다.
    - 상수는 보통 애플리케이션 전반에서 사용되기 때문에 public을 자주 사용한다.
    - 상수는 중앙에서 값을 하나로 관리할 수 있다는 장점이 있다.
    - 상수는 런타임에 변경할 수 없다. 상수를 변경하려면 프로그램을 종료하고, 코드를 변경한 다음에 프로그램을 다시 실행해야 한다.

3. **final 변수와 참조**
  - final은 변수의 값을 변경하지 못하게 막는다.
  - final을 기본형 변수에 사용하면 값을 변경할 수 없다.
  - final을 참조형 변수에 사용하면 참조값을 변경할 수 없다.
  ```java
  public class Data {
      public int value;
  }
  ```
  ```java
  public class FinalRefMain {

      public static void main(String[] args) {
          final Data data = new Data();
          // 참조 대상의 값은 변경 가능
          data.value = 10;
          data.value = 20;
          System.out.println(data.value);
      }
  }
  ```
  - 참조형 변수 data에 final이 붙었고, 변수 선언 시점에 참조값을 할당했으므로 더는 참조값을 변경할 수 없다.
  - 하지만 참조 대상의 객체 값은 변경할 수 있다.
