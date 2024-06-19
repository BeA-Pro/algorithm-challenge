## 🔗 문제 링크
[테이블 해쉬 함수](https://school.programmers.co.kr/learn/courses/30/lessons/147354)

## 💻 코드
```java
import java.util.*;

class Solution {
    public int solution(int[][] data, int col, int row_begin, int row_end) {
        int answer = 0;
        Arrays.sort(data,new Comparator<int []>(){
            @Override
            public int compare(int[] o1, int[] o2){
                if(o1[col - 1] == o2[col - 1]){
                    return o2[0] - o1[0]; // 기본키 기준 내림차순
                } else{
                    return o1[col - 1] - o2[col - 1]; // col - 1 기준 오름차순
                }
            }
        });
        
        for(int i=row_begin-1;i<row_end;i++){
            int sum = 0;
            for(int j = 0; j < data[i].length; j++) sum += data[i][j] % (i + 1);
            answer ^= sum;
        }
        
        return answer;
    }
}
```

## 📝 해설
이 문제는 배열을 자유자제로 다룰 수 있는지 판단하는 문제이다.  
data 배열의 길이가 **최대 2500**이므로 시간복잡도가 **O(nlogn)** 인 `Arrays.sort` 메서드를 활용했다.  
`int` 형이 아닌 `int[]`에 대해서 정렬해야 하기 때문에 정렬 기준을 `Comparator<int[]>`를 사용하여 문제 조건에 맞게 정의하였다.



