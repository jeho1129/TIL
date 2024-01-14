# <center>TIL<center>

# 접근 제어자 :memo:

1. **접근 제어자**
    - 자바는 public, private 같은 접근 제어자(access modifier)를 제공한다. 접근 제어자를 사용하면 해당 클래스 외부에서 특정 필드나 메서드에 접근하는 것을 허용하거나 제한할 수 있다.
    ```java
    package access;

    public class Speaker {
        int volume;
        
        Speaker(int volume) {
            this.volume = volume;
        }
        
        void volumeUp() {
            if (volume >= 100) {
                System.out.println("음량을 증가할 수 없습니다. 최대 음량입니다.");
            } else {
                volume += 10;
                System.out.println("음량을 10 증가합니다.");
            }
        }
        
        void volumeDown() {
            volume -= 10;
            System.out.println("음량을 10 감소합니다.");
        }
        
        void showVolume() {
            System.out.println(volume);
        }
    }
    ```
    ```java
    package access;

    public class SpeakerMain {
        public static void main(String[] args) {
            Speaker speaker = new Speaker(90);
            speaker.showVolume();

            speaker.volumeUp();
            speaker.showVolume();
            
            speaker.volumeDown();
            speaker.showVolume();
        }
    }
    ```
    - Speaker 객체를 사용하는 사용자는 Speaker의 volume 필드와 메서드에 모두 접근할 수 있다.
    - volume 필드를 Speaker 클래스 외부에서는 접근하지 못하게 막기 위해서는 private 접근 제어자를 사용한다.
    ```java
    package access;

    public class Speaker {
        private int volume; // private 사용
    }
    ```
    - private 접근 제어자는 모든 외부 호출을 막는다. 따라서 private이 붙은 경우 해당 클래스 내부에서만 호출할 수 있다.
    - volume 필드는 이제 Speaker 내부에서만 접근할 수 있다.
    - 이제 Speaker 외부에서 volume 필드에 접근하면 컴파일 오류가 발생한다.

2. **접근 제어자 종류**
    - private : 모든 외부 호출을 막는다.
    - default(package-private) : 같은 패키지 안에서만 호출을 허용한다.
    - protected : 같은 패키지 안에서 호출을 허용한다 + 패키지가 달라도 상속 관계의 호출을 허용한다.
    - public : 모든 외부 호출을 허용한다.
    - 위에서 순서대로 private이 가장 많이 차단하고, public이 가장 많이 허용한다.
    - package-privatte
        - 접근 제어자를 명시하지 않으면 같은 패키지 안에서만 호출을 허용하는 default 접근 제어자가 적용된다.
        - default라는 용어는 해당 접근 제어자가 기본값으로 사용되기 때문에 붙여진 이름이지만, 실제로는 package-private이 더 정확한 표현이다. 해당 접근 제어자를 사용하는 멤버는 동일한 패키지 내의 다른 클래스에서만 접근이 가능하기 때문이다.
    - 접근 제어자 사용 위치
        - 접근 제어자는 필드, 메서드, 생성자에 사용된다.
        - 클래스 레벨에도 일부 접근 제어자를 사용할 수 있다.
    - 접근 제어자의 핵심은 속성과 기능을 외부로부터 숨기는 것이다.
        - private는 나의 클래스 안으로 속성과 기능을 숨길 때 사용, 외부 클래스에서 해당 기능을 호출할 수 없다.
        - default는 나의 패키지 안으로 속성과 기능을 숨길 때 사용, 외부 패키지에서 해당 기능을 호출할 수 없다.
        - protected는 상속 관계로 속성과 기능을 숨길 때 사용, 상속 관계가 아닌 곳에서 해당 기능을 호출할 수 없다.
        - public은 기능을 숨기지 않고 어디서든 호출할 수 있게 공개한다.

3. **접근 제어자 사용(필드, 메서드)**
    ```java
    package access.a;

    public class AccessData {

        public int publicField;
        int defaultField;
        private int privateField;

        public void publicMethod() {
            System.out.println(publicField);
        }

        void defaultMethod() {
            System.out.println(defaultField);
        }

        private void privateMethod() {
            System.out.println(privateField);
        }

        public void innerAccess() {
            publicField = 100;
            defaultField = 200;
            privateField = 300;
            publicMethod();
            defaultMethod();
            privateMethod();
        }
    }
    ```
    - 패키지 위치는 package access.a이다.
    - 순서대로 public, default, private을 필드와 메서드에 사용한다.
    - 마지막에 innerAccess()가 있는데, 이 메서드는 내부 호출을 보여준다. 내부 호출은 자기 자신에게 접근하는 것이다. 따라서 private을 포함한 모든 곳에 접근할 수 있다.
    ```java
    package access.a;

    public class AccessInnerMain {
        public static void main(String[] args) {
            AccessData data = new AccessData();
            // public 호출 가능
            data.publicField = 1;
            data.publicMethod();
            
            // default 호출 가능
            data.defaultField = 2;
            data.defaultMethod();
            
            // private 호출 불가
        }
    }
    ```
    - 패키지 위치는 package access.a이다.
    - public은 모든 접근을 허용하기 때문에 필드, 메서드 모두 접근 가능하다.
    - default는 같은 패키지에서 접근할 수 있다.
    - private는 호출이 불가하다.
    ```java
    package access.b;

    import access.a.AccessData;

    public class AccessOuterMain {
        public static void main(String[] args) {
            AccessData data = new AccessData();
            // public 호출 가능
            data.publicField = 1;
            data.publicMethod();

            // default 호출 불가

            // private 호출 불가
        }
    }
    ```
    - 패키지 위치는 package access.b이다.
    - public은 모든 접근을 허용하기 때문에 필드, 메서드 모두 접근할 수 있다.
    - 서로 다른 패키지이므로, default 접근 제어자에 접근할 수 없다.
    - private도 호출이 불가하다.

4. **접근 제어자 사용(클래스 레벨)**
    - 클래스 레벨의 접근 제어자는 public, default만 사용할 수 있다.(private, protected는 사용할 수 없다.)
    - public 클래스는 반드시 파일명과 이름이 같아야 한다.
        - 하나의 자바 파일에 public 클래스는 하나만 등장할 수 있다.
        - 하나의 자바 파일에 default 접근 제어자를 사용하는 클래스는 무한정 만들 수 있다.
    - 예시
        ```java
        package access.a;

        public class PublicClass {
            public static void main(String[] args) {
                PublicClass publicclass = new PublicClass();
                DefaultClass1 class1 = new DefaultClass1();
                DefaultClass2 class2 = new DefaultClass2();
            }
        }

        class DefaultClass1 {

        }

        class DefaultClass2 {

        }
        ```
        - 패키지 위치는 package access.a이다.
        - PublicClass라는 이름의 클래스를 만들었다. 이 클래스는 public 접근 제어자다. 따라서 파일명과 이 클래스의 이름이 반드시 같아야 한다. 이 클래스는 public이기 때문에 외부에서 접근할 수 있다.
        - DefaultClass1, DefaultClass2는 default 접근 제어자다. 이 클래스는 default이기 때문에 같은 패키지 내부에서만 접근할 수 있다.

5. **캡슐화**
    - 캡슐화(Encapsulation)는 객체 지향 프로그래밍의 중요한 개념 중 하나다. 캡슐화는 데이터와 해당 데이터를 처리하는 메서드를 하나로 묶어서 외부에서의 접근을 제한하는 것을 말한다. 캡슐화를 통해 데이터의 직접적인 변경을 방지하거나 제한할 수 있다.
    - 즉, 속성과 기능을 하나로 묶고, 외부에 꼭 필요한 기능만 노출하고 나머지는 모두 내부로 숨기는 것이다.
    1. 데이터 숨기기
        - 객체에는 속성(데이터)과 기능(메서드)이 있다. 캡슐화에서 가장 필수로 숨겨야 하는 것은 속성(데이터)이다.
        - 객체의 데이터는 객체가 제공하는 기능인 메서드를 통해서 접근해야 한다.
    2. 기능 숨기기
        - 객체의 기능 중에서 외부에서 사용하지 않고 내부에서만 사용하는 기능들이 있다. 이런 기능도 모두 감추는 것이 좋다.
        - 사용자 입장에서 꼭 필요한 기능만 외부에 노출한다.
    - 데이터는 모두 숨기고, 기능은 꼭 필요한 기능만 노출하는 것이 좋은 캡슐화이다.
    - 예시
        ```java
        package access.b;

        public class BankAccount {

            private int balance;

            public BankAccount() {
                balance = 0;
            }

            // public 메서드 : 입금
            public void deposit(int amount) {
                if (isAmountValid(amount)) {
                    balance += amount;
                } else {
                    System.out.println("유효하지 않은 금액입니다.");
                }
            }

            // public 메서드 : 출금
            public void withdraw(int amount) {
                if (isAmountValid(amount) && balance - amount >= 0) {
                    balance -= amount;
                } else {
                    System.out.println("유효하지 않은 금액이거나 잔액이 부족합니다.");
                }
            }

            // public 메서드 : 잔액 확인
            public int getBalance() {
                return balance;
            }

            private boolean isAmountValid(int amount) {
                // 금액이 0보다 커야한다.
                return amount > 0;
            }
        }
        ```
        - private
            - balance : 데이터 필드는 외부에 직접 노출하지 않는다. BankAccount가 제공하는 메서드를 통해서만 접근할 수 있다.
            - isAmountValid() : 입력 금액을 검증하는 기능은 내부에서만 필요한 기능이다. 따라서 private를 사용한다.
    - 접근 제어자와 캡슐화를 통해 데이터를 안전하게 보호하는 것은 물론이고, 개발자 입장에서 해당 기능을 사용하는 복잡도도 낮출 수 있다.