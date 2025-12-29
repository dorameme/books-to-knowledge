
## 1. 한 줄 정의

| 키워드        | 의미                     |
| ---------- | ---------------------- |
| extends    | **기능을 가진 상위 타입을 상속**한다 |
| implements | **기능 없는 규약을 구현**한다     |

---

## 2. 무엇을 대상으로 쓰는가

| 구분    | extends     | implements |
| ----- | ----------- | ---------- |
| 대상    | 클래스, 추상 클래스 | 인터페이스      |
| 구현 상속 | 가능하다        | 불가능하다      |
| 다중 상속 | 클래스는 불가     | 가능하다       |

---

## 3. 코드로 즉시 구별

### 3-1. extends 예시

```java
class Animal {
    void eat() {}
}

class Dog extends Animal {
}
```

* Animal은 구현을 가진다
* Dog는 그대로 물려받는다
* is-a 관계이다
  → Dog는 Animal이다

---

### 3-2. implements 예시

```java
interface Flyable {
    void fly();
}

class Bird implements Flyable {
    public void fly() {}
}
```

* Flyable은 규칙만 정의한다
* Bird가 실제 동작을 만든다
* can-do 관계이다
  → Bird는 날 수 있다

---

## 4. 가장 쉬운 구별 질문

> **“부모가 구현을 가지고 있는가?”**

| 답   | 사용         |
| --- | ---------- |
| 그렇다 | extends    |
| 아니다 | implements |

---

## 5. 다중 상속 차이

```java
class A {}
class B {}

// 불가능
class C extends A, B {}
```

```java
interface A {}
interface B {}

// 가능
class C implements A, B {}
```

---

## 6. 실무 설계 관점

| 관점    | extends | implements |
| ----- | ------- | ---------- |
| 결합도   | 높아지기 쉽다 | 낮다         |
| 변경 영향 | 크다      | 작다         |
| 테스트   | 어렵다     | 쉽다         |
| 유연성   | 낮다      | 높다         |

---

## 7. 언제 써야 하는가

* **extends**

  * 공통 로직을 재사용할 때 사용한다
  * 강한 is-a 관계일 때 사용한다

* **implements**

  * 역할과 규칙을 정의할 때 사용한다
  * 구현 교체가 필요할 때 사용한다

---

## 8. 한 문장으로 끝내기

* **extends는 물려받는다**
* **implements는 약속을 지킨다**


-----

##  다중 상속? 다중구현?

## 1. 결론부터

* **클래스 다중 상속은 안 된다**
* **인터페이스 다중 구현은 된다**

---

## 2. 왜 클래스 다중 상속은 안 되는가

```java
class A {
    void run() {}
}

class B {
    void run() {}
}

// 컴파일 에러
class C extends A, B {}
```

* A와 B에 같은 메서드가 있다
* C가 어떤 run()을 써야 하는지 모호하다
* 다이아몬드 문제이다

→ 자바는 이를 **언어 차원에서 금지**한다

---

## 3. 왜 implements는 가능한가

```java
interface A {
    void run();
}

interface B {
    void stop();
}

class C implements A, B {
    public void run() {}
    public void stop() {}
}
```

* 인터페이스는 구현이 없다
* 충돌할 구현이 존재하지 않는다
* C가 직접 구현한다

→ 다중 구현이 가능하다

---

## 4. default 메서드는 예외인가

```java
interface A {
    default void run() {}
}

interface B {
    default void run() {}
}

// 컴파일 에러
class C implements A, B {}
```

* default 메서드도 구현이다
* 충돌이 발생한다

```java
class C implements A, B {
    @Override
    public void run() {
        A.super.run();
    }
}
```

* 직접 선택하면 해결된다
* 명시적으로 책임을 지게 한다

---



## extends 와 implements 둘다 상속?
맞다 다만 **의미를 섞어서 쓰는 경우가 많다.**

---

## 1. 결론부터 정리

* **개념적으로는 둘 다 상속이다**
* **언어·설계 관점에서는 성격이 다르다**

---

## 2. 왜 둘 다 상속이라고 부르는가

### 상속의 본래 의미

* 기존 타입의 **특성을 이어받아 확장**한다는 의미이다
* 이 기준에서는

  * 클래스 extends
  * 인터페이스 implements
    모두 상속 범주에 들어간다

→ 그래서 **이론서·UML·소프트웨어공학 책**에서는
둘 다 상속이라고 부른다

---

## 3. 왜 실무에서는 구분해서 말하는가

### extends (클래스 상속)

* 구현을 물려받는다
* 강한 is-a 관계이다
* 결합도가 높다

### implements (인터페이스 구현)

* 행위의 규약만 물려받는다
* 역할 상속이다
* 결합도가 낮다

→ 그래서 실무·언어 설명에서는
**상속 vs 구현**으로 나눠 말한다

---

## 4. UML 기준으로 보면

| 관계                   | UML 분류 |
| -------------------- | ------ |
| 클래스 extends 클래스      | 일반화    |
| 클래스 implements 인터페이스 | 실체화    |
| 인터페이스 extends 인터페이스  | 일반화    |

* UML 최상위 개념에서는 전부 **상속 계열**이다
* 표현 방식만 다르다

---

## 5. 헷갈리지 않는 정리 기준

* **이론서**
  → 둘 다 상속이라고 말한다

* **자바 문법·실무**
  → extends는 상속
  → implements는 구현이라고 말한다

---

## 6. 한 문장으로 정리

* **개념적으로는 둘 다 상속이 맞다**
* **실무에서는 의미가 달라서 구분해서 부른다**


## 5. 핵심 차이 한 줄 요약

* 클래스는 **구현 상속**이라 다중 상속이 안 된다
* 인터페이스는 **역할 상속**이라 다중 구현이 된다

