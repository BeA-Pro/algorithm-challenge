## 🔗 문제 링크
[숫자고르기]
https://www.acmicpc.net/problem/2668

## 💻 코드
```java
import java.io.*;
import java.util.*;

public class Main {
    public static int N;
    static ArrayList<Integer> list;
    static boolean[] visited;
    static int[] num;
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        StringTokenizer st = new StringTokenizer(br.readLine());


        int n = Integer.parseInt(st.nextToken());
        num = new int[n + 1];
        for(int i = 1; i <= n; i++) {
            num[i] = Integer.parseInt(br.readLine());
        }

        list = new ArrayList<>();
        visited = new boolean[n + 1];
        for(int i = 1; i <= n; i++) {
            visited[i] = true;
            dfs(i, i);
            visited[i] = false;
        }

        Collections.sort(list);
        System.out.println(list.size());
        for(int i = 0; i < list.size(); i++) {
            System.out.println(list.get(i));
        }
    }

    public static void dfs(int start, int target) {
        if(visited[num[start]] == false) {
            visited[num[start]] = true;
            dfs(num[start], target);
            visited[num[start]] = false;
        }
        if(num[start] == target) list.add(target);
    }

}



```

## 📝 해설


1. 1->3->1
2. 3->1->3
3. 5->5->5


이런 식으로 계속 반복되면서 사이클이 돌게 됨 DFS로 자기 자신이 될때까지 계속해서 탐색하면 결과 값이 나온다

N의 최대가 100이므로 DFS를 해도 시간복잡도가 O(n^2)으로 최대 연산이 10000번 밖에 일어나지 않기 때문에
완전탐색을 사용하는것이 효과적이다.




## 📌 결과
