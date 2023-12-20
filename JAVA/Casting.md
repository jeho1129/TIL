# <center>TIL<center>

# 형변환 :memo:

1. **자동 형변환**
  - 작은 범위에서 큰 범위로는 당연히 값을 넣을 수 있다.(int -> long -> double)
  - 큰 범위에서 작은 범위는 다음과 같은 문제가 발생할 수 있다.
    - 소수점 버림
    - 오버플로우
  - 자바는 기본적으로 작은 범위에서 큰 범위로의 대입은 허용한다.
  - 예시
    ```java
    public class Casting1 {
        public static void main(String[] args) {
            int intValue = 10;
            long longValue;
            double doubleValue;

            longValue = intValue;   // int -> long
            System.out.println(longValue);
            
            doubleValue = intValue; // int -> double
            System.out.println(doubleValue);
        }
    }
    ```
  - 자바는 기본적으로 같은 타입에 값을 대입할 수 있다.
  - long -> double의 경우에도 double은 부동 소수점을 사용하기 때문에 더 큰 숫자 범위를 표현한다. 따라서 대입할 수 있다.
  - 하지만 결국 대입하는 타입을 맞추어야 하기 때문에 개념적으로는 다음과 같이 동작한다.
    ```java
    int intValue = 10;
    double doubleValue;
    doubleValue = intValue;
    doubleValue = (double) intValue;  // 형 맞추기
    doubleValue = (double) 10;  // 변수 값 읽기
    doubleValue = 10.0;  // 형변환
    ```
    - 이렇게 앞에 (double)과 같이 적어주면 int형이 double형으로 형이 변한다. 이렇게 형이 변경되는 것을 형변환이라 한다.
    - 작은 범위 숫자 타입에서 큰 범위 숫자 타입으로의 대입은 개발자가 이렇게 직접 형변환을 하지 않아도 된다. 이런 과정이 자동으로 일어나기 때문에 자동 형변환, 또는 묵시적 형변환이라 한다.

2. **명시적 형변환**
  - 큰 범위에서 작은 범위로의 대입은 명시적 형변환이 필요하다.
  - 예시
    ```java
    public class Casting2 {
        public static void main(String[] args) {
            double doubleValue = 1.5;
            int intValue = 0;

            // intValue = doubleValue;  // 컴파일 오류 발생
            intValue = (int) doubleValue;   // 형변환
            System.out.println(intValue);   // 1
        }
    }
    ```
    - int형은 double형보다 숫자의 표현 범위가 작다. 그리고 실수를 표현할 수도 없다. 따라서 이 경우 숫자가 손실되는 문제가 발생할 수 있다.
    - 이런 문제는 매우 큰 버그를 유발할 수 있다. 예를 들어, 은행 프로그램이 고객에게 은행 이자를 계산해서 입금해야 하는데 만약 이런 코드가 아무런 오류 없이 수행된다면 큰 문제를 만들 수 있다. 그래서 자바는 이런 경우 컴파일 오류를 발생시킨다.
    - 하지만, 만약 이런 위험을 개발자가 직접 감수하고도 값을 대입하고 싶다면 데이터 타입을 강제로 변경할 수 있다.
    - 형변환은 다음과 같이 변경하고 싶은 데이터 타입을 (int)와 같이 괄호를 사용해서 명시적으로 입력하면 된다.
      ```java
      intValue = (int) doubleValue;
      ```
    - 이는 개발자가 직접 형변환 코드를 입력한다고 해서 명시적 형변환이라 한다.
  - 명시적 형변환 과정
    ```java
    intValue = (int) doubleValue;
    intValue = (int) 1.5; // doubleValue에 있는 값을 읽는다.
    intValue = 1; // int로 형변환된다. intValue에 int형인 숫자 1을 대입한다.
    ```
    - 참고로 형변환을 한다고 해서 doubleValue 자체의 타입이 변경되거나 그 안에 있는 값이 변경되는 것은 아니다.
    - doubleValue에서 읽은 값을 형변환하는 것이다. doubleValue 안에 들어있는 값은 1.5로 그대로 유지된다.
    - 참고로 변수의 값은 대입연산자(=)를 사용해서 직접 대입할 때만 변경된다.

3. **형변환과 오버플로우**
  ```java
  public class Casting3 {
      public static void main(String[] args) {
          long maxIntValue = 2147483647;  // int 최고값
          long maxIntOver = 2147483648L;  // int 최고값 + 1
          int intValue = 0;

          intValue = (int) maxIntValue;
          System.out.println(intValue);   // 2147483647

          intValue = (int) maxIntOver;
          System.out.println(intValue);   // -2147483648
      }
  }
  ```
  - maxIntValue의 경우 int로 표현할 수 있는 가장 큰 숫자를 입력했기 때문에 long -> int로 형변환을 해도 문제가 없다.
  - 하지만, maxIntOver의 경우 int로 표현할 수 있는 가장 큰 숫자보다 1이 큰 숫자를 입력했기 때문에 int 범위를 넘어가서 마지막에 L을 붙여서 long형을 사용해야한다. 이 경우, int로 표현할 수 있는 범위를 넘기 때문에 long -> int로 형변환하면 문제가 발생한다.
  - 결과를 보면 -2147483648이라는 전혀 다른 숫자가 출력된다. 이렇게 기존 범위를 초과해서 표현하게 되면 전혀 다른 숫자가 표현되는데, 이런 현상을 오버플로우라 한다.
  - 보통 오버플로우가 발생하면 마치 시계가 한 바퀴 돈 것처럼 다시 처음부터 시작한다. 참고로 -2147483648 숫자는 int의 가장 작은 숫자이다.
  - 중요한 것은 오버플로우가 발생하는 것 자체가 문제라는 점이다. 이 경우 단순히 대입하는 변수의 타입을 int -> long으로 변경해서 사이즈를 늘리면 오버플로우 문제가 해결된다.

4. **계산과 형변환**
  - 형변환은 대입뿐만 아니라, 계산을 할 때도 발생한다.
  - 예시
    ```java
    public class Casting4 {
        public static void main(String[] args) {
            int div1 = 3 / 2;
            System.out.println(div1);   // 1
            // int / int이므로 int타입으로 결과가 나온다.
            double div2 = 3 / 2;
            System.out.println(div2);   // 1.0
            // int / int이므로 int타입으로 결과가 나온다.
            // div2는 double이므로 int -> double에 대입해야 하므로 자동 형변환이 발생한다.
            // 따라서 1(int) -> 1.0(double)로 자동 형변환이 되었다.
            double div3 = 3.0 / 2;
            System.out.println(div3);   // 1.5
            // double / int이므로 double / double로 형변환이 발생한다.
            double div4 = (double) 3 / 2;
            // 명시적 형변환을 사용했다.
            System.out.println(div4);   // 1.5
            // double / int이므로 double / double로 형변환이 발생한다.

            int a = 3;
            int b = 2;
            double result = (double) a / b;
            System.out.println(result); // 1.5
        }
    }
    ```
  - 자바에서 계산은 다음 2가지를 기억하자
    1. 같은 타입끼리의 계산은 같은 타입의 결과를 낸다.
      - int + int는 int를, double + double은 double의 결과가 나온다.
    2. 서로 다른 타입의 계산은 큰 범위로 자동 형변환이 일어난다.
      - int + long은 long + long으로 자동 형변환이 일어난다.
      - int + double은 double + double로 자동 형변환이 일어난다.


    
