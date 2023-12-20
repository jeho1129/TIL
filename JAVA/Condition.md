# <center>TIL<center>

# 조건문 :memo:

1. **조건문**
  - 특정 조건에 따라서 다른 코드를 실행하는 것을 조건문이라 한다.
  - 조건문에는 if문, switch문이 있다.

2. **if문**
  - if문은 특정 조건이 참인지 확인하고, 그 조건이 참인 경우에만 특정 코드 블록을 실행한다.
  - 예시
    ```java
    public class If1 {

        public static void main(String[] args) {
            int age = 20;   // 사용자 나이
            if (age >= 18) {   // true
                System.out.println("성인입니다.");
            }

            if (age < 18) {   // false
                System.out.println("미성년자입니다.");
            }
        }
    }
    ```

3. **else문**
  - else문은 if문에서 만족하는 조건이 없을 때 실행하는 코드를 제공한다.
    ```java
    if (condition) {
      // 조건이 참일 때 실행되는 코드
    } else {
      // 만족하는 조건이 없을 때 실행되는 코드
    }
    ```
  - 예시
    ```java
    public class If2 {
        public static void main(String[] args) {
            int age = 20;
            if (age >= 18) {
                System.out.println("성인입니다.");
            } else {
                System.out.println("미성년자입니다.");
            }
        }
    }
    ```

4. **else if**
  - else if문은 앞선 if문의 조건이 거짓일 때 다음 조건을 검사한다. 만약 앞선 if문이 참이라면 else if를 실행하지 않는다.
    ```java
    if (condition1) {
      // 조건 1이 참일 때 실행되는 코드
    } else if (condition2) {
      // 조건 1이 거짓이고, 조건 2가 참일 때 실행되는 코드
    } else if (condition3) {
      // 조건 2가 거짓이고, 조건 3이 참일 때 실행되는 코드
    } else {
      // 모든 조건이 거짓일 때 실행되는 코드
    }
    ```
  - 예시
    ```java
    public class If3 {
        public static void main(String[] args) {
            int age = 14;
            if (age <= 7) {
                System.out.println("미취학");
            } else if (age <= 13) {
                System.out.println("초등학생");
            } else if (age <= 16) {
                System.out.println("중학생");
            } else if (age <= 19) {
                System.out.println("고등학생");
            } else {
                System.out.println("성인");
            }
        }
    }
    ```

5. **if문과 else if문**
  - if문에 else if를 함께 사용하는 것은 서로 연관된 조건일 때 사용한다. 그런데 서로 관련이 없는 독립 조건이면 else if를 사용하지 않고 if문을 각각 따로 사용해야 한다.
  - if문에 여러 조건이 있다고 항상 if-else로 묶어서 사용할 수 있는 것은 아니다. 조건이 서로 영향을 주지 않고 각각 수행해야 하는 경우에는 else if문을 사용하면 안되고, 대신에 여러 if문을 분리해서 사용해야 한다.
  - 여러 독립적인 조건을 검사해야 하는 경우가 그런 상황의 대표적인 예시다. 즉, 각 조건이 다른 조건과 연관되지 않고, 각각의 조건에 대해 별도의 작업을 수행해야 할 때 이런 상황이 발생한다.
  - 예시
    ```java
    public class If4 {
        public static void main(String[] args) {
            int price = 10000;
            int age = 10;
            int discount = 0;

            if (price >= 10000) {
                discount = discount + 1000;
                System.out.println("10000원 이상 구매, 1000원 할인");
            }

            if (age <= 10) {
                discount = discount + 1000;
                System.out.println("어린이 1000원 할인");
            }

            System.out.println("총 할인 금액 : " + discount + "원");
        }
    }
    ```

6. **참고**
  - if문 다음에 실행할 명령어 하나만 있을 경우에는 {} 중괄호를 생략할 수 있다. else, else if도 마찬가지다.
  - 문장이 두 개 이상 있을 경우에는 if문 안에 포함하려면 {}를 사용해야 한다.
  - 하지만 if문의 명령이 한 개만 있을 경우에도 다음과 같은 이유로 중괄호를 사용하는 것이 좋다.
    - 가독성 : 중괄호를 사용하면 코드를 더 읽기 쉽게 만들어 준다. 조건문의 범위가 명확하게 표시되므로 코드의 흐름을 더 쉽게 이해할 수 있다.
    - 유지보수성 : 중괄호를 사용하면 나중에 코드를 수정할 때 오류를 덜 발생시킬 수 있다. 예를 들어, if문에 또 다른 코드를 추가하려고 할 때, 중괄호가 없으면 이 코드가 if문의 일부라는 것이 명확하지 않을 수 있다.

7. **switch문**
  - switch문은 if문을 조금 더 편리하게 사용할 수 있는 기능이다. 
  - 참고로 if문은 비교 연산자를 사용할 수 있지만, switch문은 단순히 값이 같은지만 비교할 수 있다.
  - switch문은 조건식에 해당하는 특정 값으로 실행할 코드를 선택한다.
    ```java
    switch (조건식) {
      case value1:
        // 조건식의 결과 값이 value1일 때 실행되는 코드
        break;
      case value2:
        // 조건식의 결과 값이 value2일 때 실행되는 코드
        break;
      default:
        // 조건식의 결과 값이 위의 어떤 값에도 해당하지 않을 때 실행되는 코드
    }
    ```
    - 조건식의 결과 값이 어떤 case의 값과 일치하면 해당 case의 코드를 실행한다.
    - break문은 현재 실행 중인 코드를 끝내고 switch문을 빠져나가게 하는 역할을 한다.
    - 만약, break문이 없으면, 일치하는 case 이후의 모든 case 코드들이 순서대로 실행된다.
    - default는 조건식의 결과 값이 모든 case의 값과 일치하지 않을 때 실행된다. if문의 else와 같다.
    - default문은 필수가 아니다.
  - 예시
    ```java
    public class Switch1 {
        public static void main(String[] args) {
            int grade = 2;
            int coupon;
            switch (grade) {
                case 1:
                    coupon = 1000;
                    break;
                case 2:
                    coupon = 2000;
                    break;
                case 3:
                    coupon = 3000;
                    break;
                default:
                    coupon = 500;
            }
            System.out.println("발급받은 쿠폰 " + coupon);
        }
    }
    ```

8. **if문 vs switch문**
  - switch문의 조건식은 단순히 값만 넣을 수 있다.
  - switch문은 조건식이 특정 case와 같은 지만 체크할 수 있다. 쉽게 이야기해서 값이 같은지 확인하는 연산만 가능하다.(문자도 가능)
  - 반면, if문은 참, 거짓의 결과가 나오는 조건식을 자유롭게 적을 수 있다.
  - 정리하자면 switch문 없이 if문만 사용해도 된다. 하지만 특정 값에 따라 코드를 실행할 때는 switch문을 사용하면 if문보다 간결한 코드를 작성할 수 있다.

9. **새로운 switch문**
  - switch문은 if문보다 조금 덜 복잡한 것 같지만, 그래도 코드가 기대보다 깔끔하게 나오지 않는다.
  - 이런 문제를 해결하고자 자바14부터는 새로운 switch문이 정식 도입되었다.
  - 기존 코드를 새로운 switch문으로 개발하면 다음과 같다.
    ```java
    public class Switch2 {
        public static void main(String[] args) {
            int grade = 2;
            int coupon = switch (grade) {
                case 1 -> 1000;
                case 2 -> 2000;
                case 3 -> 3000;
                default -> 500;
            };
            System.out.println("발급받은 쿠폰 " + coupon);
        }
    }
    ```
    - 기존 switch문과 차이는 다음과 같다.
      - ->를 사용한다.
      - 선택된 데이터를 반환할 수 있다.

10. **삼항 연산자**
  - if문을 사용할 때 단순히 참과 거짓에 따라 특정 값을 구하는 경우가 있다.
  - 단순히 참과 거짓에 따라서 특정 값을 구하는 경우 삼항 연산자라고 불리는 ? : 연산자를 사용할 수 있다.
  - 이 연산자를 사용하면 if문과 비교해서 코드를 단순화할 수 있다.
  - (조건) ? 참_표현식 : 거짓_표현식
    - 삼항 연산자는 항이 3개라는 뜻이다. 조건, 참_표현식, 거짓_표현식 이렇게 항이 3개이다. 자바에서 유일하게 항이 3개인 연산자여서 삼항 연산자라고 한다. 또는 특정 조건에 따라 결과가 나오기 때문에 조건 연산자라고도 한다.
    - 조건에 만족하면 참_표현식이 실행되고, 조건에 만족하지 않으면 거짓_표현식이 실행된다. 앞의 if, else 문과 유사하다.
    - if문처럼 코드 블럭을 넣을 수 있는 것이 아니라 단순한 표현식만 넣을 수 있다.
  - 삼항 연산자 없이 if문만 사용해도 된다. 하지만 단순히 참과 거짓에 따라서 특정 값을 구하는 삼항 연산자를 사용하면 if문보다 간결한 코드를 작성할 수 있다.
  - 예시
    ```java
    public class CondOp1 {
        public static void main(String[] args) {
            int age = 18;
            String status = (age >= 18) ? "성인" : "미성년자";
            System.out.println("age = " + age + " status = " + status);
        }
    }
    ```




