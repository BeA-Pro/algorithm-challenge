## 🔗 문제 링크
[더 맵ㅔ](https://school.programmers.co.kr/learn/courses/30/lessons/42626)

## 💻 코드
```java
import java.util.*;

class Solution {
    public int solution(int[] scoville, int K) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        
        for(int i : scoville) pq.add(i);
        int cnt = 0;
        
        while(pq.size()!=1 && pq.peek() < K){
            pq.add(pq.remove() + pq.remove()*2);
            cnt++;
        }
        
        if(pq.peek() >= K) return cnt;
        
        return -1;
    }
}
```

## 📝 해설
그저 우선순위 큐를 위한 문제이다.
`scoville`의 크기가 최대 1,000,000이고 한 번 새로운 스코빌 지수가 생성 될 때마다 그 크기가 1씩 줄어든다. 따라서 O(nlogn)에 이 문제를 해결할 수 있다.

```java
while(pq.size()!=1 && pq.peek() < K){
    pq.add(pq.remove() + pq.remove()*2);
    cnt++;
}
```
그냥 스코빌 지수를 오름차순으로 pq에 넣고 조건에 맞게 계산된 새로운 스코빌 지수를 넣는 것을 반복하여 문제를 해결하였다.