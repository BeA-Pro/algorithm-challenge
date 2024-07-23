## 🔗 문제 링크
[아이템줍기]
https://school.programmers.co.kr/learn/courses/30/lessons/87694

## 💻 코드
```java
import java.util.*;

class Solution {
    static int answer =0;
    static int[] dx = {1,0,-1,0};
    static int[] dy = {0,1,0,-1};
    static boolean[][] visited = new boolean[101][101];
    static int[][] map = new int[101][101];
    public int solution(int[][] rectangle, int characterX, int characterY, int itemX, int itemY) {
        
        for(int[] rect : rectangle){
            fill(2*rect[0],2*rect[1],2*rect[2],2*rect[3]);
        }

        bfs(characterX*2, characterY*2, itemX*2, itemY*2);
        return answer;
    }
    public void fill(int x1, int y1, int x2, int y2){
        for (int i = x1; i<=x2; i++){
            for (int j = y1; j<=y2; j++){
                if (map[i][j] == 2)continue;
                map[i][j] = 2;
                if (i==x1||i==x2||j==y1||j==y2)map[i][j] = 1;
            }
        }
    }

    static void bfs(int startX, int startY, int itemX, int itemY)
    {
        Queue<int[]> q = new LinkedList<>();
        q.offer(new int[]{startX,startY});
        int[][] cost = new int[101][101];
        cost[startX][startY] = 1;

        while (!q.isEmpty()){
            int[] move = q.poll();

            for (int i = 0; i < 4; i++){
                int moveX = move[0] + dx[i];
                int moveY = move[1] + dy[i];

                if (0>moveX || 0>moveY || moveX>100 || moveY>100)continue;

                if (map[moveX][moveY] == 1 && cost[moveX][moveY] == 0){
                    cost[moveX][moveY] = cost[move[0]][move[1]]+1;
                    q.offer(new int[]{moveX, moveY});
                }
            }
        }
        answer = cost[itemX][itemY]/2;

    }
}
```

## 📝 해설


그려진 사각형의 테두리에서 출발점으로 시작해서 끝점까지 최단거리를 구하는 내용이다.

1. 테두리를 구한다.
2. BFS를 통해 최단거리를 구한다.

이 정도로 단순한 문제인데 테두리를 구할 때 처음에 빈 공간에 대해서 정확한 사각형이 그려지지 않아서
고생을 했는데 넓이를 2배해서 그림으로써 문제를 해결했다.

테두리를 그리고 나서 BFS를 통해 테두리를 따라가면서 진행을 하게 되면 최소 cost가 구해진다.

시간복잡도의 경우에는 직사각형의 모든 좌표값이 1이상 50 이하인 자연수이기 때문에 BFS로 완전탐색을 해도 문제가 없다고 판단함




