## ArrayList

### Vector와 ArrayList

- Vector와 ArrayList는 List 인터페이스를 구현한 클래스
- Vector는 동기화 처리가 되고, ArrayList는 동기화 처리가 되지 않음
- List Interface를 구현하므로, 저장순서가 유지되고 중복을 허용한다.
- 데이터의 저장공간으로 배열을 사용한다.(배열의 단점을 보완하기 위해 나온 클래스)

```java
// Vector
public class Vector extends AbstractList implements List, RandomAccess, Cloneable, Serializable {
    // ...
    protected Object[] elementData; // 객체를 담기 위한 객체배열
    // ...
}
```

## ArrayList의 주요 메서드

| method                                   | description                              |
|------------------------------------------|------------------------------------------|
| ArrayList()                              | ArrayList 생성자                            |
| ArrayList(Collection c)                  | Collection을 ArrayList로 변환                |
| ArrayList(int initialCapacity)           | 초기 용량을 지정하여 ArrayList 생성                 |
| boolean add(Object o)                    | ArrayList에 객체 추가                         |
| void add(int index, Object element)      | ArrayList의 index에 객체 추가                  |
| boolean addAll(Collection c)             | Collection의 모든 객체를 ArrayList에 추가         |
| boolean addAll(int index, Collection c)  | ArrayList의 index에 Collection의 모든 객체를 추가  |
| int indexOf(Object o)                    | ArrayList에서 객체의 index를 반환                |
| int lastIndexOf(Object o)                | ArrayList에서 객체의 마지막 index를 반환            |
| boolean contains(Object o)               | ArrayList에 객체가 존재하는지 확인                  |
| Object get(int index)                    | ArrayList의 index에 있는 객체를 반환              |
| Object set(int index, Object element)    | ArrayList의 index에 있는 객체를 element로 변경     |
| List subList(int fromIndex, int toIndex) | ArrayList의 fromIndex부터 toIndex까지의 객체를 반환 |
| Object[] toArray()                       | ArrayList에 있는 객체를 배열로 반환                 |
| Object[] toArray(Object[] a)             | ArrayList에 있는 객체를 지정한 배열로 반환             |
| boolean isEmpty()                        | ArrayList가 비어있는지 확인                      |
| void trimToSize()                        | ArrayList의 용량을 현재 객체의 개수로 줄인다.           |
| int size()                               | ArrayList에 있는 객체의 개수를 반환                 |

### ArrayList에 저장된 객체의 삭제 과정

1. ArrayList에 저장된 세 번째 객체를 삭제하는 경우, list.remove(2)를 호출한다.
2. 삭제하고자 하는 데이터 아래의 데이터를 한 칸씩 위로 복사해서 삭제할 데이터를 덮어쓴다.
3. 마지막 데이터를 null로 변경한다.
4. ArrayList의 size를 1 감소시킨다.

### ArrayList에 저장된 객체의 삭제과정

1. ArrayList에 저장된 첫 번째 객체부터 삭제하는 경우(배열 복사 발생)
2. ArrayList에 저장된 마지막 객체부터 삭제하는 경우(배열 복사 발생하지 않음)
