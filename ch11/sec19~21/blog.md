## Stack & Queue

- Stack 활용 예
    1. 수식계산
    2. 수식괄호검사
    3. 워드프로세서의 Undo/Redo
    4. 웹브라우저의 뒤로/앞으로
- Queue 활용 예
    1. 최근 사용 문서
    2. 인쇄작업 대기목록
    3. 버퍼(Buffer)

### Stack

- 괄호검사

```java
import java.util.Stack;

public class StackTest {
    public static void main(String[] args) {
        final Stack<String> stack = new Stack<String>();
        final String expression = "((3+5*8-2)))";
        System.out.println("expression = " + expression);

        for (int i = 0; i < expression.length(); i++) {
            final char c = expression.charAt(i);
            if (c == '(') {
                stack.push(String.valueOf(c));
            } else if (c == ')') {
                if (stack.isEmpty()) {
                    System.out.println("괄호의 개수가 맞지 않습니다.");
                    return;
                }
                stack.pop();
            }
        }
        if (stack.isEmpty()) {
            System.out.println("괄호의 개수가 맞습니다.");
        } else {
            System.out.println("괄호의 개수가 맞지 않습니다.");
        }
    }
}
```

### Queue

- 인쇄 대기목록

```java
import java.util.LinkedList;
import java.util.Queue;

public class QueueTest {
    public static void main(String[] args) {
        final Queue<String> queue = new LinkedList<String>();
        queue.offer("빨강");
        queue.offer("주황");
        queue.offer("노랑");
        queue.offer("초록");
        queue.offer("파랑");
        queue.offer("남색");
        queue.offer("보라");

        while (!queue.isEmpty()) {
            System.out.println(queue.poll() + " ");
        }
    }
}
```
