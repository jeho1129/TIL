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
