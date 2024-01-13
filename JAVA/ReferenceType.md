# <center>TIL<center>

# 참조형 :memo:

1. **기본형 vs 참조형**
    - 변수의 데이터 타입을 가장 크게 보면 기본형과 참조형으로 분류할 수 있다. 사용하는 값을 변수에 직접 넣을 수 있는 기본형, 객체가 저장된 메모리의 위치를 가르키는 참조값을 넣을 수 있는 참조형으로 분류할 수 있다.
    - 기본형(Primitive Type) : int, long, double, boolean처럼 변수에 사용할 값을 직접 넣을 수 있는 데이터 타입을 기본형이라 한다.
    - 참조형(Reference Type) : Student student1, int[] students와 같이 데이터에 접근하기 위한 참조(주소)를 저장하는 데이터 타입을 참조형이라 한다. 참조형은 객체 또는 배열에 사용된다.
    - 즉, 기본형 변수에는 직접 사용할 수 있는 값이 들어있지만 참조형 변수에는 위치(참조값)가 들어가 있다. 참조형 변수를 통해 뭔가 하려면 결국 참조값을 통해 해당 위치로 이동해야 한다.
        - 객체는 .(dot)을 통해서 메모리 상에 생성된 객체를 찾아가야 사용할 수 있다.
        - 배열은 []를 통해서 메모리 상에 생성된 배열을 찾아가야 사용할 수 있다.
    - 기본형은 소문자로 시작한다. 또한 기본형을 제외한 나머지는 모두 참조형이다.
    - 기본형은 자바가 기본으로 제공하는 데이터 타입이다. 개발자가 새로 정의할 수 없고, 개발자는 참조형인 클래스만 직접 정의할 수 있다.
    - 자바에서 String은 특별하다. String은 사실 클래스라 참조형이다. 하지만 기본형처럼 문자 값을 바로 대입할 수 있다. 문자는 매우 자주 다루기 때문에 자바에서 특별하게 편의 기능을 제공한다.

2. **기본형 vs 참조형 - 변수 대입**
    - 대원칙 : 자바는 항상 변수의 값을 복사해서 대입한다.
    - 기본형, 참조형 모두 항상 변수에 있는 값을 복사해서 대입한다. 기본형이면 변수에 들어있는 실제 사용하는 값을 복사해서 대입하고, 참조형이면 변수에 들어있는 참조값을 복사해서 대입한다.
    - 즉, 참조형을 복사할 경우 원본 참조형의 변수가 변경될 경우, 복사한 참조형은 원본 참조형의 주소를 참조하기 때문에 복사한 참조형의 변수도 변경된다.
    - 하지만, 기본형은 원본 변수가 변경되어도 복사한 변수는 변경되지 않는다.

3. **기본형 vs 참조형 - 메서드 호출**
    - 메서드 호출도 변수 대입과 마찬가지이다. 메서드를 호출할 때 사용하는 매개변수도 결국 변수일 뿐이다. 따라서 메서드를 호출할 때 매개변수에 값을 전달하는 것도 앞서 설명한 내용과 같이 값을 복사해서 전달한다.
    - 기본형 예시
        ```java
        public class MethodChange1 {
            public static void main(String[] args) {
                int a = 10;
                System.out.println("메서드 호출 전 : a = " + a);  // a = 10
                changePrimitive(a);
                System.out.println("메서드 호출 후 : a = " + a);  // a = 10
            }

            static void changePrimitive(int x) {
                x = 20;
            }
        }
        ```
        - 메서드 안에서 x = 20으로 새로운 값을 대입한다. 결과적으로 x의 값만 20으로 변경되고, a의 값은 10으로 유지된다.
        - 메서드가 종료되면 매개변수 x는 제거된다.
    - 참조형 예시
        ```java
        public class MethodChange2 {

            public static void main(String[] args) {
                Data dataA = new Data();
                dataA.value = 10;
                System.out.println("메서드 호출 전 : " + dataA.value);  // 10
                changeReference(dataA);
                System.out.println("메서드 호출 후 : " + dataA.value);  // 20
            }

            static void changeReference(Data dataX) {
                dataX.value = 20;
            }
        }
        ```
        - dataA, dataX 둘 다 같은 참조값을 가지게 되므로, dataX를 통해서도 Data 인스턴스에 접근할 수 있다.
        - dataX.value를 변경하면 dataA, dataX 모두 같은 인스턴스를 참조하기 때문에 dataA.value도 변경된다.
    - 기본형과 참조형의 메서드 호출
        - 기본형 : 메서드로 기본형 데이터를 전달하면 해당 값이 복사되어 전달된다. 이 경우, 메서드 내부에서 매개변수의 값을 변경해도 호출자의 변수 값에는 영향이 없다.
        - 참조형 : 메서드로 참조형 데이터를 전달하면 참조값이 복사되어 전달된다. 이 경우, 메서드 내부에서 매개변수로 전달된 객체의 멤버 변수를 변경하면, 호출자의 객체도 변경된다.

4. **참조형과 메서드 호출**
    ```java
    public class Method1 {
        public static void main(String[] args) {
            Student student1 = createStudent("학생1", 15, 90);
            Student student2 = createStudent("학생2", 16, 80);
            printStudent(student1);
            printStudent(student2);
        }

        static void createStudent(String name, int age, int grade) {
            Student student = new Student();
            student.name = name;
            student.age = age;
            student.grade = grade;
            return student;
        }

        static void printStudent(Student student) {
            System.out.println("이름 : " + student.name + "나이 : " + student.age + "등급 : " + student.grade);
        }
    }
    ```
    - createStudent()라는 메서드를 만들고 객체를 생성하는 부분도 이 메서드 안에 함께 포함하여 객체의 생성과 초기값 설정을 모두 처리할 수 있다.
    - 메서드 안에서 객체를 생성했기 때문에 만들어진 객체를 메서드 밖에서 사용할 수 있게 반환해야 하므로 return을 통해서 호출 결과를 반환한다. 메서드의 반환 기능을 사용해서 만들어진 객체의 참조값을 메서드 밖으로 반환하면 된다.

5. **변수와 초기화**
    - 변수의 종류
        - 멤버 변수(필드) : 클래스에 선언
        - 지역 변수 : 메서드에 선언, 매개변수도 지역 변수의 한 종류이다.
    - 변수의 값 초기화
        - 멤버 변수 : 자동 초기화
            - 인스턴스의 멤버 변수는 인스턴스를 생성할 때 자동으로 초기화된다.
            - int = 0, boolean = false, 참조형 = null
            - 개발자가 직접 초기값을 지정할 수 있다.
        - 지역 변수 : 수동 초기화
            - 지역 변수는 항상 직접 초기화해야 한다.

6. **null**
    - 참조형 변수에서 아직 가리키는 대상이 없다면 null이라는 특별한 값을 넣어둘 수 있다. null은 값이 존재하지 않는, 없다는 뜻이다.

7. **NullPointerException**
    - NullPointerException은 이름 그대로 주소가 없는 곳을 찾아갈 때 발생하는 예외이다.
    - 객체를 참조할 때는 .(dot)을 사용한다. 이렇게 하면 참조값을 사용해서 해당 객체를 찾아갈 수 있다. 그런데 참조값이 null이라면 값이 없다는 뜻이므로 찾아갈 수 있는 객체(인스턴스)가 없다.
    - 예시
        ```java
        public class NullMain {
            public static void main(String[] args) {
                Data data = null;
                data.value = 10;  // NullPointerException 예외 발생
                System.out.println(data.value);
            }
        }
        ```
        - 예외가 발생한 다음 로직은 수행되지 않는다.
    - 예시 2
        ```java
        public class NullMain2 {
            public static void main(String[] args) {
                BigData bigData = new BigData();
                System.out.println(bigData.count);  // 0
                System.out.println(bigData.data);   // null
                System.out.println(bigData.data.value); // nullPointerException
            }
        }
        ```
        - BigData를 생성하면 BigData의 인스턴스가 생성된다. 이 때 BigData 인스턴스의 멤버 변수에 초기화가 일어나는데, BigData의 data 멤버 변수는 참조형이므로 null로 초기화된다. count 멤버 변수는 숫자이므로 0으로 초기화된다.
        - 이 문제를 해결하려면 Data 인스턴스를 만들고 BigData.data 멤버 변수에 참조값을 할당하면 된다.