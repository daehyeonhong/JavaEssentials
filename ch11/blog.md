# 자바의 정석 11강

## Collection Framework

### 컬렉션 프레임 워크란?

- 컬렉션 프레임워크는 데이터 군을 저장하는 클래스들을 표준화한 설계이다.
- 컬렉션 프레임워크의 핵심 인터페이스는 `List`, `Set`, `Map`이다.
- `List`와 `Set`은 모두 `Collection` 인터페이스를 상속받는다.
- `Map`은 `Collection` 인터페이스를 상속받지 않는다.

### Collection 인터페이스

- `Collection` 인터페이스는 객체의 집합을 나타내는 인터페이스이다.

| Method                            | Description                          |
|:----------------------------------|:-------------------------------------|
| boolean add(Object o)             | 지정된 객체를 컬렉션에 추가                      |
| boolean addAll(Collection c)      | 지정된 컬렉션의 모든 객체를 컬렉션에 추가              |
| void clear()                      | 컬렉션의 모든 객체를 삭제                       |
| boolean contains(Object o)        | 지정된 객체가 컬렉션에 포함되어 있는지 여부             |
| boolean containsAll(Collection c) | 지정된 컬렉션의 모든 객체가 컬렉션에 포함되어 있는지 여부     |
| boolean equals(Object o)          | 두 컬렉션이 같은지 여부                        |
| int hashCode()                    | 컬렉션의 해시코드 반환                         |
| boolean isEmpty()                 | 컬렉션이 비어있는지 여부                        |
| Iterator iterator()               | 컬렉션의 모든 객체를 순서대로 검색하기 위한 Iterator 반환 |
| boolean remove(Object o)          | 지정된 객체를 컬렉션에서 삭제                     |
| boolean removeAll(Collection c)   | 지정된 컬렉션에 포함된 객체를 컬렉션에서 삭제            |
| boolean retainAll(Collection c)   | 지정된 컬렉션에 포함된 객체만을 컬렉션에 남기고 나머지는 삭제   |
| int size()                        | 컬렉션에 포함된 객체의 개수를 반환                  |
| Object[] toArray()                | 컬렉션에 포함된 객체들을 객체배열로 반환               |
| Object[] toArray(Object[] a)      | 컬렉션에 포함된 객체들을 지정된 배열에 저장             |

### List

- `List`는 순서가 있고 중복을 허용하는 데이터 구조이다.
- 구현체로는 `ArrayList`, `LinkedList`, `Vector` 등이 있다.
- 인덱스를 이용하여 객체를 관리한다.
- `ArrayList`는 배열을 이용하여 구현되었고, `LinkedList`는 연결리스트를 이용하여 구현되었다.
- `Vector`는 `ArrayList`와 동일하지만 동기화된 메서드로 구성되어 있어 멀티스레드 환경에서 안전하다. 다만 성능이 좋지 않다.(구형 자바에서 사용)

### Set

- `Set`은 순서가 없고 중복을 허용하지 않는 데이터 구조이다.(집합)
- `List`와 달리 인덱스로 객체를 관리하지 않는다.
- 전체적으로 `List`의 반대되는 개념이다.
- 구현체로는 `HashSet`, `TreeSet` 등이 있다.
- `HashSet`은 해시 알고리즘을 이용하여 구현되었고, `TreeSet`은 이진 검색 트리 알고리즘을 이용하여 구현되었다.

### ArrayList, LinkedList, Vector

- 앞서 설명한 것처럼 `ArrayList`는 배열을 이용하여 구현되었고, `LinkedList`는 연결리스트를 이용하여 구현되었다.
- `LinkedList`는 노드를 이용하여 데이터를 저장하고, `ArrayList`는 배열을 이용하여 데이터를 저장하는데 이는 데이터의 추가, 삭제에 있어서 성능 차이를 보인다.
- `ArrayList`는 데이터의 추가, 삭제가 빈번하지 않을 때 성능이 좋고, `LinkedList`는 데이터의 추가, 삭제가 빈번할 때 성능이 좋다.

### Stack, Queue

- `Stack`의 특징은 LIFO(Last In First Out)이고, `Queue`의 특징은 FIFO(First In First Out)이다.
- `Stack`은 `push()`와 `pop()` 메서드를 이용하여 데이터를 추가하고 삭제하고, `Queue`는 `offer()`와 `poll()` 메서드를 이용하여 데이터를 추가하고 삭제한다.
- `Stack`은 `Vector`를 상속받아 구현되었고, `Queue`는 `Collection`을 상속 받은 인터페이스이다.

```java
public class Stack<E> extends Vector<E> {
    ...
}
```

- `Queue`를 사용하는 방법은 직접 구현하거나, 구현된 클래스를 사용하는 방법이 있다. 대표적인 예로 `LinkedList`가 있다.(`Queue`를 상속받은 `Deque` 인터페이스를 구현하고 있음)

```java
public class LinkedList<E> extends AbstractSequentialList<E> implements List<E>, Deque<E>, Cloneable, java.io.Serializable {
    ...
}
``` 

### HashSet, TreeSet

- `HashSet`은 해시 알고리즘을 이용하여 구현되었고, `TreeSet`은 이진 검색 트리 알고리즘을 이용하여 구현되었다.
- `HashSet`은 해시 알고리즘을 이용하기 때문에 데이터의 순서를 보장하지 않지만, `TreeSet`은 이진 검색 트리 알고리즘을 이용하기 때문에 데이터의 순서를 보장한다.
- 이런 특성 때문에 `HashSet`은 데이터의 추가, 삭제가 빈번할 때 성능이 좋고, `TreeSet`은 정렬된 데이터가 필요할 때 성능이 좋다.

### HashSet

- `HashSet`은 해시 알고리즘을 이용하여 구현되었다고 했는데, 이는 `HashMap`을 이용하여 구현되었다는 것을 의미한다.
- `HashSet`은 `add(E e)`는 `HashMap`의 `put(K key, V value)`를 이용하여 구현되었다.

```java

public class HashSet<E>
        extends AbstractSet<E>
        implements Set<E>, Cloneable, java.io.Serializable {
    ...

    public boolean add(E e) {
        return map.put(e, PRESENT) == null;
    }
    ...
}
```

- `java`에서 `Hash`는 `hashCode()`와 `equals()`를 이용하여 구현되는데, `HashSet`은 `hashCode()`와 `equals()`를 이용하여 중복된 데이터를 저장하지 않는다.

### HashMap

- `HashMap`은 해시 알고리즘을 이용하여 구현되었다.
- 객체는 `Objects.hash()`를 이용하여 해시코드를 생성한다.
- `HashMap`은 `put(K key, V value)`를 이용하여 데이터를 저장하고, `get(Object key)`를 이용하여 데이터를 검색한다.
- `Map`은 `Collection`을 상속받은 인터페이스가 아니기 때문에 `Collection`의 메서드를 사용할 수 없지만, `keySet()`, `values()`, `entrySet()`을
  이용하여 `Collection`의 메서드를 사용할 수 있다.
- `HashMap`은 `LinkedList`를 이용하여 해시 충돌을 해결한다.

#### `Java`에서의 `Hash`란?

- `Java`에서 `Hash`는 `hashCode()`와 `equals()`를 이용하여 구현된다.
- `hashCode()`는 객체의 해시코드를 반환하는 메서드이고, `equals()`는 객체의 동등성을 비교하는 메서드이다.
- `hashCode()`와 `equals()`는 `Object` 클래스에 정의되어 있고, `Object` 클래스는 모든 클래스의 최상위 클래스이기 때문에 모든 클래스는 `hashCode()`와 `equals()`를
  사용할 수 있다.
- `hashCode()`와 `equals()`를 사용하기 위해서는 `hashCode()`와 `equals()`를 오버라이딩 해야한다.

### Collections

- `Collections`는 `Collection`의 유틸리티 메서드를 제공하는 클래스이다.
- `Collections`는 `Collection`의 메서드를 사용할 수 없는 `Map`에 대한 메서드도 제공한다.

## 자바의 정석 12장

### 제네릭

- 제네릭은 클래스 내부에서 사용할 데이터 타입을 외부에서 지정하는 기법이다.
- 제네릭을 사용하면 클래스 내부에서 사용할 데이터 타입을 컴파일 시에 체크할 수 있기 때문에 데이터 타입 안정성을 높일 수 있다. 다만 컴파일 되고 나면 제네릭 타입은 제거되기 때문에
  런타임 시에는 제네릭 타입에 대한 정보가 없다.
- 제네릭 타입은 클래스와 인터페이스, 메서드에서 사용할 수 있다.
- 제네릭 타입은 `<>`를 이용하여 선언한다. 해당 연산자는 `diamond operator`라고 부른다.
- wildcard(`<?>`)를 이용하여 제네릭 타입을 제한할 수 있다. `?`는 모든 타입을 의미한다. `extends`를 이용하여 상위 타입을 제한할 수 있다. `super`를 이용하여 하위 타입을 제한할 수
  있다.

### 열거형

- 열거형은 서로 관련된 상수를 편리하게 선언하기 위한 것이다. `enum` 키워드를 이용하여 선언한다. 모든 `enum` class는 `java.lang.Enum`을 상속받는다.
- 같은 데이터라도 `==`를 이용하여 비교하면 `false`를 반환한다. `==`는 주소값을 비교하기 때문이다. `equals()`를 이용하여 비교하면 `true`를 반환한다.
- `Java`의 열거형은 `C`나 `C++`의 열거형과 달리 값뿐만 아니라 메서드나 생성자를 가질 수 있고, 객체 자체를 비교한다.
- `values()`를 이용하여 열거형의 모든 상수를 배열로 반환할 수 있다.

### 애너테이션

- 애너테이션은 `@interface`를 이용하여 선언한다.
- 애너테이션은 메타 데이터를 프로그래밍 언어에 추가하는 기능이다. 다양한 대상에 사용 가능하고, `Java` 컴파일러는 애너테이션을 통해 코드를 검사하고, 애너테이션 정보를
  사용하여 코드를 생성할 수 있다.

### 표준 애너테이션

| Annotation        | Description                                 |
|-------------------|---------------------------------------------|
| @Override         | 어노테이션이 달린 메서드가 오버라이딩된 메서드라는 것을 컴파일러에게 알려준다. |
| @Deprecated       | 어노테이션이 달린 대상이 더 이상 사용되지 않는다는 것을 알려준다.       |
| @SuppressWarnings | 어노테이션이 달린 대상에 대한 컴파일 경고를 무시하도록 컴파일러에게 알려준다. |

### 메타 애너테이션

| Annotation  | Description                          | Values                             |
|-------------|--------------------------------------|------------------------------------|
| @Target     | 애너테이션이 적용 가능한 대상을 지정한다.              | TYPE, FIELD, METHOD, PARAMETER ... |
| @Retention  | 애너테이션이 유지되는 기간을 지정한다.                | SOURCE, CLASS, RUNTIME             |
| @Documented | 애너테이션 정보가 javadoc으로 작성된 문서에 포함되게 한다. |                                    |
| @Inherited  | 애너테이션이 자손 클래스에 상속되도록 한다.             |                                    |

## 자바의 정석 13장

### 스레드

#### 스레드와 프로세스

- 프로세스는 실행 중인 프로그램이다. 프로세스는 최소 하나의 스레드를 가지고 있다. 스레드는 프로세스가 생성되어 종료될 때까지 실행되는 프로그램 흐름이다. 하나의 프로세스에는 여러 개의
  스레드가 있을 수 있다.
- 스레드는 프로세스의 자원을 공유한다. 스레드는 자신만의 스택을 가지고 있고, 나머지 메모리는 공유한다. 스레드는 자신만의 PC(Program Counter)를 가지고 있고, 나머지 레지스터는
  공유한다.

### 스레드의 생성과 실행

- 스레드는 `Thread` 클래스를 상속받거나 `Runnable` 인터페이스를 구현하여 생성할 수 있다. `Thread` 클래스를 상속받으면 다른 클래스를 상속받을 수 없기 때문에 대부분의 경우
  `Runnable` 인터페이스를 구현하여 스레드를 생성한다.
- `Thread` 클래스의 생성자 중에서 `Thread(Runnable target)`을 이용하여 스레드를 생성할 수 있다. `Runnable` 인터페이스를 구현한 클래스의 인스턴스를 생성자의 매개변수로 넘겨주면
  된다.
- `Tread` 클래스도 `Runnable` 인터페이스를 구현하고 있기 때문에 `Thread` 클래스의 인스턴스를 생성자의 매개변수로 넘겨줄 수 있다.
- `Thread` 클래스의 `start()` 메서드를 호출하면 스레드가 실행된다. `start()` 메서드는 `run()` 메서드를 호출한다. `run()` 메서드는 스레드가 실행할 코드를 담고
  넘겨주면 된다. **주의** `run()`
  메서드를 직접 호출하면 스레드가 실행되지 않고, 단순히 메서드를 호출한 것이다.

### 싱글 스레드와 멀티 스레드, 스레드의 I/O 블락킹

- 싱글 스레드는 하나의 스레드만 실행하는 것이다. 멀티 스레드는 여러 개의 스레드를 실행하는 것이다. `main()` 메서드를 실행하는 스레드는 싱글 스레드이다. `main()` 메서드에서
  생성한 스레드는 멀티 스레드이다.
- 스레드는 I/O 작업을 수행할 때 블락킹이 발생한다. 블락킹이 발생하면 스레드는 I/O 작업이 완료될 때까지 대기하게 된다. 블락킹이 발생하면 스레드는 다른 스레드에게 CPU(프로세서)를
  양보하게 된다. 블락킹이 발생하지 않는 스레드는 종료시까지 계속 CPU를 점유하게 된다.

### 스레드의 우선순위와 그룹

- 스레드는 우선순위를 가지고 있다. 우선순위는 `1`에서 `10`까지의 값을 가지며, `10`이 가장 높은 우선순위이다. `Thread` 클래스의 `setPriority()` 메서드를 이용하여 우선순위를
  지정할 수 있다. `getPriority()` 메서드를 이용하여 우선순위를 반환할 수 있다.
- 모든 스레드는 하나의 그룹에 속해있다. 스레드 그룹은 스레드를 관리하기 위한 것이다. 스레드 그룹은 `ThreadGroup` 클래스를 이용하여 생성할 수 있다. 스레드 그룹은
  `ThreadGroup(String name)` 생성자를 이용하여 생성할 수 있다. 스레드 그룹은 `ThreadGroup` 클래스의 `setMaxPriority()` 메서드를 이용하여 그룹 내의 모든 스레드의
  최대 우선순위를 지정할 수 있다. `getMaxPriority()` 메서드를 이용하여 그룹 내의 모든 스레드의 최대 우선순위를 반환할 수 있다.

### 데몬 스레드

- 데몬 스레드란? 다른 스레드가 모두 종료되면 자동으로 종료되는 스레드이다. 데몬 스레드는 `Thread` 클래스의 `setDaemon()` 메서드를 이용하여 생성할 수 있다. `setDaemon()`
  메서드의 매개변수로 `true`를 넘겨주면 데몬 스레드가 된다. `false`를 넘겨주면 데몬 스레드가 아니다. 또한 데몬 스레드는 반드시 `start()` 메서드를 호출하기 전에 생성해야 한다.
- 데몬 스레드는 다른 스레드가 모두 종료되면 자동으로 종료되기 때문에 주로 백그라운드에서 실행되는 작업을 수행하는 스레드로 사용된다. 데몬 스레드는 자동 저장, 가비지 컬렉션,
  화면 자동 갱신 등의 작업을 수행한다.

### `sleep()`, `interrupt()`, `suspend()`, `resume()`, `join()`, `yield()`

- `sleep()` 메서드는 스레드를 잠시 멈추게 한다. `sleep()` 메서드는 `Thread` 클래스의 정적 메서드이다. `sleep()` 메서드는 `Thread`
  클래스의 `sleep(long millis)` 메서드를
  이용하여 호출할 수 있다. `sleep()` 메서드는 매개변수로 지정한 시간(밀리초) 동안 스레드를 멈춘다. `sleep()` 메서드는 `InterruptedException` 예외를 발생시킨다.
- `interrupt()` 메서드는 스레드를 깨운다. `interrupt()` 메서드는 `Thread` 클래스의 인스턴스 메서드이다. `interrupt()` 메서드는 `Thread`
  클래스의 `interrupt()`
  메서드를 이용하여 호출할 수 있다. `interrupt()` 메서드는 스레드를 깨우기 위해 `sleep()` 메서드를 호출한 스레드에게 `InterruptedException` 예외를 발생시킨다.
- `suspend()` 메서드는 스레드를 잠시 멈추게 한다. `suspend()` 메서드는 `Thread` 클래스의 인스턴스 메서드이다. `suspend()` 메서드는 `Thread`
  클래스의 `suspend()`
  메서드를 이용하여 호출할 수 있다. `suspend()` 메서드는 스레드를 잠시 멈추게 한다. `suspend()` 메서드는 `resume()` 메서드가 호출되기 전까지 스레드를 멈춘다.
- `resume()` 메서드는 `suspend()` 메서드에 의해 멈춘 스레드를 다시 실행시킨다. `resume()` 메서드는 `Thread` 클래스의 인스턴스 메서드이다. `resume()`
  메서드는 `Thread`
  클래스의 `resume()` 메서드를 이용하여 호출할 수 있다. `resume()` 메서드는 `suspend()` 메서드에 의해 멈춘 스레드를 다시 실행시킨다.
- `join()` 메서드는 스레드가 종료될 때까지 기다린다. `join()` 메서드는 `Thread` 클래스의 인스턴스 메서드이다. `join()` 메서드는 `Thread`
  클래스의 `join()` 메서드를
  이용하여 호출할 수 있다. `join()` 메서드는 매개변수로 지정한 시간(밀리초) 동안 스레드가 종료될 때까지 기다린다.
- `yield()` 메서드는 스레드가 실행 중에 다른 스레드에게 실행을 양보한다. `yield()` 메서드는 `Thread` 클래스의 정적 메서드이다. `yield()` 메서드는 `Thread`
  클래스의 `yield()`
  메서드를 이용하여 호출할 수 있다. `yield()` 메서드는 실행 중에 다른 스레드에게 실행을 양보한다.

### 스레드의 동기화

- 스레드간의 작업을 동기화하기 위해서는 `synchronized` 키워드를 사용한다. `synchronized` 키워드는 메서드나 블록에 사용할 수 있다. `synchronized` 키워드를
  사용하면 스레드가 작업을 수행하고 있는 객체를 잠금 상태로 만든다. 잠금 상태로 만들어진 객체는 다른 스레드가 사용할 수 없다. `synchronized` 키워드를 사용하면
  스레드간의 작업을 동기화할 수 있다.
- `synchronized` 키워드를 사용하여 동기화된 메서드를 호출하면 스레드는 해당 메서드가 포함된 객체를 잠금 상태로 만든다. 잠금 상태로 만들어진 객체는 다른 스레드가 사용할 수
  없다. `synchronized` 키워드를 사용하여 동기화된 블록을 실행하면 스레드는 해당 블록이 포함된 객체를 잠금 상태로 만든다. 잠금 상태로 만들어진 객체는 다른 스레드가 사용할 수
  없다.
- 임계 영역이란? 여러 스레드가 동시에 접근할 수 있는 공유 데이터를 처리하는 코드 영역이다. 임계 영역을 사용할 때는 `synchronized` 키워드를 사용하여 동기화된 메서드나
  블록을 만들어야 한다. 임계 영역을 사용하지 않으면 여러 스레드가 동시에 접근하여 데이터를 변경할 수 있기 때문에 잘못된 결과가 발생할 수 있다.
- `synchronized` 키워드를 사용하여 동기화된 메서드를 호출하면 스레드는 해당 메서드가 포함된 객체를 잠금 상태로 만든다. 잠금 상태로 만들어진 객체는 다른 스레드가 사용할 수 없다.

### `wait()`, `notify()`, `notifyAll()`

- `wait()` 메서드는 스레드를 일시 정지시킨다. `wait()` 메서드는 `Object` 클래스의 인스턴스 메서드이다. `wait()` 메서드는 `Object` 클래스의 `wait()`
  메서드를 이용하여 호출할 수 있고, `notify()` 메서드가 호출될 때까지 스레드를 일시 정지시킨다.

## 자바의 정석 14장

### Lambda

- 람다식은 메서드를 하나의 식으로 표현한 것이다. 람다식은 익명 함수(anonymous function)를 생성하기 위한 식으로 객체 지향 언어보다는 함수 지향 언어에 가깝다.
- 람다식 작성 방법
    1. 메소드 이름과 반환값을 제거하고 `->`를 사용하고, 문장이나 문장 블록을 작성한다. `(int a, int b) -> { return a + b; }`
    2. 반환값이 있는 경우, 식이나 값만 적고 `return`문은 사용하지 않는다.(`;`도 제거) `(int a, int b) -> a + b`
    3. 매개변수의 타입이 추론 가능하다면 생략할 수 있다. `(a, b) -> a + b`

- 주의사항
    1. 매개변수가 하나인 경우 괄호 `()`를 생략할 수 있다.(타입이 없는 경우) `a -> a * a // OK` `int a -> a * a // ERROR`
    2. 블록`{}`
       안의 문장이 하나인 경우에는 블록 생략 가능 `(int i) -> System.out.println(i) // OK`
- 람다식은 익명 함수가 아닌 익명 객체이다.

### 함수형 인터페이스

- 람다식은 익명 객체이므로, 람다식을 다루기 위한 참조변수가 필요하다. 람다식의 타입은 함수형 인터페이스로만 표현할 수 있다. 함수형 인터페이스는 추상 메서드가 하나만
  선언된 인터페이스이다. 함수형 인터페이스는 `@FunctionalInterface` 어노테이션을 사용하여 선언한다. 함수형 인터페이스는 람다식을 다루기 위한 참조변수의 타입으로만
  사용할 수 있다.

### `java.util.function` 패키지

| Functional Interface | Method              | Description                   |
|----------------------|---------------------|-------------------------------|
| `Runnable`           | `void run()`        | 매개변수 없음, 반환값 없음               |
| `Supplier<T>`        | `T get()`           | 매개변수 없음, T 타입 객체 반환           |
| `Consumer<T>`        | `void accept(T t)`  | T 타입 객체를 매개변수로 받고, 반환값 없음     |
| `Function<T, R>`     | `R apply(T t)`      | T 타입 객체를 매개변수로 받고, R 타입 객체 반환 |
| `Predicate<T>`       | `boolean test(T t)` | T 타입 객체를 매개변수로 받고, boolean 반환 |

- 매개변수가 2개인 함수형 인터페이스는 `Bi` 접두사를 붙인다.

| Functional Interface  | Method                   | Description                      |
|-----------------------|--------------------------|----------------------------------|
| `BiConsumer<T, U>`    | `void accept(T t, U u)`  | T, U 타입 객체를 매개변수로 받고, 반환값 없음     |
| `BiFunction<T, U, R>` | `R apply(T t, U u)`      | T, U 타입 객체를 매개변수로 받고, R 타입 객체 반환 |
| `BiPredicate<T, U>`   | `boolean test(T t, U u)` | T, U 타입 객체를 매개변수로 받고, boolean 반환 |

- 매개변수의 타입과 반환값의 타입이 같은 함수형 인터페이스

| Functional Interface | Method                | Description                   |
|----------------------|-----------------------|-------------------------------|
| `UnaryOperator<T>`   | `T apply(T t)`        | T 타입 객체를 매개변수로 받고, T 타입 객체 반환 |
| `BinaryOperator<T>`  | `T apply(T t1, T t2)` | T 타입 객체를 매개변수로 받고, T 타입 객체 반환 |

### `Predicate`의 결합, `CollectionFramework`와 `Functional Interface`

| Method           | Description                               |
|------------------|-------------------------------------------|
| `and(Predicate)` | 두 Predicate가 모두 true를 반환하면 true를 반환한다.    |
| `or(Predicate)`  | 두 Predicate 중 하나라도 true를 반환하면 true를 반환한다. |
| `negate()`       | Predicate의 결과를 부정한다.                      |

- 함수형 인터페이스를 활용하는 컬렉션 프레임워크의 메서드

| Interface    | Method                            | Description                                          |
|--------------|-----------------------------------|------------------------------------------------------|
| `Collection` | `removeIf(Predicate)`             | Predicate가 true를 반환하는 요소를 제거한다.                      |
| `List`       | `replaceAll(UnaryOperator)`       | 모든 요소에 대해 UnaryOperator를 적용한다.                       |
| `Iterator`   | `forEachRemaining(Consumer)`      | 모든 요소에 대해 Consumer를 적용한다.                            |
| `Map`        | `compute(K, BiFunction)`          | 지정된 키가 있을 때는 BiFunction을 적용하고, 없을 때는 Function을 적용한다. |
| `Map`        | `computeIfAbsent(K, Function)`    | 지정된 키가 없을 때만 Function을 적용한다.                         |
| `Map`        | `computeIfPresent(K, BiFunction)` | 지정된 키가 있을 때만 BiFunction을 적용한다.                       |
| `Map`        | `merge(K, V, BiFunction)`         | 지정된 키가 있을 때는 BiFunction을 적용하고, 없을 때는 지정된 값을 저장한다.    |
| `Map`        | `forEach(BiConsumer)`             | 모든 요소에 대해 BiConsumer를 적용한다.                          |
| `Map`        | `replaceAll(BiFunction)`          | 모든 요소에 대해 BiFunction을 적용한다.                          |

### 메서드 참조

- 람다식이 하나의 메서드만 호출하는 경우, 람다식을 메서드 참조로 대체할 수 있다.

| Type              | Lambda Expressions           | Method Reference          |
|-------------------|------------------------------|---------------------------|
| Static 메서드 참조     | `(x) -> ClassName.method(x)` | `${Classname}::${method}` |
| Instance 메서드 참조   | `(obj, x) -> obj.method(x)`  | `${Classname}::${method}` |
| 특정 객체 인스턴스 메서드 참조 | `(x) -> obj.method(x)`       | `${obj}::${method}`       |

- static methodReference

```java
Function<String, Integer> f=Integer::parseInt;
```

- 생성자와 배열 생성자 참조
  `Suplier<MyClass> s = () -> new MyClass();` -> `Suplier<MyClass> s = MyClass::new;`
  `Function<Integer, MyClass> s = (i) -> new MyClass(i);` -> `Function<Integer, MyClass> s = MyClass::new;`
  `Function<Integer, int[]> f = x -> new int[x]` -> `Function<Integer, int[]> f = int[]::new;`

### Stream

- 스트림이란? 데이터 소스를 추상화하고, 데이터를 다루는데 자주 사용되는 메서드들을 정의해 놓은 것이다. 즉, 데이터 소스를 읽기 위한
  연산과 쓰기 위한 연산을 지원하며, 한 번 생성하고 사용한 스트림은 재사용할 수 없다. 또한 스트림은 작업을 내부 반복으로 처리한다.
- 스트림은 중간 연산과 최종 연산을 제공한다.
    1. 중간 연산은 스트림을 리턴하므로 여러 개의 중간 연산을 연결할 수 있다.
    2. 최종 연산은 스트림을 리턴하지 않으므로 중간 연산이 연결된 경우에만 실행된다.
- 스트림은 데이터 소스로부터 데이터를 읽기만 할 뿐 변경하지 않고, Iterator처럼 일회용이다.
- 최종 연산 전까지 중간연산이 수행되지 않는다. 즉, 지연 연산이라고 한다.

### Optional

- Optional은 NullPointerException을 유발하는 null을 직접 다루는 것을 피하기 위해 사용한다.
- Optional은 null이 아닌 값을 저장하고, 그 값을 사용하는 메서드를 호출하는 방식으로 사용한다.

| Method                  | Description                                             |
|-------------------------|---------------------------------------------------------|
| `empty()`               | 빈 Optional 객체를 반환한다.                                    |
| `of(T value)`           | null이 아닌 객체를 저장한 Optional 객체를 반환한다.                     |
| `ofNullable(T value)`   | null인지 아닌지 확신할 수 없는 객체를 저장한 Optional 객체를 반환한다.          |
| `get()`                 | Optional 객체에 저장된 값을 반환한다.                               |
| `ifPresent(Consumer)`   | Optional 객체에 저장된 값이 null이 아니면 Consumer를 실행한다.           |
| `isPresent()`           | Optional 객체에 저장된 값이 null이면 true를 반환한다.                  |
| `ofElse(T value)`       | Optional 객체에 저장된 값이 null이면 기본값을 반환한다.                   |
| `ofElseGet(Supplier)`   | Optional 객체에 저장된 값이 null이면 Supplier를 실행한 결과를 반환한다.      |
| `ofElseThrow(Supplier)` | Optional 객체에 저장된 값이 null이면 Supplier를 실행한 결과를 예외를 발생시킨다. |
