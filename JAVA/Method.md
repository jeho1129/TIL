# <center>TIL<center>

# 메서드 :memo:

1. **메서드**
  - 자바에서는 함수를 메서드라 한다.
  - 메서드는 함수의 한 종류이다.
  - 예시
    ```java
    public class Method1 {
        public static void main(String[] args) {
            // 계산
            int sum1 = add(5, 10);
            System.out.println(sum1);
        }
        // add 메서드
        public static int add(int a, int b) {
            int sum = a + b;
            return sum;
        }
    }
    ```
    - 메서드는 크게 메서드 선언과 메서드 본문으로 나눌 수 있다.
    - 메서드 선언
      ```java
      public static int add(int a, int b)
      ```
      - 메서드의 선언 부분으로, 메서드 이름, 반환 타입, 매개변수 목록을 포함한다.
      - 메서드 선언 정보를 통해 다른 곳에서 해당 메서드를 호출할 수 있다.
      - public static
        - public : 다른 클래스에서 호출할 수 있는 메서드라는 뜻이다.
        - static : 객체를 생성하지 않고 호출할 수 있는 정적 메서드라는 뜻이다.
        - 단순하게 메서드를 만들 때 둘을 사용해야 한다고 생각하면 된다.
      - int add(int a, int b)
        - int : 반환 타입을 정의한다. 메서드의 실행 결과를 반환할 때 사용할 반환 타입을 지정한다.
        - add : 메서드에 이름을 부여한다. 이 이름으로 메서드를 호출할 수 있다.
        - (int a, int b) : 메서드를 호출할 때 전달하는 입력 값을 정의한다. 이 변수들은 해당 메서드 안에서만 사용된다. 이렇게 메서드 선언에 사용되는 변수를 매개변수(parameter)라 한다.
    - 메서드 본문
      ```java
      {
          int sum = a + b;
          return sum;
      }
      ```
      - 메서드가 수행해야 하는 코드 블록이다.
      - 메서드를 호출하면 메서드 본문이 순서대로 실행된다.
      - 메서드 본문은 블랙박스이다. 메서드를 호출하는 곳에서는 메서드 선언은 알지만 메서드 본문은 모른다.
      - 메서드의 실행 결과를 반환하려면 return문을 사용해야 한다. return문 다음에 반환할 결과를 적어주면 된다.
      - return sum : sum 변수에 들어있는 값을 반환한다.
    - 메서드 호출
      ```java
      int sum1 = add(5, 10);
      ```
      - 앞서 정의한 메서드를 호출해서 실행하려면 메서드 이름에 입력 값을 전달하면 된다.
      - 메서드를 호출하면 메서드는 계산을 끝내고 결과를 반환한다.
      - 메서드 호출 시 실행 순서
        1. 메서드 호출
        2. 파라미터 변수들이 전달되면서 메서드가 수행된다.
        3. return을 사용해서 메서드 실행의 결과인 sum을 반환한다.
        4. 메서드 호출 결과로 메서드에서 반환한 값 sum이 sum1에 대입된다.
      - 메서드 호출이 끝나면 더 이상 해당 메서드가 사용한 메모리를 낭비할 이유가 없다. 따라서 메서드 호출이 끝나면 메서드 정의에 사용한 파라미터 변수인 int a, int b와 그 안에서 정의한 int sum도 모두 제거된다.
  - 메서드 호출과 용어 정리
    - 메서드를 호출할 때는 메서드에 넘기는 값과 파라미터의 타입이 맞아야 한다. 물론 넘기는 값과 파라미터의 순서와 갯수도 맞아야 한다.
    ```java
    // 호출
    call("hello", 20)
    // 메서드 정의
    int call(String str, int age)
    ```
    - 인수(Argument)
      - "hello", 20처럼 넘기는 값을 인수라 한다.
      - 실무에서는 Argument, 인수, 인자라는 용어를 모두 사용한다.
    - 매개변수(Parameter)
      - 메서드를 정의할 때 선언한 변수인 String str, int age를 매개변수라 한다.
      - 메서드를 호출할 때 인수를 넘기면, 그 인수가 매개변수에 대입된다.
      - 실무에서는 매개변수, Parameter 용어를 모두 사용한다.
    - 즉, 인수라는 용어는 메서드 내부로 들어가는 값을 의미한다. 인자도 같은 의미이다.
    - 매개변수는 메서드의 호출부와 메서드 내부 사이에서 값을 전달하는 역할을 하는 변수라는 뜻이다.

2. 메서드 정의
  ```java
  public static int add(int a, int b) {
    // 메서드 본문, 실행 코드
  }

  제어자 반환타입 메서드이름(매개변수 목록) {
    메서드 본문
  }
  ```
  - 제어자(Modifier) : public, static과 같은 부분이다.
  - 반환 타입(Return Type) : 메서드가 실행된 후 반환하는 데이터의 타입을 지정한다. 메서드가 값을 반환하지 않는 경우, 없다는 뜻의 void를 사용해야 한다.(void print(String str))
  - 메서드 이름 : 메서드의 이름이다. 이 이름은 메서드를 호출하는 데 사용된다.
  - 매개변수 : 입력 값으로, 메서드 내부에서 사용할 수 있는 변수이다. 매개변수는 옵션이다. 입력값이 필요없는 메서드는 매개변수를 지정하지 않아도 된다.
  - 메서드 본문 : 실제 메서드의 코드가 위치한다. 중괄호 사이에 코드를 작성한다.
  - 매개변수가 없거나 반환 타입이 없는 경우
    ```java
    public class Method2 {
        public static void main(String[] args) {
            printHeader();
        }

        public static void printHeader() {
            System.out.println("프로그램을 시작합니다.");
            return; // void의 경우 생략 가능
        }
    }
    ```
    - 매개변수가 없는 경우
      - 선언 : printHeader()와 같이 매개변수를 비워두고 정의하면 된다.
      - 호출 : printHeader();와 같이 인수를 비워두고 호출하면 된다.
    - 반환 타입이 없는 경우
      - 선언 : public static void와 같이 반환 타입을 void로 정의하면 된다.
      - 호출 : 반환 타입이 없으므로 메서드만 호출하고 반환 값을 받지 않으면 된다. 반환 값을 받을 경우 컴파일 오류가 발생한다.
    - void와 return 생략
      - 모든 메서드는 항상 return을 호출해야 한다. 그런데 반환 타입 void의 경우에는 예외로 생략해도 된다. 자바가 반환 타입이 없는 경우에는 return을 마지막 줄에 넣어준다. 참고로 return을 만나면 해당 메서드는 종료된다.

3. 반환 타입
  - 반환 타입이 있으면 반드시 값을 반환해야 한다.
  - 반환 타입이 있는 메서드는 반드시 return을 사용해서 값을 반환해야 한다.
  - 이 부분은 특히 조건문과 함께 사용할 때 주의해야 한다.
  - 예시
    ```java
    public class Method3 {
        public static void main(String[] args) {
            boolean result = odd(2);
            System.out.println(result);
        }

        public static boolean odd(int i) {
            if (i % 2 == 1) {
                return true;
            }
        }
    }
    ```
    - 이 코드에서 if 조건문이 만족할 때는 true가 반환되지만, 조건을 만족하지 않는 경우에는 return이 실행되지 않는다. 따라서 이 코드를 실행하면 return이 누락되었다는 컴파일 오류가 발생한다.
  - return을 만나면 그 즉시 메서드를 빠져나간다.
  - 예시
    ```java
    public class Method4 {
        public static void main(String[] args) {
            checkAge(10);
        }

        public static void checkAge(int age) {
            if (age < 18) {
                System.out.println("미성년자는 출입이 불가능합니다.");
                return;
            }

            System.out.println("입장하세요.");
        }
    }
    ```
    - 18세 미만의 경우 출력문 이후 바로 return이 수행된다. 따라서 다음 로직을 수행하지 않고 해당 메서드를 빠져나온다.
  - 반환 값 무시 : 반환 타입이 있는 메서드를 호출했는데 만약 반환 값이 필요없다면 사용하지 않아도 된다.

4. 메서드 호출과 값 전달
  - **자바는 항상 변수의 값을 복사해서 대입한다.**(매우 중요)
  - 메서드 호출과 값 복사
    ```java
    public class Method5 {
        public static void main(String[] args) {
            int num1 = 5;
            System.out.println("1 : " + num1);  // 5
            changeNumber(num1);
            System.out.println("4 : " + num1);  // 5
        }

        public static void changeNumber(int num2) {
            System.out.println("2 : " + num2);  // 5
            num2 = num2 * 2;
            System.out.println("3 : " + num2);  // 10
        }
    }
    ```
    - changeNumber(num1) 호출 시점 : num1의 값 5를 읽고 복사해서 num2에 전달
    - changeNumber 메서드 실행 중 : num2의 변경은 num1에 영향을 주지 않는다.
    - 결과적으로 매개변수 num2의 값만 10으로 변경되고 num1의 값은 변경되지 않고 기존 값인 5로 유지된다. 자바는 항상 값을 복사해서 전달하기 때문에 num2의 값을 바꾸더라도 num1에는 영향을 주지 않는다.
  - 메서드 호출과 이름이 같은 변수
    ```java
    public class Method6 {
        public static void main(String[] args) {
            int number = 5;
            System.out.println("1 : " + number);  // 5
            changeNumber(number);
            System.out.println("4 : " + number);  // 5
        }

        public static void changeNumber(int number) {
            System.out.println("2 : " + number);  // 5
            number = number * 2;
            System.out.println("3 : " + number);  // 10
        }
    }
    ```
    - 이번에는 main()에 정의한 변수와 메서드의 매개변수 이름이 둘 다 number로 같다.
    - main()도 사실 메서드이다. 각각의 메서드 안에서 사용하는 변수는 서로 완전히 분리된 다른 변수이다. 물론 이름이 같아도 완전히 다른 변수이다. 따라서 main()의 number와 changeNumber()의 number는 서로 다른 변수이다.
  - 메서드 호출과 값 반환 받기
    - 메서드를 사용해서 값을 변경하려면 메서드의 호출 결과를 반환 받아서 사용하면 된다.
    - 예시
      ```java
      public class Method7 {
          public static void main(String[] args) {
              int num1 = 5;
              System.out.println(num1);  // 5
              num1 = changeNumber(num1);
              System.out.println(num1);  // 10
          }

          public static int changeNumber(int num2) {
              num2 = num2 * 2;
              return num2;
          }
      }
      ```

5. 메서드와 형변환
  - 메서드를 호출할 때도 형변환이 적용된다.
  - 명시적 형변환
    ```java
    public class Method8 {
        public static void main(String[] args) {
            double number = 1.5;
            // printNumber(number);  // double을 int형에 대입하므로 컴파일 오류
            printNumber((int) number);  // 명시적 형변환을 사용해 double을 int로 변환
        }

        public static void printNumber(int n) {
            System.out.println(n);
        }
    }
    ```
    - 메서드를 호출하는데 인자와 매개변수의 타입이 맞지 않다면 컴파일 오류가 발생한다.
    - 이 경우, 메서드 호출이 꼭 필요하다면 명시적 형변환을 사용해야한다.
  - 자동 형변환
    - 메서드를 호출할 때 매개변수에 값을 전달하는 것도 결국 변수에 값을 대입하는 것이다. 따라서 자동 형변환이 그대로 적용된다.
    ```java
    public class Method9 {
        public static void main(String[] args) {
            int number = 100;
            printNumber(number);  // 100.0
        }

        public static void printNumber(double n) {
            System.out.println(n);
        }
    }
    ```
    - double형 매개변수에 int형 인수를 전달하면 문제없이 잘 동작한다.(double이 더 큰 숫자 범위이므로 자동 형변환 적용)
  - 즉, 메서드를 호출할 때는 전달하는 인수의 타입과 매개변수의 타입이 맞아야 한다. 단, 타입이 달라도 자동 형변환이 가능한 경우에는 호출할 수 있다.

6. 메서드 오버로딩
  - 자바는 메서드의 이름뿐만 아니라 매개변수 정보를 함께 사용해서 메서드를 구분할 수 있기에 이름이 같고, 매개변수가 다른 메서드를 정의할 수 있다.
  ```java
  add(int a, int b)
  add(int a, int b, int c)
  add(double a, double b)
  ```
  - 이렇게 이름이 같고 매개변수가 다른 메서드를 여러 개 정의하는 것을 메서드 오버로딩(Overloading)이라 한다.
  - 오버로딩은 번역하면 과적인데, 과하게 물건을 담았다는 뜻이다. 따라서 같은 이름의 메서드를 여러 개 정의했다고 이해하면 된다.
  - 오버로딩 규칙
    - 메서드의 이름이 같아도 매개변수의 타입 및 순서가 다르면 오버로딩을 할 수 있다. 참고로 반환 타입은 인정하지 않는다.
    - 다음 케이스는 메서드 이름과 매개변수 타입이 같으므로 컴파일 오류가 발생한다.
      ```java
      int add(int a, int b)
      double add(int a, int b)
      ```
    - 메서드 시그니쳐(method signature)
      - 메서드 시그니쳐 = 메서드 이름 + 매개변수 타입(순서)
      - 메서드 시그니쳐는 자바에서 메서드를 구분할 수 있는 고유한 식별자나 서명을 뜻한다. 메서드 시그니쳐는 메서드의 이름과 매개변수 타입(순서 포함)으로 구성되어 있다. 즉, 메서드를 구분할 수 있는 기준이다. 자바 입장에서는 각각의 메서드를 고유하게 구분할 수 있어야 어떤 메서드를 호출할 지 결정할 수 있다.
      - 메서드 이름이 같아도 메서드 시그니쳐가 다르면 다른 메서드로 간주한다. 
      - 반환 타입은 시그니쳐에 포함되지 않는다.
  - 예시 1
    ```java
    public class Method10 {
        public static void main(String[] args) {
            System.out.println(add(1, 2));
            System.out.println(add(1, 2, 3));
        }

        public static int add(int a, int b) {
            return a + b;
        }

        public static int add(int a, int b, int c) {
            return a + b + c;
        }
    }
    ```
  - 예시 2
    ```java
    public class Method11 {
        public static void main(String[] args) {
            myMethod(1, 1.2);
            myMethod(1.2, 1);
        }

        public static void myMethod(int a, double b) {
            System.out.println("int a, double b");
        }

        public static void myMethod(double a, int b) {
            System.out.println("double a, int b");
        }
    }
    ```