# <center>TIL<center>

# 생성자 :memo:

1. **생성자**
    - 객체를 생성하는 시점에 어떤 작업을 하고 싶다면 생성자(Construct)를 이용하면 된다.
    ```java
    public class MemberConstruct {
        String name;
        int age;
        int grade;

        MemberConstruct(String name, int age, int grade) {
            this.name = name;
            this.age = age;
            this.grade = grade
        }
    }
    ```
    - 생성자는 메서드와 비슷하지만 다음과 같은 차이가 있다.
        - 생성자의 이름은 클래스 이름과 같아야 한다. 따라서 첫 글자도 대문자로 시작한다.
        - 생성자는 반환 타입이 없다. 비워두어야 한다.
    ```java
    public class ConstructMain1 {
        public static void main(String[] args) {
            MemberConstruct member1 = new MemberConstruct("user1", 15, 90);
            MemberConstruct member2 = new MemberConstruct("user2", 16, 80);
            MemberConstruct[] members = {member1, member2};
            for (MemberConstruct s : members) {
                System.out.println("이름:" + s.name + " 나이:" + s.age + " 성적:" + s.grade);
            }
        }
    }
    ```
    - 생성자는 인스턴스를 생성하고 나서 즉시 호출된다. 생성자를 호출하는 방법은 new 명령어 다음에 생성자 이름과 매개변수에 맞추어 인수를 전달하면 된다.
    - new 키워드를 사용해서 객체를 생성할 때 마지막에 괄호 ()도 포함해야 하는 이유가 바로 생성자 때문이다. 객체를 생성하면서 동시에 생성자를 호출한다는 의미를 포함한다.

2. **this**
    ```java
    public class MemberInit {
        String name;
        int age;
        int grade;

        void initMember(String name, int age, int grade) {
            this.name = name;
            this.age = age;
            this.grade = grade;
        }
    }
    ```
    - 메서드의 매개변수에 정의한 String name과 Member의 멤버 변수의 이름이 String name으로 둘 다 똑같다.
    - 이 경우 멤버 변수보다 매개변수가 코드 블럭의 더 안쪽에 있기 때문에 매개변수가 우선순위를 가진다. 따라서 initMember 메서드 안에서 name이라고 적으면 매개변수에 접근하게 된다.
    - 멤버 변수에 접근하려면 앞에 this라고 하면 된다. this는 인스턴스 자신의 참조값을 가리킨다.
    - this를 제거하면 name은 둘 다 매개변수를 뜻하게 되므로 멤버 변수의 값이 변경되지 않는다.
    ```java
    public class MethodInitMain1 {

        public static void main(String[] args) {
            MemberInit member1 = new MemberInit();
            member1.initMember("user1", 15, 90);

            MemberInit member2 = new MemberInit();
            member2.initMember("user2", 16, 80);

            MemberInit[] members = {member1, member2};

            for (MemberInit member : members) {
                System.out.println(member.name + member.age + member.grade);
            }
        }
    }
    ```
    - 매개변수의 이름과 멤버 변수의 이름이 같은 경우 this를 사용해서 둘을 명확하게 구분해야 한다.
    - this는 인스턴스 자신을 가리킨다.

3. **this의 생략**
    - this는 생략할 수 있다. 이 경우 변수를 찾을 때 가까운 지역변수(매개변수도 지역변수다)를 먼저 찾고 없으면 그 다음으로 멤버 변수를 찾는다. 멤버 변수도 없으면 오류가 발생한다.

4. **this와 코딩 스타일**
    - 멤버 변수에 접근하는 경우에 항상 this를 사용하는 코딩 스타일도 존재한다.
    - 이렇게 this를 사용하면 멤버 변수를 사용한다는 것을 눈으로 쉽게 확인할 수 있어 지역 변수(매개변수)와 멤버 변수를 눈에 보이도록 구분할 수 있다.
    - 하지만 최근에는 IDE가 발전하면서 IDE가 멤버 변수와 지역 변수를 색상으로 구분해준다.
    - 그로 인해 최근에는 this를 필요할 때만 쓰는 추세이다.

5. **생성자 장점**
    - 중복 호출 제거
        - 생성자가 없던 시절에는 생성 직후에 어떤 작업을 수행하기 위해 메서드를 직접 한 번 더 호출해야 했다. 생성자 덕분에 개체를 생성하면서 동시에 생성 직후에 필요한 작업을 한 번에 처리할 수 있게 되었다.
    - 제약 : 생성자 호출 필수
        - 메서드를 실수로 호출하지 않아도 프로그램은 작동한다. 하지만 회원의 이름, 나이, 성적 데이터가 없는 상태로 프로그램이 동작하게 된다. 만약에 이 값들을 필수로 반드시 입력해야 한다면, 시스템에 큰 문제가 발생할 수 있다. 결국 아무 정보가 없는 유령 회원이 시스템 내부에 등장하게 된다.
        - 생성자의 진짜 장점은 객체를 생성할 때 직접 정의한 생성자가 있다면 직접 정의한 생성자를 반드시 호출해야 한다는 점이다. 참고로 생성자를 메서드 오버로딩처럼 여러 개 정의할 수 있는데, 이 경우에는 하나만 호출하면 된다.
        - 직접 정의한 생성자를 호출하지 않으면 컴파일 오류가 발생한다. 컴파일 오류는 IDE에서 즉시 확인할 수 있는 좋은 오류이다. 이 경우, 개발자는 객체를 생성할 때 직접 정의한 생성자를 필수로 호출해야 한다는 것을 바로 알 수 있다.
        - 생성자 덕분에 회원의 이름, 나이, 성적은 항상 필수로 입력하게 된다. 따라서 아무 정보가 없는 유령 회원이 시스템 내부에 등장할 가능성을 완전 차단한다.
        - 따라서 생성자를 사용하면 필수값 입력을 보장할 수 있다.

6. **기본 생성자**
    - 매개변수가 없는 생성자를 기본 생성자라 한다.
    - 클래스에 생성자가 하나도 없으면 자바 컴파일러는 매개변수가 없고, 작동하는 코드가 없는 기본 생성자를 자동으로 만들어준다.
    - 생성자가 하나라도 있으면 자바는 기본 생성자를 만들지 않는다.
    ```java
    public class MemberDefault {
        String name;
        //기본 생성자
        public MemberDefault() {
        }
    }
    ```
    - 자바가 자동으로 생성해주는 기본 생성자는 클래스와 같은 접근 제어자를 가진다.
    - 만약 자바에서 기본 생성자를 만들어주지 않는다면 생성자 기능이 필요하지 않은 경우에도 모든 클래스에 개발자가 직접 기본 생성자를 정의해야 한다. 생성자 기능을 사용하지 않는 경우도 많기 때문에 이런 편의 기능을 제공한다.

7. **생성자 - 오버로딩과 this()**
    - 생성자도 메서드 오버로딩처럼 매개변수만 다르게 해서 여러 생성자를 제공할 수 있다.
    ```java
    public class MemberConstruct {
        String name;
        int age;
        int grade;
        
        // 추가
        MemberConstruct(String name, int age) {
            this.name = name;
            this.age = age;
            this.grade = 50;
        }

        MemberConstruct(String name, int age, int grade) {
            this.name = name;
            this.age = age;
            this.grade = grade;
        }
    }
    ```
    - 기존 MemberConstruct에 생성자를 하나 추가하여 생성자가 2개가 되었다.
    - 새로 추가한 생성자는 grade를 받지 않는 대신 50점이 된다.
    - 생성자를 오버로딩한 덕분에 성적 입력이 꼭 필요한 경우에는 grade가 있는 생성자를 호출하면 되고, 그렇지 않는 경우에는 grade가 없는 생성자를 호출하면 된다.

8. **this()**
    - 위 두 생성자를 비교할 때 코드가 중복되는 부분이 존재한다.
    - 이 때 this()라는 기능을 사용하면 생성자 내부에서 자신의 생성자를 호출할 수 있다. 참고로 this는 인스턴스 자신의 참조값을 가리킨다.
    ```java
    public class MemberConstruct {
        String name;
        int age;
        int grade;
        
        // 추가
        MemberConstruct(String name, int age) {
            this(name, age, 50);  // 변경
        }

        MemberConstruct(String name, int age, int grade) {
            this.name = name;
            this.age = age;
            this.grade = grade;
        }
    }
    ```
    - 이 코드는 첫 번째 생성자 내부에서 두 번째 생성자를 호출한다.
    - this()를 사용하면 생성자 내부에서 다른 생성자를 호출할 수 있다. 이 부분을 잘 활용하면 지금과 같이 중복을 제거할 수 있다.
    - this() 규칙
        - this()는 생성자 코드의 첫 줄에만 작성할 수 있다.
        - 그렇지 않을 경우 컴파일 오류가 발생한다.