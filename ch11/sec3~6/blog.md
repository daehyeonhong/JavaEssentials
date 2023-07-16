## Collection Interface Methods

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

## List Interface - 순서 O, 중복 O

- List 인터페이스 구현 클래스: ArrayList, Vector, LinkedList, Stack, Queue 등

| Method                                   | Description                                             |
|------------------------------------------|---------------------------------------------------------|
| void add(int index, Object element)      | 지정된 위치(index)에 객체(element)를 추가                          |
| boolean addAll(int index, Collection c)  | 지정된 위치(index)에 컬렉션에 포함된 객체들을 추가                         |
| Object get(int index)                    | 지정된 위치(index)에 있는 객체를 반환                                |
| int indexOf(Object o)                    | 지정된 객체의 위치(index)를 반환                                   |
| int lastIndexOf(Object o)                | 지정된 객체의 마지막 위치(index)를 반환                               |
| ListIterator listIterator()              | List의 객체들을 순서대로 검색하기 위한 ListIterator 반환                 |
| ListIterator listIterator(int index)     | 지정된 위치(index)부터 List의 객체들을 순서대로 검색하기 위한 ListIterator 반환 |
| Object remove(int index)                 | 지정된 위치(index)에 있는 객체를 삭제                                |
| Object set(int index, Object element)    | 지정된 위치(index)에 객체(element)를 저장                          |
| void sort(Comparator c)                  | 지정된 비교자(Comparator)로 List의 객체들을 정렬                      |
| List subList(int fromIndex, int toIndex) | 지정된 범위(`fromIndex`부터 `toIndex`까지)에 있는 객체들을 List로 반환     |

## Set Interface - 순서 X, 중복 X

- Set 인터페이스 구현 클래스: HashSet, SortedSet, TreeSet 등
- 메서드는 Collection 인터페이스와 동일

- 집합과 관련된 메서드를 추가로 제공(Collection 변화 여부를 반환)

| Method                            | Description                             |
|-----------------------------------|-----------------------------------------|
| boolean addAll(Collection c)      | 지정된 컬렉션의 모든 객체를 컬렉션에 추가(합집합)            |
| boolean containsAll(Collection c) | 지정된 컬렉션의 모든 객체가 컬렉션에 포함되어 있는지 여부 (부분집합) |
| boolean removeAll(Collection c)   | 지정된 컬렉션에 포함된 객체를 컬렉션에서 삭제(차집합)          |
| boolean retainAll(Collection c)   | 지정된 컬렉션에 포함된 객체만을 컬렉션에 남기고 나머지는 삭제(교집합) |

## Map Interface - 순서 X, 중복 (key X, value O)

- Map 인터페이스 구현 클래스: HashMap, SortedMap, TreeMap, Hashtable, Properties 등

| Method                               | Description                         |
|--------------------------------------|-------------------------------------|
| void clear()                         | Map의 모든 key-value 쌍을 삭제             |
| boolean containsKey(Object key)      | 지정된 key가 Map에 포함되어 있는지 여부           |
| boolean containsValue(Object value)  | 지정된 value가 Map에 포함되어 있는지 여부         |
| Set entrySet()                       | Map에 포함된 key-value 쌍들을 Set으로 반환     |
| Object get(Object key)               | 지정된 key에 해당하는 value를 반환             |
| int hashCode()                       | Map의 해시코드 반환                        |
| boolean isEmpty()                    | Map이 비어있는지 여부                       |
| Set keySet()                         | Map에 포함된 모든 key들을 Set으로 반환          |
| Object put(Object key, Object value) | 지정된 key와 value를 Map에 추가             |
| void putAll(Map t)                   | 지정된 Map의 모든 key-value 쌍들을 Map에 추가   |
| Object remove(Object key)            | 지정된 key에 해당하는 key-value 쌍을 삭제       |
| int size()                           | Map에 포함된 key-value 쌍들의 개수를 반환       |
| Collection values()                  | Map에 포함된 모든 value들을 Collection으로 반환 |
