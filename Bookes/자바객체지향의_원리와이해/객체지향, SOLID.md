## 객체지향의 4대 특성

- 캡슐화 :

  정보를 은닉하는 것 ( public, protected, default, private )
- 추상화

  구체적인 것을 분해해서 관심 영역에 대한 특성만을 가지고 모델링하여 클래스를 정의하는 것
- 상속화

  상속의 목적 = 재사용 + 확장
  상속은 **is a kind of** 관계를 만족해야 함 ( 팽귄성is a kind of 동물 )
- 다형성
의
  **Overiding 과 Overloading**

  Overiding : 상위 클래스와 같은 메소드의 이름, 같은 타입의 파라미터를 그대로 사용하면서 재정의

  Overloading : 상위 클래스의 메소드 이름만 도일하게 하되, 파라미터 타입과 개수를 다르게해서 중복 정의

<br>
<br>

## SOLID

### SRP (Single Responsibility Principle)

*추상화* 를 기반으로 하는 SRP는 하나의 객체가 하나의 역할만을 수행하도록 하는 원칙

### OCP (Open Closed Principle)

주변에 변화에는 닫혀있고 확장에는 열려있어야 한다.

### LSP (Liscov Subsitution Principle)

서브타입은 언제나 자신의 기반타입으로 교체할 수 있어야 한다.

-> 하위 클래스의 인스턴스는 상위 클래스의 인스턴스 역할을 수행할 수 있어야 한다.

### ISP (Interface Segregation Principle)

클라이언트측에서 사용하지 않는 메소드에 의존을 가지면 안된다.

SRP와 ISP는 같은 문제에 대한 해결책

### DIP (Dependency Inversion Principle)

추상화 된것은 구체화 된것에 의존하면 안된다. 구체화 된것이 추상화 된것에 의존해야 한다.

