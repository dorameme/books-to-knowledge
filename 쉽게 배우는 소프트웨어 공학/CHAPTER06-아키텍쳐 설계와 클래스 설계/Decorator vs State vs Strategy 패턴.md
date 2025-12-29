# Decorator vs State vs Strategy 패턴


## 1. 핵심 의도 차이

| 구분    | Decorator  | Strategy  | State           |
| ----- | ---------- | --------- | --------------- |
| 목적    | 기능 확장      | 알고리즘 선택   | 상태 기반 행동 변경     |
| 객체 개수 | 여러 개가 중첩된다 | 하나만 선택된다  | 상태 객체가 내부에서 바뀐다 |
| 교체 주체 | 외부에서 조합한다  | 외부에서 선택한다 | 객체 스스로 변경한다     |
| 핵심 질문 | 기능을 더 붙일까  | 어떤 방법을 쓸까 | 지금 상태가 무엇인가     |

---

## 2. 코드 구조 차이 (개념 중심)

### 2-1. Strategy 패턴

```java
interface PayStrategy {
    void pay();
}

class CardPay implements PayStrategy {}
class CashPay implements PayStrategy {}

class Order {
    private PayStrategy strategy;
}
```

* 알고리즘을 캡슐화한다
* 실행 시 전략을 바꾼다
* **조건문 제거 목적**이다

---

### 2-2. State 패턴

```java
interface State {
    void handle();
}

class OpenState implements State {}
class ClosedState implements State {}

class Door {
    private State state;
}
```

* 상태 객체가 행동을 결정한다
* 상태 전이가 내부에서 일어난다
* **상태 머신 대체 목적**이다

---

### 2-3. Decorator 패턴

```java
interface Coffee {
    int cost();
}

class BasicCoffee implements Coffee {}

class MilkDecorator implements Coffee {
    private Coffee coffee;
}
```

* 객체를 감싸서 기능을 추가한다
* 상속 대신 조합을 사용한다
* **기능 조합 확장 목적**이다

---

## 3. 실생활 예시로 바로 구분

### Decorator

* 기본 커피 + 우유 + 시럽이다
* 기능을 계속 추가한다

### Strategy

* 결제 방법 선택이다
* 카드 / 현금 / 포인트 중 하나이다

### State

* 문 상태이다
* 열림 / 닫힘에 따라 동작이 바뀐다

---

## 4. 가장 쉬운 구별 질문

| 질문              | 패턴        |
| --------------- | --------- |
| 기능을 계속 붙이는가     | Decorator |
| 방법을 골라 쓰는가      | Strategy  |
| 상태에 따라 행동이 바뀌는가 | State     |

---

## 5. Strategy vs State 헷갈림 정리

| 구분    | Strategy | State |
| ----- | -------- | ----- |
| 변경 주체 | 외부       | 내부    |
| 변경 이유 | 선택       | 상태 전이 |
| 객체 관점 | 수단       | 현재 상황 |

* Strategy는 **사용자가 고른다**
* State는 **객체가 스스로 바꾼다**

---

## 6. Decorator vs Strategy 차이 핵심

* Decorator는 **확장**이다
* Strategy는 **대체**이다

---

## 8. 한 문장으로 끝내기

* **Decorator는 기능 추가**
* **Strategy는 알고리즘 교체**
* **State는 상태에 따른 행동 변경**
