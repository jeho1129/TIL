# <center>TIL<center>

# 클래스 :memo:

1. **클래스가 필요한 이유**
    - 배열을 사용해서 데이터를 변경할 경우, 데이터를 변경할 때 각각 배열마다 변경하고자 하는 요소의 인덱스를 정확하게 찾아서 제거해야 하기에 유지보수적인 측면에서 매우 효율성이 떨어진다.

2. **클래스**
    ```java
    package class1;

    public class Student {
        String name;
        int age;
        int grade;
    }
    ```
    - class 키워드를 사용해서 학생 클래스를 정의한다.
    - 이렇게 클래스에 정의한 변수들을 멤버 변수, 또는 필드라 한다.
        - 멤버 변수(Member Variable) : 이 변수들은 특정 클래스에 소속된 멤버이기 때문에 이렇게 부른다.
        - 필드(Field) : 데이터 항목을 가르키는 전통적인 용어이다. DB, 엑셀 등에서 데이터 각각의 항목을 필드라 한다.
    - 클래스는 관례상 대문자로 시작하고 CamelCase를 사용한다.
        - Student, User, MemberService
    - 예시
        ```java
        public class ClassStart3 {

            public static void main(String[] args) {
                Student student1;
                student1 = new Student();
                student1.name = "학생1";
                student1.age = 15;
                student1.grade = 90;

                Student student2 = new Student();
                student2.name = "학생2";
                student2.age = 16;
                student2.grade = 80;

                System.out.println("이름 : " + student1.name + " 나이 : " + student1.age + " 성적 : " + student1.grade);
                System.out.println("이름 : " + student2.name + " 나이 : " + student2.age + " 성적 : " + student2.grade);
            }
        }
        ```
    - 클래스와 사용자 정의 타입
        - 타입은 데이터의 종류나 형태를 나타낸다.
        - int라고 하면 정수 타입, String이라고 하면 문자 타입이다.
        - 클래스를 사용하면 int, String과 같은 타입을 직접 만들 수 있다.
        - 사용자가 직접 정의하는 사용자 정의 타입을 만들려면 클래스가 필요하다.
        - 클래스를 사용해서 실제 메모리에 만들어진 실체를 객체 또는 인스턴스라 한다.
        - 클래스를 통해서 사용자가 원하는 종류의 데이터 타입을 정의할 수 있다.
    - 변수 선언
        - Student student1
        - Student 타입을 받을 수 있는 변수를 선언한다.
        - int는 정수를, String은 문자를 담을 수 있듯이 Student는 Student 타입의 객체(인스턴스)를 받을 수 있다.
    - 객체 생성
        - student1 = new Student()
        - 객체를 사용하려면 먼저 설계도인 클래스를 기반으로 객체를 생성해야 한다.
        - new Student() : new는 새로 생성한다는 뜻이다. new Student()는 Student 클래스 정보를 기반으로 새로운 객체를 생성하라는 뜻이다. 이렇게 하면 메모리에 실제 Student 객체를 생성한다.
        - 객체를 생성할 때는 new 클래스명()을 사용하면 된다. 마지막에 ()도 추가해야 한다.
        - Student 클래스는 String name, int age, int grade 멤버 변수를 가지고 있다. 이 변수를 사용하는 데 필요한 메모리 공간도 함께 확보한다.
    - 참조값 보관
        - 객체를 생성하면 자바는 메모리 어딘가에 있는 이 객체에 접근할 수 있는 참조값(주소)을 반환한다.
        - new 키워드를 통해 객체가 생성되고 나면 참조값을 반환한다. 앞서 선언한 변수인 Student student1에 생성된 객체의 참조값을 보관한다.
        - Student student1 변수는 이제 메모리에 존재하는 실제 Student 객체의 참조값을 가지고 있다.
        - student1 변수는 방금 만든 객체에 접근할 수 있는 참조값을 가지고 있다. 따라서 이 변수를 통해 객체를 접근(참조)할 수 있다. 쉽게 이야기해서 student1 변수를 통해 메모리에 있는 실제 객체를 접근하고 사용할 수 있다.
        - 이후에 student2까지 생성하면 다음과 같이 Student 객체가 메모리에 2개 생성된다. 각각 참조값이 다르므로 서로 구분할 수 있다.
    - 참조값을 변수에 보관해야 하는 이유
        - 객체를 생성하는 new Student() 코드 자체에는 아무런 이름이 없다. 이 코드는 단순히 Student 클래스를 기반으로 메모리에 실제 객체를 만드는 것이다. 따라서 생성한 객체에 접근할 수 있는 방법이 필요하다. 이런 이유로 객체를 생성할 때 반환되는 참조값을 어딘가에 보관해두어야 한다.

3. **객체 사용**
    - 클래스를 통해 생성한 객체를 사용하려면 먼저 메모리에 존재하는 객체에 접근해야 한다. 객체에 접근하려면 .(dot)을 사용하면 된다.(예 : student1.name)
    - 객체에 값 대입
        - 객체가 가지고 있는 멤버 변수(name, age, grade)에 값을 대입하려면 먼저 객체에 접근해야 한다. 객체에 접근하려면 .(dot) 키워드를 사용하면 된다.
    - 객체 값 읽기
        - 마찬가지로 .(dot) 키워드를 통해 참조값을 사용해서 객체에 접근한 다음 원하는 작업을 하면 된다.

4. **클래스, 객체, 인스턴스 정리**
    - Class
        - 클래스는 객체를 생성하기 위한 설계도이다. 클래스는 객체가 가져야 할 속성(변수)과 기능(메서드)를 정의한다. 예를 들어 학생이라는 클래스는 속성으로 name, age, grade를 가진다.
    - Object
        - 객체는 클래스에서 정의한 속성과 기능을 가진 실체이다. 객체는 서로 독립적인 상태를 가진다. 예를 들어 student1, student2는 같은 클래스에서 만들어졌지만 서로 다른 객체이다.
    - Instance
        - 인스턴스는 특정 클래스로부터 생성된 객체를 의미한다. 인스턴스는 주로 객체가 어떤 클래스에 속해 있는 지 강조할 때 사용한다. 예를 들어 student1 객체는 Student 클래스의 인스턴스라고 표현한다.
        - 인스턴스와 객체는 둘 다 클래스에서 나온 실체라는 의미에서 비슷하게 사용되지만, 용어 상 인스턴스는 객체보다 좀 더 관계에 초점을 맞춘 단어이다. 보통 student1은 Student의 객체이다라고 말하는 대신 student1은 Student의 인스턴스이다라고 특정 클래스와의 관계를 명확히 할 때 인스턴스라는 용어를 주로 사용한다.
        - 즉, 모든 인스턴스는 객체이지만 우리가 인스턴스라고 부르는 순간은 특정 클래스로부터 그 객체가 생성되었음을 강조하고 싶을 때이다. 예를 들어 student1 객체가 Student 클래스로부터 생성된다는 점을 명확히 하기 위해 student1을 Student의 인스턴스라고 부른다.

5. **배열 도입**
    - 배열을 사용하면 특정 타입을 연속한 데이터 구조로 묶어서 편리하게 관리할 수 있다. Student 클래스를 사용한 변수들도 Student 타입이기 때문에 배열을 사용해서 하나의 데이터 구조로 묶어서 관리할 수 있다.
    - 예시
        ```java
        public class ClassStart4 {

            public static void main(String[] args) {
                Student student1 = new Student();
                student1.name = "학생1";
                student1.age = 15;
                student1.grade = 90;

                Student student2 = new Student();
                student2.name = "학생2";
                student2.age = 16;
                student2.grade = 80;

                Student[] students = new Student[2];
                students[0] = student1;
                students[1] = student2;
                
                System.out.println("이름 : " + students[0].name + " 나이 : " + students[0].age + " 성적 : " + students[0].grade);
                System.out.println("이름 : " + students[1].name + " 나이 : " + students[1].age + " 성적 : " + students[1].grade);
            }
        }
        ```
        - 배열에 참조값 대입
            - Student 변수를 2개 보관할 수 있는 사이즈 2의 배열을 만든다.
            - Student 타입의 변수는 Student 인스턴스의 참조값을 보관한다. Student 배열의 각각의 항목도 Student 타입의 변수이다.
        - 배열에 들어있는 객체 사용
            - 배열에 들어있는 객체를 사용하려면 먼저 배열에 접근하고, 그 다음에 객체에 접근하면 된다.

6. **배열을 이용한 리팩토링**
    - 배열을 이용하여 for문을 사용해 코드를 효율적으로 관리할 수 있다.
    ```java
    public class ClassStart5 {

        public static void main(String[] args) {
            Student student1 = new Student();
            student1.name = "학생1";
            student1.age = 15;
            student1.grade = 90;

            Student student2 = new Student();
            student2.name = "학생2";
            student2.age = 16;
            student2.grade = 80;

            Student[] students = {student1, student2};

            for (Student s : students) {
                System.out.println("이름 : " + s.name + " 나이 : " + s.age + " 성적 : " + s.grade);
            }
        }
    }
    ```
    - 배열 선언 최적화
        - Student 타입도 일반적인 변수와 동일하게 배열을 생성할 때 포함할 수 있다.
            - Student[] students = new Student[]{student1, student2};
        - 생성과 선언을 동시에 하는 경우 다음과 같이 더 최적화할 수 있다.
            - Student[] students = {student1, student2};
    - for문 최적화
        ```java
        for (int i = 0; i < students.length; i++) {
            Student s = students[i];
            System.out.println("이름:" + s.name + " 나이:" + s.age + ...);
        }
        ```
        ```java
        for (Student s : students) {
            System.out.println("이름 : " + s.name + " 나이 : " + s.age + " 성적 : " + s.grade);
        }
        ```
        - 향상된 for문을 이용하는 것이 깔끔하다.