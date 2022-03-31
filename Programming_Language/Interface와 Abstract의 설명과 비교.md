 
# Abstract vs Interface

## 1. Abstract(추상 클래스)란?

- **개념**
    
    자바에서 **하나 이상의 추상 메소드를 포함하는 클래스**를 추상 클래스라고 한다. 
    
- **특징**
    1. **인스턴스를 생성할 수 없다.** 
        - 상속을 통해 자식 클래스를 만들고, 모든 추상 메소드를 **오버라이딩** 해야 인스턴스를 생성할 수 있다.
    2. **추상 메소드 뿐만 아니라 생성자, 필드, 일반 메소드도 포함**할 수 있다.
    3. final과는 반대의 개념으로 두가지를 동시에 사용할 수 없다.
    4. 추상클래스 내에서 추상메서드를 호출할 수 있다. 호출할 때는 선언부만 필요하기 때문이다.
    5. 상속받는 클래스는 추상 클래스의 메서드 또는 변수가 있음을 보장한다.
    6. non-static, non-final 변수를 사용할 수 있어 객체의 상태를 수정할 수 있다.
    7. **“extends”** 사용하여 상속받음
    
- **사용목적**
    
    추상 메소드가 포함된 클래스를 상속받는 **자식 클래스가 반드시 추상 메소드를 구현하도록 하기 위함(틀로써의 역할)**이다. 일반 메소드로 구현한다면 사용자에 따라 해당 메소드를 구현할 수도, 안할 수도 있다. 하지만 추상 메소드가 포함된 클래스를 상속받은 모든 자식 클래스는 추상 메소드를 구현해야만 인스턴스를 생성할 수 있으므로 반드시 구현하게 된다.
    

- **How?** 어떻게 쓰나?
    
    ```java
    // 선언
    public abstract class Person{
    public abstract void eat();  // 추상 메서드
    public void work(){	         // 일반 메서드
       // some code here 
    }
    }
    
    // 상속
    public class Student extends Person{
    public void eat(){           // 오버라이딩
       
    }
    }
    ```
    

---

## 2. Interface(인터페이스)란?

- 개념
    
    다른 클래스를 작성할 때 **기본이 되는 틀**을 제공하면서, 다른 클래스 사이의 중간 매개 역할까지 담당하는 일종의 추상 클래스를 의미한다. 추상 메서드의 집합으로, 구현된 것이 전혀 없는 설계도라고 볼 수 있다.
    
- 특징
    1. **다중상속이 가능하다.**
        
        `**다중상속` 이란?**
        
        - 간단하게 말해 상속받는 부모가 2개 이상이면 다중상속이다. 자바의 일반 클래스는 부모 클래스를 단 하나만 가져야 하므로 여러 부모 클래스를 갖는 다중 상속을 지원하지 않는다. 그러나 **인터페이스는 추상 클래스보다 더 추상적이므로 여러 인터페이스를 상속받는 다중 상속을 지원**한다.
        - **다중상속 예제**
            
            ```java
            interface Animal {
                void cry();
            }
            interface Pet {
                void play();
            }
            class Cat implements Animal,Pet{
                @Override
                public void cry() {
                    System.out.println("냐옹");
                }
                @Override
                public void play() {
                    System.out.println("쥐잡기");
                }
            }
            class Dog implements Animal,Pet{
                @Override
                public void cry() {
                    System.out.println("멍멍");
                }
                @Override
                public void play() {
                    System.out.println("산책하기");
                }
            }
             
            호출 및 결과
            Cat c = new Cat();
            Dog d = new Dog();
            c.cry(); // 냐옹
            c.play(); // 쥐잡기
            d.cry(); // 멍멍
            d.play(); // 산책하기
            ```
            
    2. **오로지 추상 메소드와 상수만을 포함할 수 있다.**
    3. 인터페이스의 조상은 인터페이스만 가능!
    4. **“implements”** 사용하여 상속받음

- **How?** 어떻게 쓰나?
    
    ```java
    // 선언
    public interface Person{
    public static final String name = "홍길동";    // 변수 선언 (public, static, final 생략해도 자동)
    public void eat();                           // 메서드 선언
    }
    // 사용
    public class Student implements Person{
    public void study(){            // 메서드 선언
       // some code here 
    }
    public void eat(){              // 오버라이딩
       // some code here 
    }
    
    }
    ```
    

### +인터페이스를 이용한 다형성

- 인터페이스도 구현클래스의 부모 클래스가 된다.
- 인터페이스 타입 매개변수는 인터페이스를 구현한 클래스의 객체만 가능하다.
- 인터페이스를 메서드의 리턴타입으로 지정할 수 있다.

---

## 3. Abstract와 Interface의 공통점

1. **추상 메소드를 가지고 있다. (미완성 설계도)**
2. **상속을 이용하여 구현 가능하다.**
3. **자식 클래스에서 추상 메서드를 완성하도록 유도한다.**

---

## 4. Abstract와 Interface의 차이점

1. **추상클래스는 인스턴스 변수 및 메서드, 생성자를 가질 수 있지만, 인터페이스는 추상메서드만 가질 수 있다.**
2. **모두 추상메서드를 사용할 수 있지만, 사용용도가 다르다.**
    1. 사용용도가 다르다는 의미는 아래 그림 참고
    
    ![Untitled](Abstract%20v%2096d3d/Untitled.png)
