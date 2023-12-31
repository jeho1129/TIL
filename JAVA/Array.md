# <center>TIL<center>

# 배열 :memo:

1. **배열의 선언과 생성**
  - 배열은 같은 타입의 변수를 사용하기 편하게 하나로 묶어둔 것이다.
  - 예시
    ```java
    public class Array1 {
        public static void main(String[] args) {
            int[] students; // 배열 변수 선언
            students = new int[5];  // 배열 생성

            // 변수 값 대입
            students[0] = 90;
            students[1] = 80;
            students[2] = 70;
            students[3] = 60;
            students[4] = 50;

            // 변수 값 사용
            System.out.println(students[0]);
            System.out.println(students[1]);
            System.out.println(students[2]);
            System.out.println(students[3]);
            System.out.println(students[4]);
        }
    }
    ```
    1. 배열 변수 선언
      - 배열을 사용하려면 int[] students;와 같이 배열 변수를 선언해야 한다.
      - 일반적인 변수와 차이점은 int[]처럼 타입 다음에 대괄호([])가 들어간다는 점이다.
      - 배열 변수를 선언한다고 해서 아직 사용할 수 있는 배열이 만들어진 것은 아니다.
      - int[] students와 같은 배열 변수에는 배열을 담을 수 있다.(배열 변수에는 10, 20과 같은 값이 아니라 배열을 담을 수 있다.)
    2. 배열 생성
      - 배열을 사용하려면 배열을 생성해야 한다.
      - new int[5]라고 입력하면 총 5개의 int형 변수가 만들어진다.
      - new는 새로 생성한다는 뜻이고, int[5]는 int형 변수 5개라는 뜻이다. 따라서 int형 변수 5개를 다룰 수 있는 배열을 새로 만든다는 뜻이다.
      - 자바는 배열을 생성할 때 그 내부 값을 자동으로 초기화한다.
      - 숫자는 0, boolean은 false, String은 null로 초기화된다.
    3. 배열 참조값 보관
      - new int[5]로 배열을 생성하면 배열의 크기만큼 메모리를 확보한다.
        - int형을 5개 사용하면 4byte * 5 = 20byte를 확보한다.
      - 배열을 생성하고 나면 자바는 메모리 어딘가에 있는 이 배열에 접근할 수 있는 참조값(주소)을 반환한다.
      - 앞서 선언한 배열 변수인 int[] students에 생성된 배열의 참조값을 보관한다.
      - int[] students 변수는 new int[5]로 생성한 배열의 참조값을 가지고 있다.
        - 이 변수는 참조값을 가지고 있다. 이 참조값을 통해 배열을 참조할 수 있다. 참조값을 통해 메모리에 있는 실제 배열에 접근하고 사용할 수 있다.
        - 배열을 생성하는 new int[5] 자체에는 아무런 이름이 없다. 그냥 int형 변수를 5개 연속으로 만드는 것이다. 따라서 생성한 배열에 접근하는 방법이 필요하다. 따라서 배열을 생성할 때 반환되는 참조값을 어딘가에 보관해두어야 한다.
  
2. **배열 사용**
  - 배열은 변수와 사용법이 비슷한데, 차이점이 있다면 [] 사이에 숫자 번호를 넣어주면 된다. 배열의 위치를 나타내는 숫자를 인덱스(index)라 한다.
  - new int[5]와 같이 5개의 요소를 가지는 int형 배열을 만들었다면 인덱스는 0 ~ 4가 존재한다.
  - 배열에 값을 대입하든 배열의 값을 사용하든 간에 일반적인 변수와 사용법은 같다. []를 통해 인덱스만 넣어주면 된다.

3. **기본형 vs 참조형**
  - 자바의 변수 데이터 타입을 가장 크게 보면 기본형과 참조형으로 분류할 수 있다. 사용하는 값을 직접 넣을 수 있는 기본형, 그리고 배열 변수와 같이 메모리의 참조값을 넣을 수 있는 참조형으로 분류할 수 있다.
  - 기본형(Primitive Type) : int, long, double, boolean처럼 변수에 사용할 값을 직접 넣을 수 있는 데이터 타입을 기본형이라 한다.
  - 참조형(Reference Type) : int[] students와 같이 데이터에 접근하기 위한 참조(주소)를 저장하는 데이터 타입을 참조형이라 한다. 객체와 클래스를 담을 수 있는 변수들도 모두 참조형이다.
  - 기본형은 선언과 동시에 크기가 정해진다. 따라서 크기를 동적으로 바꾸거나 할 수는 없다. 반면 배열과 같은 참조형은 크기를 동적으로 할당할 수 있다. 예를 들어 Scanner를 사용해서 사용자 입력에 따라 size 변수의 값이 변하고, 생성되는 배열의 크기도 달라질 수 있다. 이런 것을 동적 메모리 할당이라 한다. 기본형은 선언과 동시에 사이즈가 정적으로 정해지지만, 참조형을 사용하면 이처럼 동적으로 크기가 변해서 유연성을 제공할 수 있다.
  - 기본형은 사용할 값을 직접 저장한다. 반면 참조형은 메모리에 저장된 배열이나 객체의 참조를 저장한다. 이로 인해 참조형은 더 복잡한 데이터 구조를 만들고 관리할 수 있다. 반면 기본형은 더 빠르고 메모리를 효율적으로 처리한다.

4. **배열 리팩토링**
  - 리팩토링(Refactoring)은 기존 코드 기능은 유지하면서 내부 구조를 개선하여 가독성을 높이고, 유지보수를 용이하게 하는 과정을 뜻한다. 이는 중복을 제거하고, 복잡성을 줄이며 이해하기 쉬운 코드로 만들기 위해 수행된다. 리팩토링은 버그를 줄이고, 프로그램의 성능을 향상시킬 수도 있으며, 코드의 설계를 개선하는 데에도 도움이 된다.
  - 예시
    ```java
    public class Array2 {
        public static void main(String[] args) {
            int[] students; // 배열 변수 선언
            students = new int[5];  // 배열 생성

            // 변수 값 대입
            students[0] = 90;
            students[1] = 80;
            students[2] = 70;
            students[3] = 60;
            students[4] = 50;

            // 변수 값 사용
            for (int i = 0; i < students.length; i++) {
                System.out.println(students[i]);
            }
        }
    }
    ```
    - 반복문을 사용해서 배열을 통해 값을 사용하는 부분을 효과적으로 변경했다.
    - 배열의 인덱스는 0부터 시작하기 때문에 반복문에서 i = 0을 초기값으로 사용했다.
    - students.length
      - 배열의 길이를 제공하는 특별한 기능이다.
      - 이 값은 조회만 할 수 있다. 대입은 할 수 없다.
    - for문의 조건이 i < students.length이기 때문에 i가 5가 되면 반복을 종료한다.
  - 배열은 {}를 사용해서 생성과 동시에 편리하게 초기화하는 기능을 제공한다.
    ```java
    int[] students = new int[]{90, 80, 70, 60, 50}; // 배열 변수 선언, 배열 생성과 초기화
    int[] students = {90, 80, 70, 60, 50};  // 배열 변수의 선언을 한 줄에 함께 사용할 때만 가능
    ```

5. **2차원 배열**
  - 2차원 배열은 행과 열로 구성된다.
  - 2차원 배열은 int[][] arr = new int[2][3]과 같이 선언하고 생성한다. 그리고 arr[row][column]와 같이 사용하는데, 먼저 행 번호를 찾고, 그 다음에 열 번호를 찾으면 된다.
  - 2차원 배열의 사용법은 []가 하나 추가되는 것을 제외하고는 1차원 배열과 같다.
  - 예시
    ```java
    public class Array3 {
        public static void main(String[] args) {
            int[][] arr = new int[2][3];

            arr[0][0] = 1;
            arr[0][1] = 2;
            arr[0][2] = 3;
            arr[1][0] = 4;
            arr[1][1] = 5;
            arr[1][2] = 6;

            System.out.print(arr[0][0]);
            System.out.print(arr[0][1]);
            System.out.println(arr[0][2]);
            System.out.print(arr[1][0]);
            System.out.print(arr[1][1]);
            System.out.println(arr[1][2]);
        }
    }
    ```

6. **2차원 배열 리팩토링**
  - 구조 개선(행 출력 반복)
    ```java
    public class Array4 {
        public static void main(String[] args) {
            int[][] arr = new int[2][3];

            arr[0][0] = 1;
            arr[0][1] = 2;
            arr[0][2] = 3;
            arr[1][0] = 4;
            arr[1][1] = 5;
            arr[1][2] = 6;

            for (int row = 0; row < 2; row++) {
                System.out.print(arr[row][0]);
                System.out.print(arr[row][1]);
                System.out.print(arr[row][2]);
                System.out.println();
            }
        }
    }
    ```
    - for문을 통해 행(row)을 반복해서 접근한다. 각 행 안에서 열이 3개이므로 for문을 한번 도는 동안 3개의 열을 출력할 수 있다.
  - 구조 개선(열 출력 반복)
    ```java
    public class Array5 {
        public static void main(String[] args) {
            int[][] arr = new int[2][3];

            arr[0][0] = 1;
            arr[0][1] = 2;
            arr[0][2] = 3;
            arr[1][0] = 4;
            arr[1][1] = 5;
            arr[1][2] = 6;

            for (int row = 0; row < 2; row++) {
                for (int column = 0; column < 3; column++) {
                    System.out.print(arr[row][column]);
                }
                System.out.println();
            }
        }
    }
    ```
    - for문을 2번 중첩해서 사용하는데, 첫 번째 for문은 행을 탐색하고, 내부에 있는 두 번째 for문은 열을 탐색한다.
  - 구조 개선(초기화, 배열의 길이)
    - 이전 코드에서는 2가지 개선할 부분이 존재한다.
      1. 초기화 : 기존 배열처럼 2차원 배열도 편리하게 초기화할 수 있다.
      2. for문에서 배열의 길이 활용 : 배열의 길이가 달라지면 for문에서 조건문을 다시 변경해야 한다. 이 부분을 배열의 길이를 사용하도록 변경하면 배열이 커지거나 줄어들어도 for문의 코드를 변경하지 않고 그대로 유지할 수 있다.
    ```java
    public class Array6 {
        public static void main(String[] args) {
            int[][] arr = new int[][]{
                    {1, 2, 3},
                    {4, 5, 6}
            };

            for (int row = 0; row < arr.length; row++) {
                for (int column = 0; column < arr[row].length; column++) {
                    System.out.print(arr[row][column]);
                }
                System.out.println();
            }
        }
    }
    ```
    - 초기화
      - 1차원 배열은 다음과 같이 초기화를 한다.
        - {1, 2, 3}
      - 2차원 배열은 다음과 같이 초기화를 한다. 밖이 행이 되고, 안이 열이 된다.
        - {{1, 2, 3}, {4, 5, 6}}
        - 이렇게 라인을 적절하게 넘겨주면 행과 열이 명확해져 코드를 더 쉽게 이해할 수 있다.
        - {
            {1, 2, 3},
            {4, 5, 6}
          }
    - 배열의 길이
      - arr.length는 행의 길이를 뜻한다.
      - arr[row].length는 열의 길이를 뜻한다.
  - 구조 개선(값 입력)
    ```java
    public class Array7 {
        public static void main(String[] args) {
            int[][] arr = new int[2][3];

            int i = 1;
            for (int row = 0; row < arr.length; row++) {
                for (int column = 0; column < arr[row].length; column++) {
                    arr[row][column] = i++;
                }
            }

            for (int row = 0; row < arr.length; row++) {
                for (int column = 0; column < arr[row].length; column++) {
                    System.out.print(arr[row][column]);
                }
                System.out.println();
            }
        }
    }
    ```
    - 중첩된 for문을 사용해서 값을 순서대로 입력한다.
    - arr[row][column] = i++ 후위 증감 연산자를 사용해서 값을 먼저 대입한 다음에 증가한다.
    
7. **향상된 for문**
  - 향상된 for문(Enhanced For Loop)은 각각의 요소를 탐색한다는 의미로 for-each문이라고도 많이 부른다.
  - 향상된 for문은 배열을 사용할 때 기존 for문보다 더 편리하게 사용할 수 있다.
  - 향상된 for문 정의
    ```java
    for (변수 : 배열 또는 컬렉션) {
      // 배열 또는 컬렉션의 요소를 순회하면서 수행할 작업
    }
    ```
  - 예시
    ```java
    public class Array8 {
        public static void main(String[] args) {
            int[] numbers = {1, 2, 3, 4, 5};

            // 일반 for문
            for (int i = 0; i < numbers.length; i++) {
                int number = numbers[i];
                System.out.println(number);
            }

            // 향상된 for문(for-each문)
            for (int number : numbers) {
                System.out.println(number);
            }
        }
    }
    ```
    - 일반 for문
      - 배열에 있는 값을 순서대로 읽어서 number 변수에 넣고 출력한다.
      - 배열은 처음부터 끝까지 순서대로 읽어서 사용하는 경우가 많다. 그런데 배열의 값을 읽으려면 int i와 같은 인덱스를 탐색할 수 있는 변수를 선언해야한다. 그리고 i < numbers.length와 같이 배열의 끝 조건을 지정해줘야한다. 마지막으로 배열의 값을 하나 읽을 때마다 인덱스를 하나씩 증가해야한다.
    - 향상된 for문
      - 향상된 for문은 배열의 인덱스를 사용하지 않고, 종료 조건을 지정하지 않아도 된다. 단순히 해당 배열을 처음부터 끝까지 탐색한다.
      - :의 오른쪽에 number와 같이 탐색할 배열을 선택하고, :의 왼쪽에 int number와 같이 반복할 때마다 찾은 값을 지정할 변수를 선언한다. 그러면 배열의 값을 하나씩 꺼내서 왼쪽에 있는 number에 담고 for문을 수행한다. for문의 끝에 가면 다음 값을 꺼내서 number에 담고 for문을 반복 수행한다. 배열의 끝에 도달해서 더 값이 없으면 for문이 완전히 종료된다.
      - 향상된 for문은 배열의 인덱스를 사용하지 않고도 배열의 요소를 순회할 수 있기 때문에 코드가 간결하고 가독성이 좋다.
  - 향상된 for문을 사용하지 못하는 경우
    - 향상된 for문에는 증가하는 인덱스 값이 감춰져있다. 따라서 인덱스 값을 직접 사용해야 하는 경우에는 향상된 for문을 사용할 수 없다.
