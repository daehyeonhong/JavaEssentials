## Stack & Queue

- Stack: LIFO(Last In First Out) 구조
    - `push()`: 스택에 객체를 저장
    - `pop()`: 스택의 맨 위에 저장된 객체를 꺼냄
- Queue: FIFO(First In First Out) 구조
    - `offer()`: 큐에 객체를 저장
    - `poll()`: 큐의 맨 앞에 저장된 객체를 꺼냄

- Stack과 Queue는 List 인터페이스를 구현한 클래스로 구현됨
    - Stack: ArrayList 클래스를 상속받아 구현
    - Queue: LinkedList 클래스를 상속받아 구현
- Stack과 Queue Method

| Method                     | Description                                                              |
|:---------------------------|:-------------------------------------------------------------------------|
| `boolean empty()`          | 스택이 비어있는지 확인                                                             |
| `Object peek()`            | 스택의 맨 위에 저장된 객체를 반환 pop()과 달리 꺼내지는 않음. (비어있을 때는 `EmptyStackException`발생) |
| `Object pop()`             | 스택의 맨 위에 저장된 객체를 꺼냄 (비어있을 때는 `EmptyStackException`발생)                    |
| `Object push(Object item)` | 스택에 객체를 저장                                                               |
| `int search(Object o)`     | 스택에 저장된 객체를 찾아서 그 위치를 반환 (1부터 시작, 없으면 -1 반환)                             |

| Method                    | Description                                             |
|:--------------------------|:--------------------------------------------------------|
| `boolean add(Object o)`   | 큐에 객체를 저장 (저장에 성공하면 true, 실패하면 false)                   |
| `Object element()`        | 큐의 맨 앞에 저장된 객체를 반환 (비어있을 때는 `NoSuchElementException`발생) |
| `boolean offer(Object o)` | 큐에 객체를 저장 (저장에 성공하면 true, 실패하면 false)                   |
| `Object peek()`           | 큐의 맨 앞에 저장된 객체를 반환 (비어있을 때는 null 반환)                    |
| `Object poll()`           | 큐의 맨 앞에 저장된 객체를 꺼냄 (비어있을 때는 null 반환)                    |
| `Object peek()`           | 큐의 맨 앞에 저장된 객체를 꺼냄 (비어있을 때는 null 반환)                    |

- Queue는 Interface이므로 객체 생성 불가
    1. Queue 인터페이스 직접 구현
    2. Queue 인터페이스를 구현한 클래스를 이용하여 객체 생성 
