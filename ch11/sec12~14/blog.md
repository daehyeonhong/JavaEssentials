## LinkedList - 배열의 장단점

- 장점
    - 배열은 구조가 간단하고, 데이터를 읽어오는 시간(접근시간, access time)이 빠름
    - 데이터의 추가/삭제가 용이함
- 단점
    1. 크기를 변경할 수 없음
        - 크기를 변경해야 하는 경우 새로운 배열을 생성 후, 데이터를 복사해야 함
        - 크기 변경을 피하기 위해 충분히 큰 배열을 생성하면 메모리 낭비가 됨
    2. 비순차적인 데이터의 추가, 삭제에 시간이 많이 걸린다.
        - 데이터를 추가하거나 삭제하기 위해, 다른 데이터를 이동해야 함
        - 그러나 순차적인 데이터 추가(끝에 추가)와 삭제(끝부터 삭제)는 빠르다.

### 배열의 단점을 보완

- 배열과 달리 LinkedList는 불연속적으로 존재하는 데이터를 서로 연결(link)한 형태로 구성된 리스트
- 데이터의 삭제: 단 한번의 참조변경만으로 가능
- 데이터의 추가: 한 번의 Node 생성과 두 번의 참조변경만으로 가능
- LinkedList - 연결리스트. 데이터 접근성이 나쁨
- doubly linked list - 양방향 연결리스트. 데이터 접근성이 좋음
- doubly circular linked list - 양방향 순환 연결리스트. head와 tail이 연결되어 있음

### ArrayList vs. LinkedList - 성능비교

1. 순차적으로 데이터를 추가/삭제하는 경우
    - ArrayList가 LinkedList보다 빠름 (ArrayList: 406, LinkedList: 606)
2. 순차적으로 삭제하는 경우
    - ArrayList가 LinkedList보다 빠름 (ArrayList: 11, LinkedList: 46)
3. 중간 데이터를 추가하는 경우(ArrayList: 7382, LinkedList:31)
    - LinkedList가 ArrayList보다 빠름
4. 중간 데이터를 삭제하는 경우
    - LinkedList가 ArrayList보다 빠름 (ArrayList: 6694, LinkedList: 380)
5. 접근시간테스트
    - ArrayList가 LinkedList보다 빠름 (ArrayList: 1, LinkedList: 432)

| Collection | Read(AccessTime) | Add/Remove | Note                             |
|------------|------------------|------------|----------------------------------|
| ArrayList  | 빠르다              | 느리다        | 순차적인 추가삭제는 더 빠름.<br/>비효율적인 메모리사용 |
| LinkedList | 느리다              | 빠르다        | 데이터가 많을수록 접근성이 떨어짐               |
