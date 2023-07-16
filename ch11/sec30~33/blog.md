## Comparator and Comparable

- 객체 정렬에 필요한 메서드(정렬기준 제공)를 정의한 인터페이스
- Comparable: 기본 정렬 기준을 구현하는데 사용
- Comparator: 기본 정렬 기준 외에 다른 기준으로 정렬하고자 할 때 사용

```java
public interface Comparator<T> {
    int compare(T o1, T o2); // o1, o2 비교
    // 0: o1==o2, 1: o1>o2, -1: o1<o2

    boolean equals(Object obj); // equals() 오버라이딩
}
```

```java
public interface Comparable<T> {
    int compareTo(T o); // this와 o 비교
}
```

### Comparable

```java
public final class Integer extends Number implements Comparable<Integer> {
    ...

    public int compareTo(Object o) {
        return compareTo((Integer) o);
    }

    public int compareTo(Integer anotherInteger) {
        int thisVal = this.value;
        int anotherVal = anotherInteger.value;
        return (thisVal < anotherVal ? -1 : (thisVal == anotherVal ? 0 : 1));
    }
    ...
}
```
