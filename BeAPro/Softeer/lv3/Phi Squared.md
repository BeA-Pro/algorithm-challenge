## 🔗 문제 링크
[Phi Squared](https://softeer.ai/practice/7697)

## 💻 코드
```java
import java.util.*;
import java.io.*;

class PhiSquaredInfo{
    long size,index;
    PhiSquaredInfo(int size, int index){
        this.size = size;
        this.index = index;
    }
}

public class Softeer_lv3_PhiSquared {
    static int n;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        n = Integer.parseInt(br.readLine());
        String[] input = br.readLine().split(" ");
        Deque<PhiSquaredInfo> dq = new ArrayDeque<>();
        for (int i = 0; i < n; i++) {
            dq.addLast(new PhiSquaredInfo(Integer.parseInt(input[i]), i + 1));
        }
        while (dq.size()>1) {
            Deque<PhiSquaredInfo> nextDq = new ArrayDeque<>();
            while (!dq.isEmpty()) {
                PhiSquaredInfo cur = dq.removeFirst();
                long prev = 0, next = 0;
                if (!nextDq.isEmpty() && nextDq.peekLast().size <= cur.size) {
                    prev= nextDq.removeLast().size;
                }
                if (!dq.isEmpty() && dq.peekFirst().size <= cur.size) {
                    next= dq.removeFirst().size;
                }
                cur.size+=prev+next;
                nextDq.addLast(cur);
            }
            dq = nextDq;
        }
        System.out.println(dq.peekFirst().size);
        System.out.println(dq.peekFirst().index);
    }
}
```

## 📝 해설
`Deque`를 활용하여 해결 할 수 있는 문제입니다. 하루가 지날 때마다 세포의 수가 최소 반은 줄기 때문에 약 시간 복잡도는 O(NlogN)입니다.

1. dq의 앞에서 미생물을 뽑는다.
2. nextDq의 뒤에서 미생물의 크기가 작다면 흡수한다.
3. dq의 앞에서 미생물의 크기가 작다면 흡수한다.

단순 구현 문제로 `LinkedList`를 사용해도 됐지만 숙련도 문제로 끄적이다 포기했습니다.
아마 `DoublyLikedList`를 직접 구현하는 것이 아니라 `Collections`의 `LinkedList`를 사용하는 것이라면 `Deque`을 사용하는 것이 더 좋을 것 같습니다.

사실 이 문제는 다 풀어놓고 틀렸습니다가 떠서 1시간 넘게 고민했는데 처음 주어지는 세포의 최대 크기가 500,000이기 때문에 `long`형을 사용해야합니다. 수의 크기에 항상 주의하는 습관을 들여야겠습니다.