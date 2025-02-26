# 아이템 15 : 클래스와 멤버 접근권한 최소화하기

## 캡슐화(정보 은닉)

**API를 통해서만 다른 컴포넌트와 소통**하며 서로의 내부 동작 방식에 영향을 받지 않는 개념

→ 모든 내부 구현화 데이터 정보를 외부로부터 완벽히 숨겨, **구현과 API를 깔끔하게 분리하는 것**을 목적으로 한다.

### 캡슐화의 장점

1. 컴포넌트를 병렬로 개발 가능하기 때문에 시스템 개발 속도가 높아진다.
2. 시스템 관리 비용을 낮춘다.
    
    : 각 컴포넌트를 더 빨리 파악하여 디버깅할 수 있고, 다른 컴포넌트를 교체하는 부담도 적기 때문
    
3. 정보 은닉 자체가 성능을 높여주지는 않지만, 성능 최적화에 도움을 준다.
4. 외부에 의존하지 않고 독자적으로 동작할 수 있는 컴포넌트이기 때문에, 소프트웨어 재사용성을 높인다.
5. 큰 시스템을 제작하는 난이도를 낮춰준다.
    
    : 시스템 전체가 아직 완성되지 않은 상태에서도 컴포넌트의 동작을 검증할 수 있기 때문
    

## 접근 제어 메커니즘 - 접근 제한자

요소의 접근성은 그 요소가 선언된 위치 + 접근 제한자로 정해진다.

→ 모든 클래스와 멤버의 접근성을 가능한 한 좁혀야 한다.

### 톱 레벨 클래스와 인터페이스 접근자

**public, package-private**가 접근제어자로 사용된다.

- public : 공개 API가 되며, 하위 호환을 위해 관리가 필요하다.
- package-private : 해당 패키지 안에서만 이용할 수 있으며, 클라이언트에 피해 없이 다음 릴리스에서 수정, 교체, 제거가 가능하다.

### 클래스 내에서의 활용

만약 한 클래스에서만 사용하는 `package-private` 톱 레벨 클래스나 인터페이스는, 사용하는 클래스 안에 `private static`으로 중첩시키면 바깥 클래스 하나에서만 접근 할 수 있게 된다.

```java
// AS-IS
public class A{
    private int a;
}
public class B{ // B가 A에서만 쓰이는 클래스라면?
    private int b;
}
```

```java
// TO-DO
public class A{
    private int a;
    
    private static class B{
        private int b;
    }
}
```

### 멤버 접근자

필드, 메서드, 중첩 클래스, 중첩 인터페이스에서는 public, protected, package-private, private가 접근제어자로 사용된다.

1. `private` : 멤버를 선언한 톱레벨 클래스에서만 접근 가능
2. `package-private` : 멤버가 소속된 패키지 안의 모든 클래스에서 접근 가능. 접근 제한자를 명시하지 않았을때 기본 접근 수준
3. `protected` : pakage-private의 접근 범위를 포함하며, 이 멤버를 선언한 클래스의 하위 클래스에도 접근 가능
4. `public` : 모든 곳에서 접근 가능

### 직렬화에서의 주의사항

`package-private` 와 `private` 멤버는 클래스의 구현에 해당하므로 공개 API에 영향을 주지 않지만, `Serializable` 을 구현한 클래스에서는 필드들로 의도치 않게 공개 API가 될 수 있으니 주의하자. `Serializable` 역직렬화 과정에서 `private` 필드가 노출되기 때문이다.

## 모듈 시스템에서의 접근 제한자

모듈에 적용되는 암묵적 접근 수준은 `public`, `protected` 수준과 같으나 그 효과가 **모듈 내부로 한정**된다는 점만 다르다. 

이 접근 수준을 활용한 예로 `JDK`가 있으며, 자바 라이브러리에서 공개하지 않은 패키지들은 해당 모듈 밖에서 절대 접근 할 수 없다.

> 💡 **모듈(Module)** <br>
패키지들의 묶음을 말하며 자신에 속하는 패키지 중 공개(export)할 것들을 `module-info.java` 파일에 선언한다. <br>
→ 모듈 시스템을 활용하면 클래스를 외부에 공개하지 않으면서도 **같은 모듈을 이루는 패키지 사이에서는 자유롭게 공유가 가능**하다는 장점이 있다.


### 멤버 접근성 좁히기 방해 제약

상위 클래스의 메서드를 재정의할 때는, 리스코프 치환 원칙으로 인해 그 접근 수준을 상위클래스에서보다 좁게 설정할 수 없다.


> 💡 **리스코프 치환 원칙** <br>
상위 클래스의 인스턴스는 하위 클래스의 인스턴스로 대체해 사용할 수 있어야 한다. <br>
→ 부모 클래스의 행동 규약을 자식 클래스가 위반하면 안된다.(다형성)



## 접근 제어자 주의사항

public클래스 안의 인스턴스 필드는 되도록 public이 아니어야 한다.

- 필드가 가변 객체를 참조하거나, final이 아닌 인스턴스 필드를 공개하면 **불변식을 보장할 수 없게 되기 때문이다.**
- 필드가 수정될 때 다른 작업 수행이 불가능하므로 public 가변 필드를 갖는 클래스는 **스레드 안전하지 않다.**

### 해결 방법

1. 상수라면 public static final필드로 공개한다.
2. 배열
    - private로 변경 후 public 불변 리스트를 추가한다.
    - 배열을 private로 만든 후 그 복사본을 반환하는 public 메서드를 추가한다.

https://velog.io/@semi-cloud/Effective-Java-%EC%95%84%EC%9D%B4%ED%85%9C-15-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%99%80-%EB%A9%A4%EB%B2%84%EC%9D%98-%EC%A0%91%EA%B7%BC-%EA%B6%8C%ED%95%9C%EC%9D%84-%EC%B5%9C%EC%86%8C%ED%99%94%ED%95%98%EB%9D%BC