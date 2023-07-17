## `HashSet`

- `HashSet`은 순서가 없고 중복을 허용하지 않는 데이터 집합이다.
- 순서를 유지하고 싶다면 Linked`HashSet`을 사용하면 된다.

## TreeSet

- 범위 검색과 정렬에 유리한 컬렉션이다.
- `HashSet`보다 데이터를 추가하거나 삭제하는데 시간이 더 걸린다.

### `HashSet` - 주요 메서드

| Method                                           | Description                                   |
|:-------------------------------------------------|:----------------------------------------------|
| `HashSet`()                                      | `HashSet`을 생성한다.                              |
| `HashSet`(Collection c)                          | 주어진 컬렉션의 모든 객체를 포함하는 `HashSet`을 생성한다.         |
| `HashSet`(int initialCapacity)                   | 지정된 초기 용량으로 `HashSet`을 생성한다.                  |
| `HashSet`(int initialCapacity, float loadFactor) | 지정된 초기 용량과 load factor로 `HashSet`을 생성한다.      |
| boolean add(Object o)                            | 지정된 객체를 `HashSet`에 추가한다. (합집합)                |
| boolean addAll(Collection c)                     | 지정된 컬렉션의 모든 객체를 `HashSet`에 추가한다.              |
| boolean remove(Object o)                         | 지정된 객체를 `HashSet`에서 제거한다.                     |
| boolean removeAll(Collection c)                  | 지정된 컬렉션에 포함된 객체를 `HashSet`에서 제거한다. (교집합)      |
| boolean retainAll(Collection c)                  | 지정된 컬렉션에 포함된 객체만을 남기고 `HashSet`에서 제거한다.       |
| void clear()                                     | `HashSet`의 모든 객체를 제거한다. (차집합)                 |
| boolean contains(Object o)                       | 지정된 객체가 `HashSet`에 포함되어 있는지 확인한다.             |
| boolean containsAll(Collection c)                | 지정된 컬렉션의 모든 객체가 `HashSet`에 포함되어 있는지 확인한다.     |
| iterator iterator()                              | `HashSet`에 저장된 모든 객체를 하나씩 꺼내는 Iterator를 반환한다. |
| boolean isEmpty()                                | `HashSet`이 비어있는지 확인한다.                        |
| int size()                                       | `HashSet`에 저장된 객체의 개수를 반환한다.                  |
| Object[] toArray()                               | `HashSet`에 저장된 객체를 Object 배열로 반환한다.           |
| <T> T[] toArray(T[] a)                           | `HashSet`에 저장된 객체를 지정된 배열에 담아 반환한다.           |

### `HashSet` 예제

- `HashSet`은 객체를 저장하기 전(`add()`)에 기존에 저장된 객체와 같은지 `hashCode()`와 `equals()`로 비교한다.
