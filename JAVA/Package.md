# <center>TIL<center>

# 패키지 :memo:

1. **패키지**
    - 컴퓨터는 보통 파일을 분류하기 위해 폴더, 디렉토리라는 개념을 제공한다. 자바도 이런 개념을 제공하는데, 이것이 바로 패키지이다.
    - 패키지 안에 관련된 자바 클래스들을 넣는다.
    - 패키지 사용
        ```java
        package pack;

        public class Data {
            public Data() {
                System.out.println("패키지 pack Data 생성");
            }
        }
        ```
        - 패키지를 사용하는 경우 코드 첫 줄에 패키지 이름을 적어주어야 한다.
        - 패키지를 먼저 만들고, 그 이후에 클래스를 만든다.
        - 이후 Data 인스턴스가 생성되면 생성자를 통해 정보를 출력한다.
        - 생성자에 public을 사용했다. 다른 패키지에서 이 클래스의 생성자를 호출하려면 public을 사용해야 한다.
        ```java
        package pack;

        public class PackageMain1 {

            public static void main(String[] args) {
                Data data = new Data();
                pack.a.User user = new pack.a.User();
            }
        }
        ```
        - 사용자와 같은 위치 : PackageMain1과 같은 Data는 같은 pack이라는 패키지에 소속되어 있다. 이렇게 같은 패키지에 있는 경우에는 패키지 경로를 생략해도 된다.
        - 사용자와 다른 위치 : PackageMain1과 User는 서로 다른 패키지다. 이렇게 패키지가 다르면 pack.a.User와 같이 패키지 전체 경로를 포함해서 클래스를 적어주어야 한다.

2. **import**
    - 서로 다른 패키지일 경우 패키지 전체 경로를 적어주는 것이 불편하기에 import를 사용한다.
    ```java
    package pack;

    import pack.a.User;

    public class PackageMain2 {

        public static void main(String[] args) {
            Data data = new Data();
            User user = new User();  // import 사용으로 패키지 명 생략 가능
        }
    }
    ```
    - 코드 첫 줄에는 package를 사용하고, 다음 줄에는 import를 사용할 수 있다.
    - import를 사용하면 다른 패키지에 있는 클래스를 가져와서 사용할 수 있다.
    - import를 사용한 덕분에 코드에서는 패키지명을 생략하고 클래스 이름만 적을수 있다.
    - 특정 패키지에 포함된 모든 클래스를 포함해서 사용하고 싶으면 import 시점에 *을 사용하면 된다.(예 : import pack.a.*)
    - 클래스 이름 중복
        - 패키지 덕분에 클래스 이름이 같아도 패키지 이름으로 구분해서 같은 이름의 클래스를 사용할 수 있다.
        ```java
        package pack;

        import pack.a.User;

        public class PackageMain3 {

            public static void main(String[] args) {
                User userA = new User();
                pack.b.User userB = new pack.b.User();
            }
        }
        ```
        - 같은 이름의 클래스가 있다면 import는 둘 중 하나만 선택할 수 있다. 이 때는 자주 사용하는 클래스를 import하고 나머지를 패키지를 포함한 전체 경로를 적어주면 된다.

3. **패키지 규칙**
    - 패키지의 이름과 위치는 폴더(디렉토리) 위치와 같아야한다.
    - 패키지 이름은 모두 소문자를 사용한다. (관례)
    - 패키지 이름의 앞 부분에는 일반적으로 회사의 도메인 이름을 거꾸로 사용한다. 예를 들어, com.company.myapp과 같이 사용한다. (관례)
        - 이 부분은 필수는 아니다. 하지만 수 많은 외부 라이브러리가 함께 사용되면 같은 패키지에 같은 클래스 이름이 존재할 수도 있다. 이렇게 도메인 이름을 거꾸로 사용하면 이런 문제를 방지할 수 있다.
        - 오픈소스나 라이브러리를 만들어서 외부에 제공한다면 꼭 지키는 것이 좋다.
    - 계층 구조
        - a 패키지 하위에 b, c 패키지가 존재하여 총 a, a.b, a.c 3개의 패키지가 존재할 때 우리 눈에 보기에 계층 구조를 이루지만 사실, a 패키지와 a.b, a.c 패키지는 서로 완전히 다른 패키지이다.
        - 따라서 a 패키지의 클래스에서 a, b 패키지의 클래스가 필요하면 import해서 사용해야한다. 반대의 경우도 마찬가지이다.
        - 패키지가 계층 구조를 이루더라도 모든 패키지는 서로 다른 패키지이다.