# 컬렉션과 프레임워크

## 컬렉션

- 여러 객체를 모아 놓은 것

## 프레임워크

- 표준화, 정형화된 체계적인 프로그래밍 방식
    - 프레임워크와 라이브러리
        - 프레임워크: 뼈대나 기반구조를 뜻하며, 개발자가 필요한 기능을 구현할 수 있도록 알맞은 환경을 제공하는 것
        - 라이브러리: 개발자가 작성한 프로그램에서 호출하여 사용할 수 있는 함수들의 집합

## 컬렉션 프레임워크

- 컬렉션을 다루기 위한 프레임워크
- 컬렉션을 쉽고 효과적으로 다룰 수 있는 다양한 클래스를 제공
- java.util 패키지에 구현되어 있음, JDK 1.2부터 지원
- 컬렉션 클래스(Collection class): 다수의 데이터를 저장할 수 있는 클래스(ex: Vector, ArrayList, HashSet, HashMap 등)

- 컬렉션 프레임워크의 핵심 인터페이스
    1. List: 순서가 있는 데이터의 집합, 데이터의 중복을 허용
        - 구현 클래스: ArrayList, Vector, LinkedList, Stack, Queue 등
    2. Set: 순서를 유지하지 않는 데이터의 집합, 데이터의 중복을 허용하지 않음
        - 구현 클래스: HashSet, TreeSet 등
    3. Map: 키(key)와 값(value)의 쌍으로 이루어진 데이터의 집합, 순서는 유지되지 않으며, 키는 중복을 허용하지 않고 값은 중복을 허용
        - 구현 클래스: HashMap, TreeMap, Hashtable, Properties 등
- List와 Set은 모두 Collection 인터페이스를 상속받음
- Map은 Collection 인터페이스를 상속받지 않음