## Iterator, ListIterator, Enumeration

- 컬렉션에 저장된 데이터를 접근하는데 사용되는 인터페이스
- `Enumeration`은 `Iterator`의 구버전

### Iterator

| Method                                 | Description                                                     |
|:---------------------------------------|:----------------------------------------------------------------|
| boolean hasNext()                      | 읽어 올 요소가 남아있는지 확인                                               |
| Object next()                          | 다음 요소를 읽어옴. hasNext()를 호출해서 읽어 올 요소가 있는지 확인하는 것이 안전하다.          |
| void remove()                          | next()로 읽어 온 요소를 삭제 next()를 호출한 다음에 remove()를 호출해야 함.(Optional) |
| void forEachRemaining(Consumer action) | Iterator의 모든 요소를 지정된 action을 이용해서 처리                            |

### Enumeration

| Method                    | Description                                                                          |    
|:--------------------------|:-------------------------------------------------------------------------------------|
| boolean hasMoreElements() | 읽어 올 요소가 남아있는지 확인                                                                    |
| Object nextElement()      | 다음 요소를 읽어옴. hasMoreElements()를 호출해서 읽어 올 요소가 있는지 확인하는 것이 안전하다. Iterator의 next()와 같다. |

### ListIterator

- Iterator의 기능을 향상시킨 것으로 양방향으로 이동이 가능하다.
- next()와 previous()를 이용해서 이동한다.
- List Interface를 구현한 컬렉션에서만 사용할 수 있다.

## Iterator, ListIterator, Enumeration

- 컬렉션에 저장된 요소들을 읽어오는 방법을 표준화한 것
- ex) List를 사용한 코드에서 Set으로 변경하고자 할 때, Iterator를 사용하면 코드의 변경을 최소화할 수 있다.

### Iterator

- Iterator는 일회용이다. (한 번 사용하고 나면 다시 사용할 수 없다.)
- Iterator를 다 사용했다면 다시 얻어와야 한다.

## Map과 Iterator

- Map은 Collection을 상속받지 않기 때문에 Iterator를 사용할 수 없다.
- 하지만 Map에는 keySet(), entrySet(), values()와 같은 메서드가 정의되어 있어서 이 메서드들이 반환하는 Set, Collection에 대해서는 Iterator를 사용할 수 있다.
```java
final Map<String, Integer> map = new HashMap<>();
final Iterator<String> iterator = map.keySet().iterator();
```
