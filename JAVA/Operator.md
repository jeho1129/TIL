# <center>TIL<center>

# 연산자 :memo:

1. **연산자와 피연산자**
  - 연산자(operator) : 연산 기호
  - 피연산자(operand) : 연산 대상

2. **산술 연산자**
  - 산술 연산자는 주로 숫자를 계산하는 데 사용된다.
  - +, -, *, /, %
  - 예제
    ```java
    public class Operator1 {
        public static void main(String[] args) {
            // 변수 초기화
            int a = 5;
            int b = 2;
            // 덧셈
            int sum = a + b;
            System.out.println("a + b = " + sum);   // 출력 a + b = 7
            // 뺄셈
            int diff = a - b;
            System.out.println("a - b = " + diff);  // 출력 a - b = 3
            // 곱셈
            int multi = a * b;
            System.out.println("a * b = " + multi);  // 출력 a * b = 10
            // 나눗셈
            int div = a / b;
            System.out.println("a / b = " + div);   // 출력 a / b = 2 (div가 정수형 변수이므로)
            // 나머지
            int mod = a % b;
            System.out.println("a % b = " + mod);   // 출력 a % b = 1
        }
    }
    ```
    - 5 / 2의 결과는 2.5가 되어야 하지만, 결과는 소수점이 제거된 2가 나왔다.
      - 자바에서 같은 int형끼리 계산하면 계산 결과도 같은 int 형을 사용한다. int 형은 정수이기 때문에 소수점 이하를 포함할 수 없다.
  - 나누기는 0으로 나눌 수 없다.

3. **문자열 더하기**
  - 자바는 문자열에도 + 연산자를 사용할 수 있다. 문자열에 + 연산자를 사용하면 두 문자를 연결할 수 있다.
  - 예제
    ```java
    public class Operator2 {
        public static void main(String[] args) {
            // 문자열과 문자열 더하기 1
            String result1 = "hello " + "world";
            System.out.println(result1);    // 출력 hello world
            // 문자열과 문자열 더하기 2
            String s1 = "string1";
            String s2 = "string2";
            String result2 = s1 + s2;
            System.out.println(result2);    // 출력 string1string2
            // 문자열과 숫자 더하기 1
            String result3 = "a + b = " + 10;
            System.out.println(result3);    // 출력 a + b = 10
            // 문자열과 숫자 더하기 2
            int num = 20;
            String str = "a + b = ";
            String result4 = str + num;
            System.out.println(result4);    // 출력 a + b = 20
        }
    }
    ```
    - 자바에서 문자와 숫자를 더하면 숫자를 문자열로 변경한 다음 서로 더한다.
    - 변수에 담겨 있어도 문자와 숫자를 더하면 문자가 된다.
    - 자바는 문자열인 String 타입에 다른 타입을 더하는 경우 대상 타입을 문자열로 변경한다. 쉽게 이야기해서 문자열에 더하는 것은 다 문자열이 된다.

4. **연산자 우선순위**
  - 예제
    ```java
    public class Operator3 {
        public static void main(String[] args) {
            int sum1 = 1 + 2 * 3;   // 1 + (2 * 3)
            int sum2 = (1 + 2) * 3;
            System.out.println("sum1 = " + sum1);   // sum1 = 7
            System.out.println("sum2 = " + sum2);   // sum2 = 9
        }
    }
    ```
    - 연산자 우선순위를 변경하려면 수학과 마찬가지로 괄호 ()를 사용하면 된다.
  - 예제 2
    ```java
    public class Operator4 {
        public static void main(String[] args) {
            int sum3 = 2 * 2 + 3 * 3;   // (2 * 2) + (3 * 3)
            int sum4 = (2 * 2) + (3 * 3);   // sum3과 같다.
            System.out.println("sum3 = " + sum3);
            System.out.println("sum4 = " + sum4);
        }
    }
    ```
    - 수식이 복잡한 경우에는 괄호를 명시적으로 사용하는 것이 더 명확하고 이해하기 쉽다.
    - 코드를 몇 자 줄여서 모호하거나 복잡해지는 것보다는 코드가 더 많더라도 명확하고 단순한 것이 더 유지보수하기 좋다.
    - 연산자 우선순위가 애매하거나 조금이라도 복잡하다면 언제나 괄호를 고려하자.
  - 연산자 우선순위
    - 실무에서는 연산자 우선순위를 외우지 않는다.
    1. 상식선에서 우선순위를 사용하자
    2. 애매하면 괄호를 사용하자
      - 코드를 봤을 때 연산자 우선순위를 고민해야할 것 같으면, 나 뿐만 아니라 모든 사람이 그렇게 느낀다는 것이다. 이 때는 다음과 같이 괄호를 사용해서 우선순위를 명시적으로 지정하면 된다.

5. **증감 연산자**
  - 증가 및 감소 연산자를 줄여서 증감 연산자라 한다.
  - 증감 연산자는 ++와 --로 표현되며, 이들은 변수의 값을 1만큼 증가시키거나 감소시킨다.
  - 프로그래밍에서는 값을 1씩 증가하거나, 감소할 때가 아주 많기 때문에 이런 편의 기능을 제공한다.
  - 예제
    ```java
    public class OperatorAdd1 {
        public static void main(String[] args) {
            int a = 0;
            a = a + 1;
            System.out.println("a = " + a);  // 1
            a = a + 1;
            System.out.println("a = " + a);  // 2
            // 증감 연산자
            ++a;  // a = a + 1
            System.out.println("a = " + a);  // 3
            ++a;
            System.out.println("a = " + a);  // 4
        }
    }
    ```
    - a = a + 1을 ++a로 간단히 표현할 수 있는 것이 증감 연산자이다.
    - 값을 하나 감소할 때는 --a와 같이 표현하면 된다.(a = a - 1)
  - 전위, 후위 증감연산자
    - 증감 연산자는 피연산자 앞에 두거나 뒤에 둘 수 있으며, 연산자의 위치에 따라 연산이 수행되는 시점이 달라진다.
    - ++a : 증감 연산자를 피연산자 앞에 둘 수 있다. 전위 증감 연산자라 한다.
    - a++ : 증감 연산자를 피연산자 뒤에 둘 수 있다. 후위 증감 연산자라 한다.
    - 예제
      ```java
      public class OperatorAdd2 {
          public static void main(String[] args) {
              // 전위 증감 연산자
              int a = 1;
              int b = 0;
              b = ++a;  // a의 값을 먼저 증가시키고, 그 결과를 b에 대입
              System.out.println("a = " + a + ", b = " + b);  // a = 2, b = 2
              // 후위 증감 연산자
              a = 1;
              b = 0;
              b = a++;  // a의 현재 값을 b에 먼저 대입하고, 그 후 a 값을 증가시킴
              System.out.println("a = " + a + ", b = " + b);  // a = 2, b = 1
          }
      }
      ```
    - 증감 연산자가 변수 앞에 오는 경우를 전위 증감 연산자라 하며, 이 경우에는 증감 연산이 먼저 수행된 후 나머지 연산이 수행된다.
      - b = ++a
        a = a + 1
        b = a
    - 증감 연산자가 변수 뒤에 오는 경우를 후위 증감 연산자라 하며, 이 경우에는 다른 연산이 먼저 수행된 후 증감 연산이 수행된다.
      - b = a++
        b = a
        a = a + 1
    - 참고로 다음과 같이 증감 연산자를 단독으로 사용하는 경우에는 다른 연산이 없기 때문에, 본인의 값만 증가한다. 따라서 전위이든 후위이든 둘 다 결과가 같다.

6. **비교 연산자**
  - 비교 연산자는 두 값을 비교하는 데 사용된다. 비교 연산자는 주로 조건문과 함께 사용된다.
  - 종류
    - == : 동등성
    - != : 불일치
    - >, < : 크거나 작다.
    - >=, <= : 크거나 같다 or 작거나 같다.
  - 비교 연산자를 사용하면 참 또는 거짓이라는 결과가 나온다.
  - 예제
    ```java
    public class Comp1 {
        public static void main(String[] args) {
            int a = 2;
            int b = 3;
            System.out.println(a == b);  // false
            System.out.println(a != b);  // true
            System.out.println(a > b);  // false
            System.out.println(a < b);  // true
            System.out.println(a >= b);  // false
            System.out.println(a <= b);  // true
            // 결과를 boolean 변수에 담을 수 있다.
            boolean result = a == b;
            System.out.println(result);  // false
        }
    }
    ```
  - 문자열 비교
    - 문자열이 같은지 비교할 때는 ==이 아니라 .equals() 메서드를 사용해야 한다.
    - 예제
      ```java
      public class Comp2 {
          public static void main(String[] args) {
              String str1 = "문자열1";
              String str2 = "문자열2";
              boolean result1 = "hello".equals("hello");  // 리터럴 비교
              boolean result2 = str1.equals("문자열1");  // 문자열 변수, 리터럴 비교
              boolean result3 = str1.equals(str2);  // 문자열 변수 비교
              System.out.println(result1);  // true
              System.out.println(result2);  // true
              System.out.println(result3);  // false
          }
      }
      ```
    - 현재 문장 자동 완성 단축키 : Ctrl + Shift + Enter

7. **논리 연산자**
  - 논리 연산자는 boolean 형인 true, false를 비교하는 데 사용된다.
  - 논리 연산자
    - && : AND, 두 피연산자가 모두 참이어야 true를 반환
    - || : OR, 두 피연산자 중 하나라도 참이면 true를 반환
    - ! : NOT, 피연산자의 논리적 부정을 반환
  - 예제
    ```java
    public class Logical1 {
        public static void main(String[] args) {
            System.out.println("&& : AND 연산");
            System.out.println(true && true);   // true
            System.out.println(true && false);  // false
            System.out.println(false && false); // false
            System.out.println("|| : OR 연산");
            System.out.println(true || true);   // true
            System.out.println(true || false);  // true
            System.out.println(false || false); // false
            System.out.println("! : NOT 연산");
            System.out.println(!true);  // false
            System.out.println(!false); // true
        }
    }
    ```
  - 논리 연산자의 활용
    ```java
    public class Logical2 {
        public static void main(String[] args) {
            int a = 15;
            // a는 10보다 크고, 20보다 작다.
            boolean result = a > 10 && a < 20;  // (a > 10) && (a < 20)
            System.out.println("result = " + result);   // result = true
        }
    }
    ```

8. **대입 연산자**
  - 대입 연산자(=)는 값을 변수에 할당하는 연산자다. 이 연산자를 사용하면 변수에 값을 할당할 수 있다.
  - 축약(복합) 대입 연산자
    - 산술 연산자와 대입 연산자를 한번에 축약해서 사용할 수 있는데, 이것을 축약 연산자라 한다.
    - 종류 : +=, -=, /=, %=
    - 예시
      - i = i + 3 -> i += 3
      - i = i * 4 -> i *= 4