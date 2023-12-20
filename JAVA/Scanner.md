# <center>TIL<center>

# Scanner :memo:

1. **Scanner**
  - System.out을 통해 출력을 했듯이, System.in을 통해 사용자의 입력을 받을 수 있다.
  - 그런데 자바가 제공하는 System.in을 통해 사용자 입력을 받기 위해서는 여러 과정을 거쳐야해서 복잡하고 어렵다.
  - 자바는 이런 문제를 해결하기 위해 Scanner라는 클래스를 제공한다. 이 클래스를 사용하면 사용자 입력을 매우 편리하게 받을 수 있다.
  - 예시 1
    ```java
    package scanner;

    import java.util.Scanner;

    public class Scanner1 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);
            System.out.print("문자열을 입력하세요 : ");
            String str = scanner.nextLine();    // 입력을 String으로 가져온다.
            System.out.println("입력한 문자열 : " + str);

            System.out.print("정수를 입력하세요 : ");
            int intValue = scanner.nextInt();   // 입력을 int로 가져온다.
            System.out.println("입력한 정수 : " + intValue);

            System.out.print("실수를 입력하세요 : ");
            double doubleValue = scanner.nextDouble();  // 입력을 double로 가져온다.
            System.out.println("입력한 실수 : " + doubleValue);
        }
    }
    ```
    - Scanner scanner = new Scanner(System.in);
      - 이 코드는 Scanner의 기능을 사용하기 위해 new를 사용해서 Scanner를 만든다. Scanner는 System.in을 사용해서 사용자의 입력을 편리하게 받도록 도와준다.
      - Scanner scanner 코드는 scanner 변수를 선언하는 것이다. 이제부터 scanner 변수를 통해서 scanner를 사용할 수 있다.
    - scanner.nextLine()
      - 엔터(\n)을 입력할 때까지 문자를 가져온다.
    - 타입이 다르면 오류가 발생한다.
    - print() : 출력하고 다음 라인으로 넘기지 않는다.
    - println() : 출력하고 다음 라인으로 넘긴다.
  - 예시 2
    ```java
    package scanner;

    import java.util.Scanner;

    public class Scanner2 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);

            System.out.print("첫 번째 숫자를 입력하세요 : ");
            int num1 = scanner.nextInt();
            
            System.out.print("두 번째 숫자를 입력하세요 : ");
            int num2 = scanner.nextInt();

            int sum = num1 + num2;
            System.out.println("두 숫자의 합 : " + sum);
        }
    }
    ```
  - 예시 3
    ```java
    package scanner;

    import java.util.Scanner;

    public class Scanner3 {
        public static void main(String[] args) {
            Scanner scanner = new Scanner(System.in);

            while (true) {
                System.out.print("문자열을 입력하세요(exit : 종료) : ");
                String str = scanner.nextLine();
                if (str.equals("exit")) {
                    System.out.println("프로그램을 종료합니다.");
                    break;
                }
                System.out.println("입력한 문자열 : " + str);
            }
        }
    }
    ```