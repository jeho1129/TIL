# <center>TIL<center>

# 반복문 :memo:

1. **반복문**
  - 반복문은 이름 그대로 특정 코드를 반복해서 실행할 때 사용된다.
  - 자바는 다음 3가지 종류의 반복문을 제공한다.
    - while
    - do-while
    - for

2. **while**
  - while문은 조건에 따라 코드를 반복해서 실행할 때 사용한다.
    ```java
    while (조건식) {
      // 코드
    }
    ```
    - 조건식을 확인한다. 참이면 코드 블럭을 실행하고, 거짓이면 while문을 벗어난다.
    - 조건식이 참이면 코드 블럭을 실행하고, 이후에 코드 블럭이 끝나면 다시 조건식 검사로 돌아가서 조건식을 검사한다.(무한 반복)
  - 예시
    ```java
    public class While1_1 {
        public static void main(String[] args) {
            int count = 0;
            while (count < 3) {
                count += 1;
                System.out.println(count);
            }
        }
    }
    ```

3. **do-while**
  - do-while문은 while문과 비슷하지만, 조건에 상관없이 무조건 한 번은 코드를 실행한다.
  - do-while문은 최초 한 번은 코드 블럭을 꼭 실행해야 하는 경우에 사용하면 된다.
    ```java
    do {
      // 코드
    } while (조건식);
    ```
  - 예시
    ```java
    public class DoWhile1 {
        public static void main(String[] args) {
            int i = 10;
            do {
                System.out.println(i);
                i++;
            } while (i < 3);
        }
    }
    ```
    - do-while문은 최초 한 번은 항상 실행된다. 따라서 10이 출력된다.
    - 코드 블럭을 실행 후에 조건식을 검증하는데, i = 10이기 때문에 while 조건식이 거짓이 된다. 따라서 do-while 문을 빠져나온다.

4. **break, continue**
  - break와 continue는 반복문에서 사용할 수 있는 키워드다.
  - break는 반복문을 즉시 종료하고 나간다.
  - continue는 반복문의 나머지 부분을 건너뛰고 다음 반복으로 진행하는데 사용된다.
  - 참고로 while, do-while, for와 같은 모든 반복문에서 사용할 수 있다.
    - ```java
      while (조건식) {
        // 코드1
        break; // 즉시 while문 종료
        // 코드2
      }
      ```
      - break를 만나면 코드2가 실행되지 않고 while문이 종료된다.
    - ```java
      while (조건식) {
        // 코드1
        continue; // 즉시 조건식으로 이동한다.
        // 코드2
      }
      ```
      - continue를 만나면 코드2가 실행되지 않고 다시 조건식으로 이동한다. 조건식이 참이면 while문을 실행한다.
  - break 예시
    ```java
    public class Break1 {
        public static void main(String[] args) {
            int sum = 0;
            int i = 1;

            while (true) {
                sum = sum + i;
                if (sum > 10) {
                    System.out.println(i);
                    System.out.println(sum);
                    break;
                }
                i++;
            }
        }
    }
    ```
  - continue 예시
    ```java
    public class Continue1 {
        public static void main(String[] args) {
            int i = 1;
            while (i <= 5) {
                if (i == 3) {
                    i++;
                    continue;
                }
                System.out.println(i);
                i++;
            }
        }
    }
    ```

5. **for**
  - for문도 while문과 같은 반복문이고, 코드를 반복 실행하는 역할을 한다.
  - for문은 주로 반복 횟수가 정해져 있을 때 사용한다.
    ```java
    for (1. 초기식; 2. 조건식; 4. 증감식) {
      // 3. 코드
    }
    ```
    - for문은 다음 순서대로 실행된다.
      1. 초기식이 실행된다. 주로 반복 횟수와 관련된 변수를 선언하고 초기화할 때 사용한다. 초기석은 1번만 사용된다.
      2. 조건식을 검증한다. 참이면 코드를 실행하고, 거짓이면 for문을 빠져나간다.
      3. 코드를 실행한다.
      4. 코드가 종료되면 증감식을 실행한다. 주로 초기식에 넣은 반복 횟수와 관련된 변수의 값을 증가할 때 사용한다.
      5. 다시 조건식부터 시작한다.
  - 예시
    ```java
    public class For1 {
        public static void main(String[] args) {
            for (int i = 1; i <= 10; i++) {
                System.out.println(i);
            }
        }
    }
    ```
  - for문은 초기화, 조건 검사, 반복 후 작업 등이 규칙적으로 한 줄에 모두 들어있어 코드를 이해하기 더 쉽다. 특히 반복을 위해 값이 증가하는 카운터 변수를 다른 부분과 명확하게 구분할 수 있다.
  - for문에서 초기식, 조건식, 증감식은 선택이다. 단, 생략해도 각 영역을 구분하는 세미콜론은 유지해야한다.
    ```java
    for (; ; ) {
      // 코드
    }
    ```
    - 이렇게 하면 조건이 없기 때문에 무한 반복하는 코드가 된다.
  - for문 없이 while문으로 모든 반복을 다룰 수 있지만, 카운터 변수가 명확하거나, 반복 횟수가 정해진 경우에는 for문을 사용하는 것이 구조적으로 더 깔끔하고, 유지보수하기 좋다.
