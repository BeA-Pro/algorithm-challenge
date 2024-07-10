## 🔗 문제 링크
[튜플]
https://school.programmers.co.kr/learn/courses/30/lessons/64065

## 💻 코드
```java
import java.util.*;

class Solution {
    public int[] solution(String s) {
        s = s.substring(2,s.length()-2).replace("},{","-");
        String str[] = s.split("-");

        Arrays.sort(str,(o1,o2) -> {
            return o1.length() - o2.length();
        });

        List<Integer> arr = new ArrayList<>();
        for(String st : str){
            String[] temp = st.split(",");

            for(String t : temp){
                int i = Integer.parseInt(t);

                if(!arr.contains(i)){
                    arr.add(i);
                }
            }


        }

        int[] answer = new int[arr.size()];
        for(int i=0;i<arr.size(); i++){
            answer[i] = arr.get(i);
        }
        return answer;
    }
}
```

## 📝 해설

문자열 문제를 안 푼지 오래되서 맛보기로 풀어봤음
시작의 {{와 끝의 }}를 지우고, },{ 를 replace를 통해 -로 바꾼뒤 -마다 split을 해주면
각각의 문자열 배열이 생성되게 되는데 이때 길이에 따라 먼저 나오는 문자가 정해지므로
오름차순 정렬로 나열한다. 이후 list에 하나씩 집어 넣으면서 해당 값이 존재하지 않으면 list에
추가하는 방식으로 문제를 풀었다. 

