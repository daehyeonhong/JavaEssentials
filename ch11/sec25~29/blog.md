## Arrays

- 배열을 다루기 편리한 메서드(static)를 제공한다.

1. 배열의 출력 `toString()`
2. 배열의 복사 `copyOf()`, `copyOfRange()`(새로운 배열을 생성하여 복사)
3. 배열 채우기 `fill()`, `setAll()` (기존 배열에 채우기)
4. 배열의 정렬과 검색 `sort()`, `binarySearch()`
5. 다차원 배열의 출력 `deepToString()`
6. 다차원 배열의 비교 `deepEquals()`

```java
final String[][]str2D1=new String[][]{{"aaa","bbb"},{"AAA","BBB"}};
final String[][]str2D2=new String[][]{{"aaa","bbb"},{"AAA","BBB"}};

        System.out.println(Arrays.equals(str2D1,str2D2)); // false
        System.out.println(Arrays.deepEquals(str2D1,str2D2)); // true
```

7. 배열을 List로 변환 `asList(Object... a)`

```java
final List<String> list=Arrays.asList("aaa","bbb","ccc");
final List<Integer> list2=Arrays.asList(1,2,3);
```

8. Lambda와 Stream
