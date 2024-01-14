# <center>TIL<center>

# 메모리 구조와 static :memo:

1. **자바 메모리 구조**
  - 자바의 메모리 구조는 크게 메서드 영역, 스택 영역, 힙 영역 3개로 나눌 수 있다.
    - 메서드 영역
      - 클래스 정보를 보관한다.
      - 프로그램을 실행하는 데 필요한 공통 데이터를 관리한다. 이 영역은 프로그램의 모든 영역에서 공유한다.
      - 클래스 정보 : 클래스의 실행 코드(바이트 코드), 필드, 메서드와 생성자 코드 등 모든 실행 코드가 존재한다.
      - static 영역 : static 변수들을 보관한다.
      - 런타임 상수 풀 : 프로그램을 실행하는 데 필요한 공통 리터럴 상수를 보관한다. 예를 들어 프로그램에 "hello"라는 리터럴 문자가 있으면 이런 문자를 공통으로 묶어 관리한다. 이 외에도 프로그램을 효율적으로 관리하기 위한 상수들을 관리한다.
    - 스택 영역
      - 실제 프로그램이 실행되는 영역이다. 메서드를 실행할 때마다 하나씩 쌓인다.
      - 자바 실행 시, 하나의 실행 스택이 생성된다. 각 스택 프레임은 지역 변수, 중간 연산 결과, 메서드 호출 정보 등을 포함한다.
      - 스택 프레임 : 스택 영역에 쌓이는 네모 박스가 하나의 스택 프레임이다. 메서드를 호출할 때마다 하나의 스택 프레임이 쌓이고, 메서드가 종료되면 해당 스택 프레임이 제거된다.
    - 힙 영역
      - 객체(인스턴스)와 배열이 생성되는 영역이다. new 명령어를 사용하면 이 영역을 사용한다.
      - 가비지 컬렉션(GC)이 이루어지는 주요 영역이며, 더 이상 참조되지 않는 객체는 GC에 의해 제거된다.
  - 자바에서 특정 클래스로 100개의 인스턴스를 생성하면, 힙 메모리에 100개의 인스턴스가 생긴다. 각각의 인스턴스는 내부에 변수와 메서드를 가진다. 같은 클래스로부터 생성된 객체라도, 인스턴스 내부의 변수 값은 서로 다를 수 있지만 메서드는 공통된 코드를 공유한다. 따라서 객체가 생성될 때, 인스턴스 변수에는 메모리가 할당되지만, 메서드에 대한 새로운 메모리 할당은 없다. 메서드는 메서드 영역에서 공통으로 관리되고 실행된다.
  - 즉, 인스턴스의 메서드를 호출하면 실제로는 메서드 영역에 있는 코드를 불러서 수행한다.

2. **스택 영역**
  - 예시
    ```java
    package memory;

    public class JavaMemoryMain1 {

        public static void main(String[] args) {
            System.out.println("main start");
            method1(10);
            System.out.println("main end");
        }

        static void method1(int m1) {
            System.out.println("method1 start");
            int cal = m1 * 2;
            method2(cal);
            System.out.println("method1 end");
        }

        static void method2(int m2) {
            System.out.println("method2 start");
            System.out.println("method2 end");
        }
    }
    // 실행 결과
    // main start
    // method1 start
    // method2 start
    // method2 end
    // method1 end
    // main end
    ```
    - 처음 자바 프로그램을 실행하면 main()을 실행한다. 이 때 main()을 위한 스택 프레임이 하나 생성된다. main() 스택 프레임은 내부에 args라는 매개변수를 가진다.
    - main()은 method1()을 호출한다. method1() 스택 프레임이 생성된다. method1()는 m1, cal 지역 변수(매개변수 포함)를 가지므로 해당 지역 변수들이 스택 프레임에 포함된다.
    - method1()은 method2()를 호출한다. method2() 스택 프레임이 생성된다. method2()는 m2 지역 변수(매개변수 포함)를 가지므로 해당 지역 변수가 스택 프레임에 포함된다.
    - method2()가 종료된다. 이 때 method2() 스택 프레임이 제거되고, 매개변수 m2도 제거된다. method2() 스택 프레임이 제거되었으므로, 프로그램은 method1()로 돌아간다.
    - method1()이 종료된다. 이 때 method1() 스택 프레임이 제거되고, 지역 변수 m1, cal도 제거된다. 프로그램은 main()로 돌아간다.
    - main()이 종료된다. 자바는 프로그램을 정리하고 종료한다.
  - 자바는 스택 영역을 사용해서 메서드 호출과 지역 변수(매개변수 포함)를 관리한다.
  - 메서드를 계속 호출하면 스택 프레임이 계속 쌓인다.
  - 지역 변수(매개변수 포함)는 스택 영역에서 관리한다.
  - 스택 프레임이 종료되면 지역 변수도 함께 제거된다.
  - 스택 프레임이 모두 제거되면 프로그램도 종료된다.

3. **스택 영역과 힙 영역**
  - 힙 영역 외부가 아닌 힙 영역 안에서만 인스턴스끼리 서로 참조하는 경우에도 GC의 대상이 된다.
  - 지역 변수는 스택 영역에, 객체(인스턴스)는 힙 영역에 관리된다.

4. **static 변수**
  - static 키워드는 주로 멤버 변수와 메서드에 사용된다.
  ```java
  public class Counter {
      public int count;
  }
  ```
  ```java
  public class Data2 {
      public String name;

      public Data2(String name, Counter counter) {
          this.name = name;
          counter.count++;
      }
  }
  ```
  ```java
  public class DataCountMain2 {

      public static void main(String[] args) {
          Counter counter = new Counter();
          Data2 data1 = new Data2("A", counter);
          System.out.println(counter.count);

          Data2 data2 = new Data2("B", counter);
          System.out.println(counter.count);
      }
  }
  ```
  - 생성자가 호출되면 counter 인스턴스에 있는 count 변수의 값을 하나 증가시킨다.
  - Counter 인스턴스를 공용으로 사용한 덕분에 객체를 생성할 때마다 값을 정확하게 증가시킬 수 있다.
  - 하지만, Counter라는 별도 클래스를 추가로 사용해야 하기 때문에, 생성자의 매개변수도 추가되고, 생성자가 복잡해진다. 생성자를 호출하는 부분도 복잡해진다.
  - 특정 클래스에서 공용으로 함께 사용할 수 있는 변수를 만들 수 있다면 편리할 것이다.
  - static 키워드를 사용하면 공용으로 함께 사용하는 변수를 만들 수 있다.
  ```java
  public class Data3 {
      public String name;
      public static int count;  // static
      
      public Data3(String name) {
          this.name = name;
          count++;
      }
  }
  ```
  - 멤버 변수에 static을 붙이게 되면 static 변수, 정적 변수 또는 클래스 변수라 한다.
  - 객체가 생성되면 생성자에서 정적 변수 count의 값을 하나 증가시킨다.
  - name, count는 둘 다 멤버 변수이다.
  - 멤버 변수는 static이 붙은 것과 아닌 것에 따라 다음과 같이 분류할 수 있다.
    - 인스턴스 변수 : static이 붙지 않은 멤버 변수
      - static이 붙지 않은 멤버 변수는 인스턴스를 생성해야 사용할 수 있고, 인스턴스에 소속되어 있다. 따라서 인스턴스 변수라 한다.
      - 인스턴스 변수는 인스턴스를 만들 때마다 새로 만들어진다.
    - 클래스 변수 : static이 붙은 멤버 변수
      - 클래스 변수, 정적 변수, static 변수 등으로 부른다.
      - static이 붙은 멤버 변수는 인스턴스와 무관하게 클래스에 바로 접근해서 사용할 수 있고, 클래스 자체에 소속되어 있다.
      - 클래스 변수는 자바 프로그램을 시작할 때 딱 1개 만들어진다. 인스턴스와는 다르게 보통 여러 곳에서 공유하는 목적으로 사용된다.
  ```java
  public class DataCountMain3 {

      public static void main(String[] args) {
          Data3 data1 = new Data3("A");
          System.out.println(Data3.count);

          Data3 data2 = new Data3("B");
          System.out.println(Data3.count);
      }
  }
  ```
  - 코드를 보면 count 정적 변수에 접근하는 방법이 Data3.count와 같이 클래스명에 .(dot)을 사용하여 클래스에 직접 접근하는 것처럼 느껴진다.
  - static이 붙은 멤버 변수는 메서드 영역에서 관리한다. static이 붙은 멤버 변수 count는 인스턴스 영역에 생성되지 않는다. 대신 메서드 영역에서 이 변수를 관리한다.
  - Data3("A") 인스턴스를 생성하면 생성자가 호출된다.
  - 생성자에는 count++ 코드가 있다. count는 static이 붙은 정적 변수다. 정적 변수는 인스턴스 영역이 아니라 메서드 영역에서 관리한다. 따라서 이 경우 메서드 영역에 있는 count의 값이 하나 증가된다.
  - 참고로 Data3의 생성자와 같이 자신의 클래스에 있는 정적 변수라면 클래스명을 생략할 수 있다.
  - static 변수를 사용한 덕분에 공용 변수를 사용하여 편리하게 문제를 해결할 수 있다.
  - 변수와 생명주기
    - 지역 변수(매개변수 포함) : 지역 변수는 스택 영역에 있는 스택 프레임 안에 보관된다. 메서드가 종료되면 스택 프레임도 제거되는데 이 때 해당 스택 프레임에 포함된 지역 변수도 함께 제거된다. 따라서 생존 주기가 짧다.
    - 인스턴스 변수 : 인스턴스 변수는 힙 영역을 사용한다. 힙 영역은 GC가 발생하기 전까지는 생존하기 때문에 보통 지역 변수보다 생존 주기가 길다.
    - 클래스 변수 : 클래스 변수는 메서드 영역의 static 영역에 보관되는 변수이다. 메서드 영역은 프로그램 전체에서 사용하는 공용 공간이다. 클래스 변수는 해당 클래스가 JVM에 로딩되는 순간 생성된다. 그리고 JVM이 종료될 때까지 생명주기가 이어진다. 따라서 가장 긴 생명주기를 가진다.
    - static이 정적이라는 이유는 바로 여기에 있다. 힙 영역에 생성되는 인스턴스 변수는 동적으로 생성되고 제거된다. 반면 static인 정적 변수는 거의 프로그램 실행 시점에 만들어지고, 프로그램 종료 시점에 제거된다.
  - 정적 변수 접근법
    - static 변수는 클래스를 통해 바로 접근할 수 있고, 인스턴스를 통해서도 접근할 수 있다.
    ```java
    Data3 data3 = new Data3("C");
    // 인스턴스를 통한 접근
    System.out.println(data3.count);
    // 클래스를 통한 접근
    System.out.println(Data3.count);
    ```
    - 정적 변수의 경우 인스턴스를 통한 접근은 추천하지 않는다. 코드를 읽을 때 마치 인스턴스 변수에 접근하는 것처럼 오해할 수 있기 때문이다.
    - 정적 변수는 클래스에서 공용으로 관리하기 때문에 클래스를 통해서 접근하는 것이 더 명확하다.

5. **static 메서드**
  ```java
  public class DecoUtil1 {

      public String deco(String str) {
          String result = "*" + str + "*";
          return result;
      }
  }
  ```
  ```java
  public class DecoMain1 {

      public static void main(String[] args) {
          String s = "hello java";
          DecoUtil1 utils = new DecoUtil1();
          String deco = utils.deco(s);

          System.out.println(deco);
      }
  }
  ```
  - deco() 메서드를 호출하기 위해서는 DecoUtil1의 인스턴스를 먼저 생성해야 한다. 그런데 deco()라는 기능은 멤버 변수도 없고, 단순히 기능만 제공할 뿐이다. 인스턴스가 필요한 이유는 멤버 변수 등을 사용하는 목적이 큰데, 이 메서드는 사용하는 인스턴스 변수도 없고 단순히 기능만 제공한다.
  ```java
  public class DecoUtil1 {

      public static String deco(String str) {
          String result = "*" + str + "*";
          return result;
      }
  }
  ```
  ```java
  public class DecoMain1 {

      public static void main(String[] args) {
          String s = "hello java";
          String deco = DecoUtil1.deco(s);

          System.out.println(deco);
      }
  }
  ```
  - 메서드 앞에 static을 붙여 정적 메서드를 만들었다.
  - 이 정적 메서드는 정적 변수처럼 인스턴스 생성 없이 클래스 명을 통해 바로 호출할 수 있다.
  - static이 붙은 정적 메서드는 객체 생성 없이 클래스명 + . + 메서드 명으로 바로 호출할 수 있다.
  - 정적 메서드 덕분에 불필요한 객체 생성 없이 편리하게 메서드를 사용했다.
  - 클래스 메서드
    - 메서드 앞에도 static을 붙일 수 있다. 이것을 정적 메서드 또는 클래스 메서드라 한다. 클래스 메서드라는 용어는 인스턴스 생성 없이 마치 클래스에 있는 메서드를 바로 호출하는 것처럼 느껴지기 때문이다.
  - 인스턴스 메서드
    - static이 붙지 않은 메서드는 인스턴스를 생성해야 호출할 수 있다. 이것을 인스턴스 메서드라 한다.
  - 정적 메서드는 객체 생성 없이 클래스에 있는 메서드를 바로 호출할 수 있다는 장점이 있지만 정적 메서드는 언제나 사용할 수 있는 것이 아니다.
  - 정적 메서드 사용법
    - static 메서드는 static만 사용할 수 있다.
    - 클래스 내부의 기능을 사용할 때, 정적 메서드는 static이 붙은 정적 메서드나 정적 변수만 사용할 수 있다.
    - 클래스 내부의 기능을 사용할 때, 정적 메서드는 인스턴스 변수나 인스턴스 메서드를 사용할 수 없다.
    - 모든 곳에서 static을 호출할 수 있다.
    - 정적 메서드는 공용 기능이다. 따라서 접근 제어자만 허락한다면 클래스를 통해 모든 곳에서 static을 호출할 수 있다.
    ```java
    public class DecoData {

        private int instanceValue;
        private static int staticValue;

        public static void staticCall() {
            staticValue++;  // 정적 변수 접근
            staticMethod(); // 정적 메서드 접근
        }
        
        public void instanceCall() {
            instanceValue++;    // 인스턴스 변수 접근
            instanceMethod();   // 인스턴스 메서드 접근
            
            staticValue++;  // 정적 변수 접근
            staticMethod(); // 정적 메서드 접근
        }

        private void instanceMethod() {
            System.out.println(instanceValue);
        }

        private static void staticMethod() {
            System.out.println(staticValue);
        }
    }
    ```
    - staticCall() 메서드는 정적 메서드이다. 따라서 static만 사용할 수 있다. 정적 변수, 정적 메서드에는 접근할 수 있지만, static이 없는 인스턴스 변수나 인스턴스 메서드에 접근하면 컴파일 오류가 발생한다.
    - instanceCall() 메서드는 인스턴스 메서드이다. 모든 곳에서 공용인 static을 호출할 수 있다. 따라서 정적 변수, 정적 메서드는 물론 인스턴스 변수, 인스턴스 메서드에도 접근할 수 있다.
  - 정적 메서드가 인스턴스의 기능을 사용할 수 없는 이유
    - 정적 메서드는 클래스의 이름을 통해 바로 호출할 수 있다. 그래서 인스턴스처럼 참조값의 개념이 없다.
    - 특정 인스턴스의 기능을 사용하려면 참조값을 알아야 하는데, 정적 메서드는 참조값 없이 호출한다. 따라서 정적 메서드 내부에서 인스턴스 변수나 인스턴스 메서드를 사용할 수 없다.
    - 객체의 참조값을 직접 매개변수로 전달하면 정적 메서드는 인스턴스의 변수나 메서드를 호출할 수 있다.
  - 멤버 메서드의 종류
    - 인스턴스 메서드 : static이 붙지 않은 멤버 메서드
    - 클래스 메서드 : static이 붙은 멤버 메서드
    - static이 붙지 않은 멤버 메서드는 인스턴스를 생성해야 사용할 수 있고, 인스턴스에 소속되어 있다. 따라서 인스턴스 메서드라 한다. static이 붙은 멤버 메서드는 인스턴스와 무관하게 클래스에 바로 접근해서 사용할 수 있고, 클래스 자체에 소속되어 있다. 따라서 클래스 메서드라 한다.
  - 정적 메서드 활용
    - 정적 메서드는 객체 생성이 필요 없이 메서드의 호출만으로 필요한 기능을 수행할 때 주로 사용한다.
    - 간단한 메서드 하나로 끝나는 유틸리티성 메서드에 자주 사용한다.
  - 정적 메서드 접근법
    - static 메서드는 static 변수와 마찬가지로 클래스를 통해 바로 접근할 수 있고, 인스턴스를 통해서도 접근할 수 있다.
    ```java
    DecoData data3 = new DecoData();
    // 인스턴스를 통한 접근
    data3.staticCall();
    // 클래스를 통한 접근
    DecoData.staticCall();
    ```
    - 정적 메서드의 경우 인스턴스를 통한 접근은 추천하지 않는다. 코드를 읽을 때 마치 인스턴스 메서드에 접근하는 것처럼 오해할 수 있기 때문이다.
    - 정적 메서드는 클래스에서 공용으로 관리하기 때문에 클래스를 통해서 접근하는 것이 더 명확하다.
  - 정적 메서드를 사용할 때 해당 메서드를 자주 호출해야 한다면 static import 기능을 고려할 수 있다. 이 기능을 사용하면 클래스 명을 생략하고 메서드를 호출할 수 있다.
  ```java
  package static2;
  //import static static2.DecoData.staticCall;
  import static static2.DecoData.*;
  public class DecoDataMain {
      public static void main(String[] args) {
          staticCall(); // 클래스 명 생략 가능
      }
  }
  ```
  - 특정 클래스의 모든 정적 메서드에 적용하려면 *을 사용하면 된다.
  - import static은 정적 메서드뿐만 아니라 정적 변수에도 사용할 수 있다.
  - 인스턴스 생성 없이 실행하는 가장 대표적인 메서드가 바로 main() 메서드이다. main() 메서드는 프로그램을 시작하는 시작점이 되는데, 객체를 생성하지 않아도 main() 메서드가 작동한다.
  - 정적 메서드는 정적 메서드만 호출할 수 있기에 정적 메서드인 main()이 호출하는 메서드에는 정적 메서드를 사용한다.


