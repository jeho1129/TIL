# <center>TIL<center>

# 객체 지향 프로그래밍 :memo:

1. **절차 지향 프로그래밍**
    - 프로그래밍 방식은 크게 절차 지향 프로그래밍과 객체 지향 프로그래밍으로 나눌 수 있다.
    - 절차 지향 프로그래밍
        - 절차 지향 프로그래밍은 이름 그대로 절차를 지향한다. 즉, 실행 순서를 중요하게 생각하는 방식이다.
        - 절차 지향 프로그래밍은 프로그램의 흐름을 순차적으로 따르며 처리하는 방식이다. 즉, 어떻게를 중심으로 프로그래밍한다.
    - 객체 지향 프로그래밍
        - 객체 지향 프로그래밍은 이름 그대로 객체를 지향한다. 즉, 객체를 중요하게 생각하는 방식이다.
        - 객체 지향 프로그래밍은 실제 세계의 사물이나 사건을 객체로 보고, 객체들 간의 상호작용을 중심으로 프로그래밍하는 방식이다. 즉, 무엇을 중심으로 프로그래밍한다.
    - 차이점
        - 절차 지향은 데이터와 해당 데이터에 대한 처리 방식이 분리되어 있다. 반면 객체 지향에서는 데이터와 해당 데이터에 대한 행동이 하나의 객체 안에 포함되어 있다.
    - 예시
        ```java
        public class MusicPlayerMain1 {

            public static void main(String[] args) {
                int volume = 0;
                boolean isOn = false;

                // 음악 플레이어 켜기
                isOn = true;
                System.out.println("음악 플레이어를 시작합니다.");
                // 볼륨 증가
                volume++;
                System.out.println(volume);
                // 볼륨 감소
                volume--;
                System.out.println(volume);
                // 음악 플레이어 상태
                System.out.println("음악 플레이어 상태 확인");
                if (isOn) {
                    System.out.println("음악 플레이어 ON, 볼륨 : " + volume);
                } else {
                    System.out.println("음악 플레이어 OFF");
                }
                // 음악 플레이어 끄기
                isOn = false;
                System.out.println("음악 플레이어를 종료합니다.");
            }
        }
        ```
    - 데이터 묶음
        - MusicPlayerData라는 클래스를 만들고, 음악 플레이어에 사용되는 데이터들을 묶어서 멤버 변수로 사용하기
        ```java
        public class MusicPlayerMain2 {

            public static void main(String[] args) {
                MusicPlayerData data = new MusicPlayerData();
                // 음악 플레이어 켜기
                data.isOn = true;
                System.out.println("음악 플레이어를 시작합니다.");
                // 볼륨 증가
                data.volume++;
                System.out.println(data.volume);
                // 볼륨 감소
                data.volume--;
                System.out.println(data.volume);
                // 음악 플레이어 상태
                System.out.println("음악 플레이어 상태 확인");
                if (data.isOn) {
                    System.out.println("음악 플레이어 ON, 볼륨 : " + data.volume);
                } else {
                    System.out.println("음악 플레이어 OFF");
                }
                // 음악 플레이어 끄기
                data.isOn = false;
                System.out.println("음악 플레이어를 종료합니다.");
            }
        }
        ```
        - 음악 플레이어와 관련된 데이터는 MusicPlayerData 클래스에 존재한다. 이제 이 클래스를 사용하도록 기존 로직을 변경했기에 프로그램 로직이 더 복잡해져서 다양한 변수들이 추가되더라도 음악 플레이어와 관련된 변수들은 MusicPlayerData data 객체에 속해있으므로 쉽게 구분할 수 있다.
    - 메서드 추출
        - 메서드를 사용해서 각각의 기능을 구분할 수 있다.
        ```java
        public class MusicPlayerMain2 {

            public static void main(String[] args) {
                MusicPlayerData data = new MusicPlayerData();
                // 음악 플레이어 켜기
                on(data);
                // 볼륨 증가
                volumeUp(data);
                // 볼륨 감소
                volumeDown(data);
                // 음악 플레이어 상태
                showStatus(data);
                // 음악 플레이어 끄기
                off(data);
            }

            static void on(MusicPlayerData data) {
                data.isOn = true;
                System.out.println("음악 플레이어를 시작합니다.");
            }

            static void off(MusicPlayerData data) {
                data.isOn = false;
                System.out.println("음악 플레이어를 종료합니다.");
            }

            static void volumeUp(MusicPlayerData data) {
                data.volume++;
                System.out.println(data.volume);
            }

            static void volumeDown(MusicPlayerData data) {
                data.volume--;
                System.out.println(data.volume);
            }

            static void showStatus(MusicPlayerData data) {
                System.out.println("음악 플레이어 상태 확인");
                if (data.isOn) {
                    System.out.println("음악 플레이어 ON, 볼륨 : " + data.volume);
                } else {
                    System.out.println("음악 플레이어 OFF");
                }
            }
        }
        ```
        - 각각의 기능을 메서드로 만든 덕분에 각각의 기능이 모듈화되었다.
            - 중복 제거 : 로직 중복이 제거되었다. 같은 로직이 필요하면 해당 메서드를 여러 번 호출하면 된다.
            - 변경 영향 범위 : 기능을 수정할 때 해당 메서드 내부만 변경하면 된다.
            - 메서드 이름 추가 : 메서드 이름을 통해 코드를 더 쉽게 이해할 수 있다.
        - 모듈화 : 레고 블럭과 같은 느낌이다. 필요한 블럭을 가져가서 사용할 수 있다. 음악 플레이어의 기능이 필요하면 해당 기능을 메서드 호출만으로 손쉽게 사용할 수 있다.
    - 절차 지향 프로그래밍의 한계
        - 지금까지 작성한 코드의 한계는 바로 데이터와 기능이 분리되어 있다는 점이다. 음악 플레이어의 데이터는 MusicPlayerData에 있는데, 그 데이터를 사용하는 기능은 각각 메서드에 분리되어있다.
        - 데이터와 그 데이터를 사용하는 기능은 매우 밀접하게 연관되어있다. 각각의 메서드를 보면 대부분 MusicPlayerData의 데이터를 사용한다. 따라서 이후에 관련 데이터가 변경되면 메서드들도 함께 변경해야한다. 그리고 데이터와 기능이 분리되어 있으면 유지보수 관점에서도 관리 포인트가 2곳으로 늘어난다.
        - 객체 지향 프로그래밍이 나오기 전까지는 지금과 같이 데이터와 기능이 분리되어 있었다. 하지만 객체 지향 프로그래밍이 나오면서 데이터와 기능을 하나로 묶어서 사용할 수 있게 되었다.

2. **클래스와 메서드**
    ```java
    public class ValueDataMain {

        public static void main(String[] args) {
            ValueData valueData = new ValueData();
            add(valueData);
            add(valueData);
            add(valueData);
            System.out.println("최종 숫자 = " + valueData.value);
        }

        static void add(ValueData valueData) {
            valueData.value++;
            System.out.println(valueData.value);
        }
    }
    ```
    - ValueData라는 인스턴스를 생성하고 외부에서 ValueData.value에 접근해 숫자를 하나씩 증가시키는 단순한 코드이다. 코드를 보면 데이터인 value와 value의 값을 증가시키는 기능인 add() 메서드가 서로 분리되어 있다.
    - 자바 같은 객체 지향 언어는 클래스 내부에 속성(데이터)과 기능(메서드)을 함께 포함할 수 있다. 클래스 내부에 멤버 변수 뿐만 아니라 메서드도 함께 포함할 수 있다는 뜻이다.
    ```java
    public class ValueData {
        int value;
        
        void add() {
            value++;
            System.out.println(value);
        }
    }
    ```
    - 이 클래스에는 데이터인 value와 해당 데이터를 사용하는 기능인 add() 메서드를 함께 정의했다.
    - 여기서 만드는 add() 메서드에는 static 키워드를 사용하지 않는다.
        - 메서드는 객체를 생성해야 호출할 수 있다. 그런데 static이 붙으면 객체를 생성하지 않고도 메서드를 호출할 수 있다.
    - 예시
        ```java
        public class ValueObjectMain {
            public static void main(String[] args) {
                ValueData valueData = new ValueData();
                valueData.add();
                valueData.add();
                valueData.add();
                System.out.println("최종 숫자 = " + valueData.value);
            }
        }
        ```
        - 인스턴스의 메서드를 호출하는 방법은 멤버 변수를 사용하는 방법과 동일하다. .(dot)을 통해 객체 접근한 다음에 원하는 메서드를 호출하면 된다.
        - add() 메서드를 호출하면 메서드 내부에서 value++을 호출하게 된다. 이 때 value에 접근해야 하는데, 기본으로 본인 인스턴스에 있는 멤버 변수에 접근한다.
    - 클래스는 속성(데이터, 멤버 변수)과 기능(메서드)을 정의할 수 있다.
    - 객체는 자신의 메서드를 통해 자신의 멤버 변수에 접근할 수 있다.
        - 객체의 메서드 내부에서 접근하는 멤버 변수는 객체 자신의 멤버 변수이다.

3. **객체 지향 프로그래밍**
    ```java
    public class MusicPlayer {

        int volume = 0;
        boolean isOn = false;

        void on() {
            isOn = true;
            System.out.println("음악 플레이어를 시작합니다.");
        }

        void off() {
            isOn = false;
            System.out.println("음악 플레이어를 종료합니다.");
        }

        void volumeUp() {
            volume++;
            System.out.println(volume);
        }

        void volumeDown() {
            volume--;
            System.out.println(volume);
        }

        void showStatus() {
            System.out.println("음악 플레이어 상태 확인");
            if (isOn) {
                System.out.println("음악 플레이어 ON, 볼륨 : " + volume);
            } else {
                System.out.println("음악 플레이어 OFF");
            }
        }
    }
    ```
    ```java
    public class MusicPlayerMain4 {
        public static void main(String[] args) {
            MusicPlayer player = new MusicPlayer();
            // 음악 플레이어 켜기
            player.on();
            // 볼륨 증가
            player.volumeUp();
            // 볼륨 감소
            player.volumeDown();
            // 음악 플레이어 상태
            player.showStatus();
            // 음악 플레이어 끄기
            player.off();
        }
    }
    ```
    - MusicPlayer를 사용하는 입장에서는 MusicPlayer의 데이터인 volume, isOn 같은 데이터는 전혀 사용하지 않는다.
    - MusicPlayer를 사용하는 입장에서는 이제 MusicPlayer 내부에 어떤 속성(데이터)이 있는지 전혀 몰라도 된다. 단순하게 MusicPlayer가 제공하는 기능 중에 필요한 기능을 호출해서 사용하기만 하면 된다.
    - 캡슐화
        - MusicPlayer를 보면 음악 플레이어를 구성하기 위한 속성과 기능이 마치 하나의 캡슐에 쌓여있는 것 같다. 이렇게 속성과 기능을 하나로 묶어서 필요한 기능을 메서드를 통해 외부에 제공하는 것을 캡슐화라 한다.
    - 객체 지향 프로그래밍 덕분에 음악 플레이어 객체를 사용하는 입장에서 진짜 음악 플레이어를 만들고 사용하는 것처럼 친숙하게 느껴진다. 그래서 코드가 더 읽기 쉬운 것은 물론이고, 속성과 기능이 한 곳에 있기 때문에 변경도 더 쉬워진다. 예를 들어서 MusicPlayer 내부 코드가 변하는 경우에 다른 코드는 변경하지 않아도 된다. MusicPlayer의 필드 이름이 다른 이름으로 변한다고 할 때 MusicPlayer 내부만 변경하면 된다.
    - 또 음악 플레이어가 내부에서 출력하는 메세지를 변경할 때도 MusicPlayer 내부만 변경하면 된다. 이 경우 MusicPlayer를 사용하는 개발자는 코드를 전혀 변경하지 않아도 된다. 물론 외부에서 호출하는 MusicPlayer의 메서드 이름을 변경한다면 MusicPlayer를 사용하는 곳의 코드도 변경해야 한다. 