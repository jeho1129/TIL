# <center>TIL<center>

# Hello JAVA :memo:

1. **Java 기본**
  - 자바 언어는 대소문자를 구분한다. 대소문자가 다르면 오류가 발생할 수 있다.
  - 코드 분석
    ```java
    public class Hellojava {

        public static void main(String[] args) {
            System.out.println("hello java");
        }
    }
    ```
    - public class Hellojava
      - Hellojava를 클래스라 한다.
      - 지금은 단순히 Hellojava.java라는 파일을 만들었다고 이해하면 된다.
      - 파일명과 클래스 이름이 같아야 한다.
      - {} 블록을 사용해서 클래스의 시작과 끝을 나타낸다.
    - public static void main(String[] args)
      - main 메서드라 한다.
      - 자바는 main 메서드를 찾아서 프로그램을 시작한다.
      - 지금은 단순히 main은 프로그램의 시작점이라고 이해하면 된다.
      - {} 블록을 사용해서 메서드의 시작과 끝을 나타낸다.
    - System.out.println("hello java");
      - System.out.println() : 값을 콘솔에 출력하는 기능이다.
      - "hello java" : 자바는 문자열을 사용할 때 ""를 사용한다. 쌍따옴표 사이에 원하는 문자열을 감싸면 된다.
      - ; : 자바는 세미콜론으로 문장을 구분한다. 문장이 끝나면 세미콜론을 필수로 넣어줘야 한다.
    - 코드 실행 과정
      1. Hellojava 프로그램을 실행한다.
      2. 자바는 시작점인 main() 메서드를 실행한다.
      3. System.out.println("hello java")를 만나고, 문자열 hello java를 출력한다.
      4. main() 메서드의 {} 블록이 끝나면 프로그램이 종료된다.
  - 코드 블록
    - 블록({})이 시작되고 끝날 때마다 들여쓰기가 적용되어 있는 것을 확인할 수 있따. 이것은 코드를 쉽게 구분하고 이해하도록 도와주는 좋은 관례이다. 블록이 중첩될 때마다 들여쓰기의 깊이가 추가된다.
    - 들여쓰기는 보통 스페이스 4번을 사용한다. 참고로 IntelliJ IDE를 사용하면 탭을 한번 누르면 자동으로 들여쓰기가 적용된다.
    - 참고로 들여쓰기를 하지 않아도 프로그램은 작동하지만, 코드를 읽기에 좋지 않다.
  - 코드 실행 순서 : 프로그램은 main()을 시작으로 위에서 아래로 한 줄씩 실행된다.
  - IntelliJ 단축키
    - public static void main(String[] args) : psvm
    - System.out.println() : sout

2. **주석**
  - 소스 코드가 복잡하다면 소스 코드에 대한 이해를 돕기 위해 설명을 적어두고 싶을 수 있다.
  - 또는 특정 코드를 지우지 않고, 잠시 실행을 막아두고 싶을 때도 있다.
  - 이럴 때 주석을 사용하면 된다. 자바는 주석이 있는 곳을 무시한다.
  - 주석의 종류
    - 한 줄 주석 : //
    - 여러 줄 주석 : /* */
  - 예시
    ```java
    public class CommentJava {
        /*
        주석을 설명하는 부분입니다.
        */
        public static void main(String[] args) {
            System.out.println("hello java1"); //hello java1을 출력합니다. (한 줄 주석 - 부분 적용)
            //System.out.println("hello java2"); 한 줄 주석 - 라인 전체 적용
            /* 여러 줄 주석
            System.out.println("hello java3");
            System.out.println("hello java4");
            */
        }
    }
    ```

3. **자바란?**
  - 자바는 표준 스펙과 구현으로 나눌 수 있다.
  - 자바 표준 스펙
    - 예시
      - 자바 컴파일러 - 스펙
      - 자바 실행 라이브러리 - 스펙
      - 자바 가상 머신(JVM) - 스펙
    - 자바는 이렇게 만들어야 한다는 설계도이며, 문서이다.
    - 이 표준 스펙을 기반으로 여러 회사에서 실제 작동하는 자바를 만든다.
    - 자바 표준 스펙은 자바 커뮤니티 프로세스(JCP)를 통해 관리된다.
  - 자바 구현
    - 예시
      - 오라클 Open JDK
      - Adoptium Eclipse Temurin
      - Amazon Corretto
    - 여러 회사에서 자바 표준 스펙에 맞추어 실제 작동하는 자바 프로그램을 개발한다.
    - 각각 장단점이 있다. 예를 들어 Amazon Corretto는 AWS에 최적화되어 있다.
    - 각 회사들은 대부분 윈도우, Mac, Linux 같이 다양한 OS에서 작동하는 버전의 자바도 함께 제공된다.
    - 자바 구현들은 모두 표준 스펙에 맞도록 개발되어 있따. 따라서 오라클 Open JDK를 사용하다가 Amazon Corretto 자바로 변경해도 대부분 문제 없이 작동한다.
  - 컴파일과 실행
    - 자바 프로그램은 컴파일과 실행 단계를 거친다.
    - Hello.java와 같은 자바 소스 코드를 개발자가 작성한다.
    - 자바 컴파일러를 사용해서 소스 코드를 컴파일한다.
      - 자바가 제공하는 javac라는 프로그램을 사용한다.
      - .java -> .class 파일이 생성된다.
      - 자바 소스 코드를 바이트코드로 변환하며 자바 가상 머신에서 더 빠르게 실행될 수 있게 최적화하고 문법 오류도 검출한다.
    - 자바 프로그램을 실행한다.
      - 자바가 제공하는 java라는 프로그램을 사용한다.
      - 자바 가상 머신(JVM)이 실행되면서 프로그램이 작동한다.
  - IDE와 Java
    - 인테리제이를 통한 자바 설치 관리
      - 인텔리제이는 내부에 자바를 편리하게 설치하고 관리할 수 있는 기능을 제공한다.
      - 이 기능을 사용하면 인텔리제이를 통해 자바를 편리하게 다운로드 받고 실행할 수 있다.
    - 인텔리제이를 통한 자바 컴파일, 실행 과정
      - 컴파일
        - 자바 코드를 컴파일하려면 javac라는 프로그램을 직접 사용해야 하는데, 인텔리제이는 자바 코드를 실행할 때 이 과정을 자동으로 처리해준다.
        - 인텔리제이 화면에서 프로젝트에 있는 out 폴더에 가보면 컴파일된 .class 파일이 있는 것을 확인할 수 있다.
      - 실행
        - 자바를 실행하려면 java라는 프로그램을 사용해야 한다. 이 때 컴파일된 .class 파일을 지정해주면 된다
        - 확장자는 제외
      - 인텔리제이에서 자바 코드를 실행하면 컴파일과 실행 모두 한 번에 처리한다.
      - 인텔리제이 덕분에 매우 편리하게 자바 프로그램을 개발하고 학습할 수 있다.

4. **자바와 운영체제 독립성**
  - 일반적인 프로그램은 다른 운영체제에서 실행할 수 없다.
  - 자바 프로그램은 자바가 설치된 모든 OS에서 실행할 수 있다.
  - 자바 개발자는 특정 OS에 맞추어 개발을 하지 않아도 된다. 자바 개발자는 자바에 맞추어 개발하면 된다. OS 호환성 문제는 자바가 해결한다.
  - 개발할 때 자바와 서버에서 실행할 때 다른 자바를 사용할 수 있다.
  - 개발자들은 개발의 편의를 위해 윈도우나 Mac OS를 주로 사용한다.
  - 서버는 주로 리눅스를 사용한다. 만약 AWS를 사용한다면, Amazon Corretto 자바를 AWS 리눅스 서버에 설치하면 된다.
  - 자바의 운영체제 독립성 덕분에 각각의 환경에 맞추어 자바를 설치하는 것이 가능하다.
